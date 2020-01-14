---
layout: default
title:  "Rust 2020: Are we IDE yet?"
date:   2019-01-04 14:33:12 +0100
categories: rust
---

# Rust 2020: Are we IDE yet?

IntelliJ CLion is still leading the way for advanced refactoring and polish, but as you may know I've been banging on about the need for decent debuggers for Rust for years. I'm happy to say in 2020 that a good debugging experience is now available through VSCode. (Hopefully Clion will raise their debugging game)

## OSX / Linux / Windows Instructions

(Yes this works _on all major OSes_.)

You will need the latest 1.41 VSCode Code.
    
Rust analyser is now doing [weekly releases](https://github.com/rust-analyzer/rust-analyze/releases) - you can read all about the [latest changes](https://rust-analyzer.github.io/thisweek/2020/01/13/changelog-7.html) (At some point we'll get Rust Analyzer put on the VSCode marketplace)

For now you'll need to save down the server somewhere and download the Rust Analyser vsix file and install it into VSCode by clicking on extensions and the clicking on '...' at the top and then click on "Install from VSIX" 

In the preferences under Extensions, Rust Analyzer 
   - Set the path to the rust analyser server. 
   - I would turn off 'Enhanced Typing' for now as it quite often stops you pressing the enter key. 



## Essential extensions:

The best VSCode debugger for Rust is:

  - Codelldb

Why is this the best rust debugger?

  - msvc and gnu debugging support on windows.
  - break on panic!
  - Visualisers for HashMap, Vec, String and &str.

`Rust Test Lens` extension from [github](https://github.com/hdevalke/rust-test-lens) will enable you to debug specific tests.

## Non essential extensions:

Other extensions you should consider:
  - Arrow Key Debugging (keybindings made by me).
  - GitLens
  - Dracula Intellij Theme
  - Intellij Idea Keybindings
  - Strict Whitespace

### Python fun on OSX and maybe other OSes

_You may not need to do these fun and games but if codelldb still can't find python_...

The Codelldb extention has a setting for where it should find a working Python 3 install.
If the debugger says it can't find python then try setting this.

Apparently python is usually quite messed up on OSX, and in my case this this was no exception.
In order to be able to use python I had to install conda (Anacoda or condamini) and then
```
conda create -n vscode python=3.7
conda activate vscode
open -a "Visual Studio Code"
```
This will set up a working python environment and VSCode should then pick this up.

(Originally written 19/12/2019 but held back till Rust Analyser packaged releases.)
