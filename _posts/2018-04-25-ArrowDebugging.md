---
layout: default
title:  "Arrow Debugging"
date:   2018-04-25 17:33:12 +0100
categories: rust
---

# Debugging Ergonomics

For once this is not another post on some other cool way I've fallen more in love with Rust. For a few years I've been wondering if one could attach the debugger step forward to the mouse wheel. I feel like pressing function keys to step in and out of functions is about as ergonmic as using a qwerty keyboard.

I was close, but better than mucking around with the mouse, using the arrow keys for debugging seems to work in practice extreamly well.

So here are the keybindings:
```
             ^ Step back
             |
Step out <--   ---> Step in
             |
             V Step over
```

I use ALT as a modifer so they don't get in the way of moving the cursor about. At the moment I have replaced 'Step Back' with 'Resume' as I don't have a debugger that goes backwards for python, but I can't recommend that because at some point most debuggers will support the step back. Maybe a poor man's implementation would be just to move
the program counter back to the previous line...

Anyway, give it a try - it works well for me. If people like it maybe we should roll it into an intellij plugin so its easy to deploy.

ttfn,

Giles
