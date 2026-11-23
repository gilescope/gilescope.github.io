---
layout: default
title:  "Pay for a Green Tree Once"
date:   2026-11-19 12:00:00 +0000
categories: ci github git ai
image: /assets/img/pay-for-a-green-tree-once-og.png
---

![A linocut tree: tangled commit-graph roots below the ground line, one clean green canopy above it](/assets/img/pay-for-a-green-tree-once.png)

It is a little-known fact[^1] that every git commit carries a second hash
around with it, in the way that a man might carry a perfectly good umbrella
for twenty years without once opening it. It is the one CI should have been
keyed on all along, and I spent a year finding that out.

The first hash, the famous one, is the commit hash. `git rev-parse HEAD`
gives it to you. It is a fingerprint of everything: the files, who changed
them, when, what they said about it, and which commit came before. It is, in
short, History, and like all History it changes every time someone retells
it.

The second is the tree hash. `git rev-parse HEAD^{tree}` gives you that one.
It is a fingerprint of the files and nothing else. It does not know who you
are. It does not know what time it is. It does not care.[^2]

```console
$ git rev-parse HEAD
548387b9b68944ff6ddba39848bf11be3cabd05b
$ git rev-parse 'HEAD^{tree}'
9f48c9eafa883f2e0f271dc9d5425ee8c25b39ae
```

Two commits with the same files have the same tree hash. Rebase, and the
commit hash changes. Click "Update branch", and it changes. Fix a typo in the
message, and it changes. Push an empty commit so that the DCO bot will stop
sulking, and it changes. Squash onto `main`, and it changes. Through all of
this the tree hash does not move. The commit hash is the code plus the story
about the code. The tree hash is just the code. **If a CI job is a pure
function of the files, then its verdict is a pure function of the tree hash,
and a second run on the same tree is a second payment for the same answer.**

This is what cashing that in looked like on
[midnight-node](https://github.com/midnightntwrk/midnight-node), a Substrate
chain in Rust whose test job takes seventeen minutes when it runs and
thirteen seconds when it does not.

## The three runs

A repository with a merge queue tests the same tree three times, which is
the sort of thing that happens when nobody is technically wrong:

1. On the PR, when the last commit is pushed.
2. In the merge queue, on top of whatever is ahead of it.
3. On `main`, after the squash lands.

If nothing was ahead of it in the queue, all three trees are byte-identical.
Even when something was, run 3 is always the same tree as run 2, because the
queue merged exactly what it tested, and `main` then receives those exact
bytes and examines them again out of what can only be described as
politeness. Keyed on commit hash, those are three different builds. Keyed on
tree hash, they are one. Nothing changed between them except the story.

Release branches get the same gift, with interest, and they do not even need
the queue, which is as well because most of them do not run one. A fix goes
into `release/2.1` straight from the PR, and if the PR was up to date with
the branch, the squash is the PR's tree exactly. The push to the branch
builds images tagged by tree, finds them already in the registry from the PR
run, and builds nothing. The candidate is then
cut from a ref whose images already exist, so cutting it is mostly a re-tag.
A release candidate used to wait for a full build; now it waits for the parts
nobody can skip, which is the nearest thing CI has to a free lunch, and like
all free lunches it was paid for earlier, by you. A cherry-pick onto a release
branch is a different tree, because the base is different, and pays once like
any other first sighting.

## Efficient use of the GitHub Actions cache

I wrote a small composite action with the soul of a librarian,
[tree-cache-guard](https://github.com/midnightntwrk/midnight-node/blob/main/.github/actions/tree-cache-guard/action.yml),
and wrapped each job in it. Stripped to the idea:

```bash
tree=$(git rev-parse "HEAD^{tree}")
key="passed-${WORKFLOW_NAME}-${CHECK_NAME}-${RUNNER_ARCH}-${ImageOS}-${tree}"

hits=$(gh cache list --repo "$GITHUB_REPOSITORY" --key "$key" \
         --json id --jq 'length')
echo "hit=$(( hits > 0 ))" >> "$GITHUB_OUTPUT"
```

Every real step in the job carries `if: steps.guard.outputs.hit != 'true'`.
If the librarian already has the card, the job quietly puts its coat back on
and leaves. If not, the job runs as it always did, and a last step files the
card: a one-file directory saved to the Actions cache under that key.

```yaml
- uses: ./.github/actions/tree-cache-guard/save
  if: steps.guard.outputs.hit != 'true'
  with:
    key: ${{ steps.guard.outputs.key }}
```

The file is empty and called `ok`. The key is the message.[^3] Each sentinel
costs about 249 bytes of the repository's 10 GB cache budget, and the
thousand of them I listed this morning come to 249 KB, which is to say that
a year's worth of remembered verdicts would fit on a floppy disk with room
left over for the manual.

The card names the workflow, the job, the runner architecture and the runner
image as well as the tree, because the same tree does not mean the same
verdict if the job has moved from `ubuntu24` to `ubuntu26`, and an `arm64`
pass says nothing whatsoever about `x64`. Matrix jobs add their matrix value
as a suffix for the same reason. The librarian is indifferent, not careless.

## What it bought

Over the 30 days to 2026-11-19 the guard wrapped 9,210 job runs across those
seven workflows. 1,497 of them were hits, about one in six, and where they
fell is the whole story:

| event          | hits | misses | hit rate |
| -------------- | ---- | ------ | -------- |
| pull request   | 477  | 6,449  | 7%       |
| merge queue    | 753  | 1,162  | 39%      |
| push to `main` | 238  | 101    | 70%      |

A PR run is usually the first time anyone has seen that tree, so it pays. The
queue run is the same tree as the PR about two times in five. The `main` run
is the same tree as the queue seven times in ten.

Pricing each hit at the mean duration of a miss on the same job, those 1,497
hits were worth 11,400 runner-minutes, 190 hours, in one month. The guard is
not free: the lookup ran 9,210 times at about a second a go, 113 minutes in
all, and the 1,497 hits still had to check out and ask, 343 minutes between
them. That is 456 minutes of overhead against 11,400 saved, one minute spent
for every 25 saved. Net, the guard took 17.6% off a month that would
otherwise have cost 1,050 hours of runner time, and the 184 hours it kept is
a working month of machines, every month, purchased with an empty file. The
heaviest hitters:

| job                     | runs | hits | miss mean | saved |
| ----------------------- | ---- | ---- | --------- | ----- |
| Formatting and Linting  | 575  | 156  | 18 min    | 47 h  |
| Run tests               | 503  | 137  | 17 min    | 39 h  |
| Local Environment Tests | 366  | 48   | 27 min    | 21 h  |
| Test Toolkit            | 392  | 59   | 21 min    | 20 h  |

A hit on `Run tests` takes 13 seconds, and most of the 13 is the checkout,
which is the time it takes the librarian to find her glasses.

Twenty-one jobs across seven workflows are guarded today, up from the twenty
I landed in
[#889](https://github.com/midnightntwrk/midnight-node/pull/889) in May. Each
check has about 53 distinct trees in the cache at once, across 47 refs, which
is roughly a week of the team's work at the cache's seven-day idle
eviction.[^4]

I had landed the same idea one layer down two months earlier, in
[#783](https://github.com/midnightntwrk/midnight-node/pull/783): Docker
image tags switched from `{version}-{8-char-commit}-{arch}` to
`{version}-{12-char-tree}-{arch}`, and the build job checks the registry for
the tag before building anything. The ADR for that one is
[in the repo](https://github.com/midnightntwrk/midnight-node/blob/main/docs/decisions/0004-tree-content-hash-image-tags.md),
including the arithmetic for twelve characters: 48 bits puts the birthday
bound near 16 million objects, where eight characters sat at about 65
thousand, which is uncomfortably close for a registry that keeps every tag
and never forgets a face. Commit-hash alias tags are still created, so
`docker pull` by commit works and so does the reverse lookup from an image to
every commit that produced it.

## Where it bit

**The lookup is an optimisation, never a gate.** Three months in, somebody's
job went red with this:

```text
tls: failed to verify certificate: x509: certificate is not valid for any
names, but wanted to match api.github.com
```

A runner's egress was being intercepted by something that spoke TLS but could
not produce a certificate with the right name on it. `gh cache list` failed,
and the guard, whose entire purpose was to save the build time, failed the
build. The bug report I wrote that day is the whole design rule:

> If we can't add to the cache that should not fail the build, but if we
> can't read from the cache that shouldn't fail the build either - we should
> just consider it a cache miss and run the build step.

In [#2021](https://github.com/midnightntwrk/midnight-node/pull/2021) I made
the lookup retry three times, five seconds apart, and treat anything that is
not a non-negative integer as a miss. The save step was already
`continue-on-error: true`. The clerk who notes that you passed must never be
allowed to fail you.

**A tree is not enough when the workflow came from somewhere else.** Some
events run the workflow file from a different commit than the one checked
out, so the tree hash describes code the workflow did not come from. The
guard compares `github.workflow_sha` with `github.sha` and refuses to
consult the cache when they differ. Those runs always execute. A librarian
will file anything, but she does want to know which book it is.

**The lookup is blind to refs, and that is both the feature and the catch.**
The Actions cache is scoped: a run can restore entries from its own branch
and its base, and
[nothing else](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/caching-dependencies-to-speed-up-workflows#restrictions-for-accessing-a-cache).
A sentinel written on `refs/pull/1523/merge` is not restorable from
`refs/heads/main`. The guard never restores anything; it asks the REST API
whether the key exists, and the REST API lists the whole repository. That is
exactly why the PR run's pass is visible to the queue run and the `main` run.

It is also why a job on `main` can be skipped on the strength of a run that
happened on a PR. For `cargo test`, `cargo fmt` and `actionlint` that is the
point: same tree, same answer. For a check whose result has to be recorded
against the default branch, a code-scanning upload for instance, it is a bug,
and I have been round that loop once. The obvious fix, swapping the API call
for `actions/cache/restore` with `lookup-only: true`, resolves scope
correctly and would un-skip every job on `main`, giving back most of what the
guard bought. If a job needs the strict behaviour, it should opt out of the
guard, not change the guard. Both things are true. This is allowed.

## The rule

Key your CI on what the job actually reads. A commit hash encodes history,
and a job does not care about history. Neither does a sign-off, a rebase or
a tidier commit message. The tree hash was sitting in every checkout the
whole time, one `^{tree}` away, like the umbrella.

What this is, if you squint, is a poor man's deterministic build system.
Nix, Bazel and Buck2 key every action on a hash of its inputs and skip the
ones that have already been done. This keys one action, the whole job, on a
hash of every input at once, and skips it the same way. You get a little of
their power for the price of a shell script and an empty file, and you do
not get the rest: a one-line change to the README is a new tree, and the
test job runs again in full, because the guard cannot tell which files a job
reads.

The next fence is cheaper than it looks, because git already hands you the
hash of any subdirectory: `git rev-parse HEAD:docs` is the tree of `docs/`
and nothing else, and a job that only reads `docs/` can be keyed on it, after
which README churn stops costing it anything. The catch is honesty. A key
that says "only `docs/`" is a promise, and a job will break it the moment
someone adds a step that peeks at a sibling. The cheap way to keep the
promise is to make it impossible to break: once the checkout is done, delete
everything the key does not cover, and a job that reaches outside its
subdirectory falls over on the spot instead of quietly caching a lie. Past
that, the proper tools already know how to build the rest of the fence.
Until then, the rule is the same at any granularity.

Pay for a green tree once.

---

*Timings and cache counts were pulled from the GitHub API on 2026-11-19.*

[^1]: Little-known in the sense that it is written in the manual, which is
    where facts go to be safe from people.

[^2]: It is, in this respect, much like a cat, but reproducible.

[^3]: There is a school of thought that says a cache entry ought to contain
    something. This school has never had to pay for the bandwidth.

[^4]: Seven days is also about the right lifetime for a sentinel: longer than
    a PR, shorter than anyone's memory of why it was there.
