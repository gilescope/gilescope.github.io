---
layout: default
title:  "A Year of Merge Queue Lessons"
date:   2026-10-16 19:00:00 +0000
categories: ci github rust ai
---

A merge queue has one job: never let a red commit onto `main`. Ours once
spent a day refusing to let anything onto `main` at all.

This is a year of running GitHub's merge queue on
[midnight-node](https://github.com/midnightntwrk/midnight-node), a Substrate
chain in Rust with seventeen required checks and, at its busiest, 144 PRs
landing on `main` in a month. Most of what follows was learned the way CI
lessons are always learned, which is by a PR that should have merged and did
not. Claude did a lot of the digging; the quotes are from those sessions.

## Why a queue at all

Without a queue, "require branches to be up to date" makes every PR merge
`main` and re-run CI before it can land. On a busy trunk that serialises
merges at one per CI run. With a queue, GitHub builds each PR on top of the
PRs ahead of it and lands them in order, so CI runs overlap.

Four dependabot PRs, 25 minutes of CI each:

| strategy                  | wall clock |
| ------------------------- | ---------- |
| up-to-date, one at a time | ~100 min   |
| merge queue, in parallel  | ~25 min    |

That was the pitch. Here is the bill.

## The ledger

Each entry is one thing the queue taught us, with the PR that paid for it.

**Every required check must fire on `merge_group`.**
[#240](https://github.com/midnightntwrk/midnight-node/pull/240). The queue
builds a synthetic branch, `gh-readonly-queue/main/...`, and triggers a
`merge_group` event, not a `pull_request`. A workflow that only listens for
`pull_request` never runs, the check never reports, and the queue waits out
its timeout before dequeuing the PR. Eight workflows, eight one-line fixes.

**Concurrency groups keyed on the branch cancel the queue.**
[#250](https://github.com/midnightntwrk/midnight-node/pull/250). The usual
"cancel the previous run of this PR" idiom groups by `head_ref`. Queue
entries share one, so each new entry cancelled the one before it. The fix is
to give queue runs their own group:

```yaml
concurrency:
  group: ${{ github.event_name == 'pull_request' && format('{0}-{1}', github.workflow, github.head_ref) || github.run_id }}
  cancel-in-progress: true
```

**A skipped job passes. That cuts both ways.**
[#254](https://github.com/midnightntwrk/midnight-node/pull/254) is the trap:
jobs guarded with `if: github.event_name == 'pull_request'` skipped on queue
runs, and GitHub counts a skipped required check as green. The queue was
merging PRs it had not tested.
[#660](https://github.com/midnightntwrk/midnight-node/pull/660) is the
feature: the same rule lets you keep a flaky job out of the queue with
`if: github.event_name != 'merge_group'` while leaving it on PRs.

**Anything that touches the network will eject a PR eventually.**
Link checker 503s ([#278](https://github.com/midnightntwrk/midnight-node/pull/278)),
advisory database fetches ([#660](https://github.com/midnightntwrk/midnight-node/pull/660)),
Rekor uploads for SBOM attestation ([#781](https://github.com/midnightntwrk/midnight-node/pull/781)),
and finally the Actions cache API itself
([#2021](https://github.com/midnightntwrk/midnight-node/pull/2021)). An ejected
PR re-queues from the back. The rule that emerged: a queue check may only
depend on the repo and the runner. Network checks run on the PR, on the push
to `main`, and nightly, which loses nothing. The cache fix says it best:

> The lookup is an optimisation, never a gate: any failure (API outage, TLS
> interception, rate limit, malformed output) must degrade to a cache miss so
> the job runs, rather than failing the build.

**The queue is only as fast as your runner pool.**
[#556](https://github.com/midnightntwrk/midnight-node/pull/556). Five queue
entries building at once starved the shared 16-core self-hosted pool, so the
whole queue slowed down. Moving non-critical jobs to free 4-core runners cut
16-core use elevenfold. From the PR:

> If the build takes 1h instead of 30m but we can land 6 PRs in that hour then
> we're effectively landing one every 10 mins.

Queue concurrency went 5, then 2, then settled at 3 or 4. The check timeout
went from 60 to 180 minutes, because a slow day was kicking out builds that
were nearly done.

**Pay for a green tree once.**
[#889](https://github.com/midnightntwrk/midnight-node/pull/889). A PR goes
green, enters the queue, and lands on `main`. If `main` has not moved, all
three runs build the same tree. `git rev-parse HEAD^{tree}` is a content hash
of the whole repo, so each job checks the Actions cache for a sentinel keyed on
it, and exits in seconds on a hit. The cache ignores ref scope, which is what
makes the PR run's sentinel visible to the queue run. Twenty jobs across six
workflows.

**The day the queue froze.**
[#1812](https://github.com/midnightntwrk/midnight-node/pull/1812). We added
`DCO` to the required checks. The DCO probot app only reports on
`pull_request` events. So every merge group waited the full 180 minutes for a
check that would never arrive, was dequeued, and the next one started
waiting. Four PRs sat in the queue for a day, each expelled on a three-hour
cycle, while every individual check was green. Someone removed `DCO` from the
ruleset; an hour later a Terraform apply put it back and the queue refroze.

The fix is a shim: a workflow on `merge_group` whose only job is named `DCO`
and whose only step is an `echo`. Required checks match by context name, so
it satisfies the ruleset. It is not a bypass, because a PR cannot enter the
queue until the real probot check on the PR itself is green, and the merge
group carries those same commits. Two things the shim must not do: re-validate
sign-offs on the queue's commit, because GitHub's generated squash commit may
lack `Signed-off-by` even when every PR commit had it; and listen on
`pull_request`, because then any PR could forge its own DCO pass. CODEOWNERS
on `.github/` is what guards the second.

**Rename a required check and the queue wedges silently.**
Converting a sequential job into a matrix split `Startup E2E in dev mode`
into `... (ledger-8)` and `... (ledger-9)`. The ruleset still wanted the old
name, which now never reported. Same failure as DCO, no app involved. The
ruleset and the workflow have to change in the same breath.

**Draft to ready does not re-run CI.**
On the sibling repo, midnight-zk,
[#481](https://github.com/midnightntwrk/midnight-zk/pull/481) merged with
Rustfmt and five test jobs skipped. It was opened as a draft, the draft
condition skipped the tests, and marking it ready did not trigger a run.
Skipped is green. The fix is one word in the trigger,
[#548](https://github.com/midnightntwrk/midnight-zk/pull/548):

```yaml
pull_request:
  types: [opened, synchronize, reopened, ready_for_review]
```

## When not to use one

A queue serves one target branch. midnight-zk works in stacks, each PR
targeting the one below it, and only the bottom of a stack targets `main`.
Claude recommended a queue there anyway, twice.

> **Giles:** a merge queue is a queue (or one queue per target branch) - I'm
> not sure it's quite right here.
>
> **Claude:** The timelines bear you out on the merge queue: it doesn't fit
> midnight-zk. I anchored on midnight-node's setup.

A second-opinion subagent then re-recommended it. Claude rejected that one
with the same reason. At three merges a week there was no contention to
solve.

The other correction went the opposite way. The plan for the DCO shim was a
three-step dance through infrastructure-as-code: drop the required check,
drain the queue, land the shim, re-add the check. It turns out a PR that adds
a `merge_group` workflow runs that workflow in its own queue entry, so the
shim satisfies the check it introduces. One PR.

## Where it stands

| midnight-node `main` today                |            |
| ----------------------------------------- | ---------- |
| required status checks                    | 17         |
| merge method in queue                     | squash     |
| merge-group CI runs to date               | ~2,500     |
| PRs landed on `main`, best month (Mar 26) | 144        |

A queue is a promise that `main` is green. Everything above is the list of
ways we accidentally promised something else.

---

*Written with Claude (the CI work over the year with several Claude models,
this post with claude-fable-5-1). PR numbers link to the public repos; the
incident timings come from the workflow comments and session notes, not from
memory.*
