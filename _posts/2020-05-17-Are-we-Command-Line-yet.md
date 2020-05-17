---
layout: default
title:  "2020: Are we command line yet?"
date:   2019-01-04 14:33:12 +0100
categories: windows
---

# 2020: Are we Command Line yet?


## OSX / Linux / Windows Instructions

(Yes this works _on all major OSes_.)

Once there was sh, then bash, then fish came along with auto-suggest and things were _so_ much better. When you type a command it will suggest the rest and you just arrow right if that's exactly what you wanted to do. It's so good I can't go back to not having it. (There are other good things about fish but autosuggest was the killer).

I tend to hop across operating systems pretty frequently. It would be nice to use the same shell on all OSes. I've tried fish on windows and while it works pretty well I still feel a second class citizen.

Over the years meanwhile PowerShell has got leaner and meaner (It still seems at least a 50mb hit on a docker image though!). Since v6 it's crossplatform as pwsh and since v7 it now understands '&&' for running multiple jobs one after another.

Long story short, PSReadLine has nacent autosuggest support (on the 'fish' branch) and with posh git and oh my posh I think we've got ourselves a crossplatform shell that's pretty good on all platforms. 

## TL/DR:

   * Get pwsh 7
   * Install-Module PSReadLine -AllowPrerelease -Force 
   * Install-Module posh-git -Scope CurrentUser
   * Install-Module oh-my-posh -Scope CurrentUser

Then in your $profile you can set your prompt:
Set-Prompt

(The PSReadLine has the fish prompt)

Is this better than bash everywhere? In 2020 I think so.
(And don't forget to grab [Windows Terminal](https://github.com/Microsoft/Terminal) if you can - it's great - I can run `vi` and `tig` in it with no trouble!)
## References

[Fishy Readline](https://github.com/PowerShell/PSReadLine/issues/687)
