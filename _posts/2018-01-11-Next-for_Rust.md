---
layout: default
title:  "Next for Rust"
date:   2018-01-11 17:33:12 +0100
categories: rust
---

# Next for Rust in 2018

There's been a lot of good solid progress last year. For me one of the big things was line numbers on the stacktraces in OSX. My prediction for 2018 is that Rust on WebAssembly rather than being a distracting side-show will catch the eye of the mainstream JavaScript community. (Getting the sourcemaps working was a nice touch btw.) 

## Consolidation:

With NLL (non-lexical-lifetimes), procedural macros, incremental compilation and a few other big changes landing in the Rust language it's important that we concentrate on finishing things rather than starting new RFCs. The run rate has been swift as these changes have been integrated but it's time to let the language settle so that these can stabilise, people can really build on-top of them and we can then see what should be changed next. It feels like we're getting towards the end of an epoc... and to that end we should be trying to ensure that futures (Tokio) and Hyper have stable 1.0 releases. People should not have to rely on nightly builds of the compiler (esp. for production environments).

## Enterprise:

Private repositories (native support in JFrog's artifactory) are one of the next stepping stones. As too is rebuilding the test runner so that it can support various CI tools out of the box. We've long past the point where everyone who wanted CI was expected to roll their own CI setup. There should be some standard apporches so that private CIs (E.g. TemaCity) and public CIs (E.g. Travis)  work out of the box.

## Debugging:

In many ways Rust is an easy low level language to use, but compared to Java/C# the debugging experiance is well below par.
 
	- We need both a robust debugger that manages to attach to the process every time (not just half the time). 
	- We need to be able to set the next instruction pointer. 
	- Most importantly of all we need to have first class debuging symbols for LLDB. I.e. Rust generating specific rather than C/C++ metadata to LLDB when compiling. The LLDB debuggger needs to be enhanced so that we can see things like Strings, HashMaps and generic types - ideally making use of the Debug trait as a generic print mechanism. 
	- We need to get the lldb repl working with Rust.

## Error handling:

I think the Failure crate is a good step forwards - getting error handling right makes a world of difference to development speed.
panic! should give file and line numbers. Let's tee this up as one of the first things in the next epoc.

# Community:

I have not one bad word to say about the Rust community - if it can stay this nice while growing I think that's as good as it gets. I wish everyone involved and yet to be involved in Rust a happy 2018

