---
layout: default
title: "Deployment"
date: 2016-02-12 00:00:00 +0000
---


Deployment is a subject dear to anyone's heart who's current deployment system is sub-optimal. Safe rapid deployment is at the heart of the dev-ops movement.

<h3>Spec</h3>

What do we want out of a good deployment system?

<ul>
 <li>One click (partial) Rollback</li>
 <li>Speed (if it's too slow this can affect rollback)</li>
 <li>Consistency (and ideally monitoring of that consistency)</li>
 <li>Hands free automation - people shouldn't need to log into boxes.</li>
 <li>Promotion of releases from one environment to another.</li>
</ul>

In many ways we want to consider managing environments as a whole, rather than concerning ourselves with the implementation of the individual machines.

<h3>Windows Implementations</h3>

I focus on windows here as it seems a harder problem to solve. Linux seems to have apt-get package management systems that coupled with Puppet or some other newer deployment system seem to manage most of the above.

For Windows the landscape is changing rapidly. It started with <a href="http://nget.org" target="_blank">NuGet</a> which is a dll dependency finder for .Net, but which has now been used as a distribution mechanism by <a title="Install system for Windows" href="https://chocolatey.org/" target="_blank">Chocolatey</a>. This then gives us a package manager for Windows, with dependencies thrown in.

It's good, but it's not enough to install MSIs, we have to ensure the other bits like setting up shares, configuring firewalls and the like are also done if we're going to truly have one click deployment.

<h4>Enter stage left, Powershell DSC.</h4>

Powershell is a puppet-esk declarative config for specifying how a machine should be configured (think /etc for windows). It can install Chocolatey packages and configure the other bits and pieces.

The down side: It's lacking a UI / website, which means the barrier for entry is still a bit high. On the plus side it looks like this will be the de-facto way of configuring windows, with hundreds of DSC modules coming out (wave after wave of them).

There are other alternatives, CA's Nolio and <a href="https://octopusdeploy.com" target="_blank">Octopus Deploy</a> being some that seem to be getting a reasonable amount of purchase (and Puppet can use DSC modules if you're in a hybrid environment). Indeed Octopus Deploy has recently open sourced its configuration modules (which someone will make callable from Puppet &amp; DSC no doubt).

And just recently MicroSoft has announced their first steps of <a href="http://blogs.msdn.com/b/powershell/archive/2015/05/06/powershell-dsc-for-linux-is-now-available.aspx" target="_blank">Linux support for Powershell DSC</a>. Puppet really will have competition!

(Interestingly Windows getting built-in support for SSH will make things like Puppet on Windows easier to set-up - this can only be a good thing!)

<hr />

Why am I not talking about Windows Nano server and Docker in this article? It's because you need to be able to automate building an image before you deploy it across lots of servers.

You wouldn't take a build from a developers machine and put it in production, you'd take it from the CI server. It's the same here - don't put an image you can't recreate into production - it will bite back. (Let's call this the George's Marvelous Medicine principle - reproducibility is key! )

Once you can do this, it's time to move up the stack and have <a href="https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/manage_powershell" target="_blank">fun with containers</a>.
