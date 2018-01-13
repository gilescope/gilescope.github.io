---
layout: default
title:  "Next for Rust"
date:   2018-01-11 17:33:12 +0100
categories: rust
---

# Next for Rust in 2018

There's been a lot of good solid progress last year. For me one of the big things was line numbers on the stacktraces in OSX. My prediction for 2018 is that Rust on WebAssembly rather than being a distracting side-show will catch the eye of the mainstream JavaScript community. (Getting the sourcemaps working was a nice touch btw.) 

The Intelli Rust plugin has made huge gains over the year and is starting to push the envolope on what IDEs are capable of - great to see new ideas and innovation in the IDE space. We're getting past playing catchup and starting to push the boundries. Alas without better debugging support in the compiler and LLDB I think they will be limited in what they can do to improve the debug experience (more on this later).

## Consolidation:

With NLL (non-lexical-lifetimes), procedural macros, incremental compilation and a few other big changes landing in the Rust language it's important that we concentrate on finishing things rather than starting new RFCs. The run rate has been swift as these changes have been integrated but it's time to let the language settle so that these can stabilise, people can really build on-top of them and we can then see what should be changed next. 

It feels like we're getting towards the end of an epoc... and to that end we should be trying to ensure that futures (Tokio) and Hyper have stable 1.0 releases. People should not have to rely on nightly builds of the compiler (esp. for production environments).

## Enterprise:

Private repositories (native support in JFrog's artifactory) are one of the next stepping stones. As too is rebuilding the test runner so that it can support various CI tools out of the box. 

We've long past the point where everyone who wanted CI was expected to roll their own CI setup. There should be some standard apporches so that private CIs (E.g. TeamCity) work out of thr box just like the public CIs do (E.g. Travis).

## Debugging:

In many ways Rust is an easy low level language to use, but compared to Java/C# the debugging experience is well below par.
 
	- We need a debugger that attaches to a process every time 
		- (not just half the time). 
	- We need to be able to set the next instruction pointer. 
	- We need to have first class debuging symbols for LLDB: 
		- Rust compiler to generate Rust metadata for LLDB 
			- (Currently generates C/C++ metadata). 
		- The LLDB debuggger needs to visualise:
			- Strings and &str
			- Vec
			- HashMaps 
			- generic types 
		- Use the Debug trait as a generic print mechanism. 
	- We need to get the lldb repl working with Rust.

And of course we need the above in Windows and OSX as well as Linux.

## Error handling:

I think the Failure crate is a good step forwards - getting error handling right makes a world of difference to development speed.

panic! should give file and line numbers. Let's tee this up as one of the first things in the next epoc.

# Community:

I have not one bad word to say about the Rust community - if it can stay this nice while growing I think that's as good as it gets. I wish everyone involved and yet to be involved in Rust a happy 2018

