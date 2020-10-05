---
layout: default
title:  "Rustt 2021: Foundation"
date:   2020-10-05 00:00:00 +0000
categories: rust
---

# Rust 2021: Foundation

I work in the finance industry and we use Rust and Python as our main languages. These are the few niggles and many things that we're excited to see progress about in the upcoming year:

## Foundation

   * Create Rust Foundation v0.1. Breaking changes expected!

## Language - finish off work in progress:

   * Stabler ABI

   * Switch to new name mangling scheme: https://github.com/rust-lang/rust/issues/60705

   * Runtime ABI - allow rust binaries to interoperate directly across mono-morphic boundaries without reducing to using plain C struct/funcs.

   * Allow for multiple dynamically linked rust components in the same build, establish protocol for verifying type layout are consistent across shared libraries.

   * A big push to reduce work in progress and get the chalk as the main trait solver. - https://github.com/rust-lang/rust/issues/48049

   * We would like to see the error handling WG produce a blessed error handling crate, much like the futures crate has been blessed.

   * Please stabilize minimal specialization https://github.com/rust-lang/rust/pull/68970

## The Compiler - Better compile times and less compiling

   * Don't compile unless you really have to (avoid cascades of recompilation) - mtimes independent builds that can be 'fresh' even if we're using docker layers or we've copied the files from somewhere else.

   * sccache doesn't cache enough of the crates to be worthwhile - we need it to understand more of rustc's arguments / find some way to be more aggressive at caching?

   * CraneLift gets enough performance optimizations that we could use it. For our tests to run quickly we need them to run in release mode. (I hear this is a long shot at the moment as it doesn't do any inlining.

   * Linker performance: heavyweight LTO and dependency on GNU ld/gold slows down development cycles, even for relatively small projects (on linux) have over 1 minute link times before a useful component can be delivered. (Maybe we should switch to lld...)

   * Can we unify cargo check and cargo build so that cargo build can use cargo check's metadata?
## Cargo:

   * Features working at a workspace level please! https://internals.rust-lang.org/t/features-and-workspaces-request-for-meta-issue/11964

   * Commands like git has to be able to get/set config entries from scripts.

   * .cargo/config doesn't allow environment variables to be embedded within it and those to be resolved. We can set CARGO_* env vars as a workaround, but It would be nice to have.

## Ecosystem:

   * Better integration with CIs like Teamcity and especially Artifactory (https://www.jfrog.com/jira/browse/RTFACT-13469).

   * language integration with the most popular dynamic language (python) - Pyo3 is great - we look for even more refinement over the next year and see some alternative approaches that might be faster or have simpler integration - possibly via reflection of a standard runtime ABI (see above) - avoid macro-bloat to generate simple wrappers (or maybe pyo3 to adopt https://github.com/dtolnay/watt ?).

   * Conda packages: Like a lot of big data companies we use conda extensively. Having more of the rust tooling pre-packaged in conda-forge so that windows and linux users could just `conda install` the packages rather than having to manually compile them at point of use would be excellent. It's great to be able to type `conda install ripgrep --channel conda-forge` and not have to wait for it to compile, but we'd like to do that for `cargo-expand`, `sccache` and many others.


Hope this helps!

With kind regards,

Giles