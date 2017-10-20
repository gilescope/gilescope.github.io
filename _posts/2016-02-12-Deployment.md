                                                                                               |
| Deployment is a subject dear to anyone's heart who's current deployment system is sub-optimal. Safe rapid deployment is at the heart of the dev-ops movement.

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

For Windows the landscape is changing rapidly. It started with <a href="http://nget.org" target="_blank">NuGet</a> which is a dll dependency finder for .Net, but which has now been used as a distribution mechanism by <a title="Install system for Windows" href="https://chocolatey.org/" target="_blank">Chocolatey</a>.  This then gives us a package manager for Windows, with dependencies thrown in.

It's good, but it's not enough to install MSIs, we have to ensure the other bits like setting up shares, configuring firewalls and the like are also done if we're going to truly have one click deployment.

<h4>Enter stage left, Powershell DSC.</h4>

Powershell is a puppet-esk declarative config for specifying how a machine should be configured (think /etc for windows).  It can install Chocolatey packages and configure the other bits and pieces.

The down side: It's lacking a UI / website, which means the barrier for entry is still a bit high. On the plus side it looks like this will be the de-facto way of configuring windows, with hundreds of DSC modules coming out (wave after wave of them).

There are other alternatives, CA's Nolio and <a href="https://octopusdeploy.com" target="_blank">Octopus Deploy</a> being some that seem to be getting a reasonable amount of purchase (and Puppet can use DSC modules if you're in a hybrid environment). Indeed Octopus Deploy has recently open sourced its configuration modules (which someone will make callable from Puppet &amp; DSC no doubt).

And just recently MicroSoft has announced their first steps of <a href="http://blogs.msdn.com/b/powershell/archive/2015/05/06/powershell-dsc-for-linux-is-now-available.aspx" target="_blank">Linux support for Powershell DSC</a>. Puppet really will have competition!

(Interestingly Windows getting built-in support for SSH will make things like Puppet on Windows easier to set-up - this can only be a good thing!)

<hr />

Why am I not talking about Windows Nano server and Docker in this article? It's because you need to be able to automate building an image before you deploy it across lots of servers.

You wouldn't take a build from a developers machine and put it in production, you'd take it from the CI server. It's the same here - don't put an image you can't recreate into production - it will bite back. (Let's call this the George's Marvelous Medicine principle - reproducibility is key! )

&nbsp;

Once you can do this, it's time to move up the stack and have <a href="https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/manage_powershell" target="_blank">fun with containers</a>. |
| Deployment is a subject dear to anyone's heart who's current deployment system is sub-optimal. Safe rapid deployment is at the heart of the dev-ops movement.

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

For Windows the landscape is changing rapidly. It started with <a href="http://nget.org" target="_blank">NuGet</a> which is a dll dependency fetcher for .Net, but which has now been used as a distribution mechanism by <a title="Install system for Windows" href="https://chocolatey.org/" target="_blank">Chocolatey</a>.  This then gives us a package manager for Windows, with dependencies thrown in.

It's good, but it's not enough to install MSIs, we have to ensure the other bits like setting up shares, configuring firewalls and the like are also done if we're going to truely have one click deployment.

<h4>Enter stage left, Powershell DSC.</h4>

Powershell is a puppet-esk declarative config for specifying how a machine should be configured (think /etc for windows).  It can install Chocolatey packages and configure the other bits and pieces.

The down side: It's lacking a UI / website, which means the barrier for entry is still a bit high. On the plus side it looks like this will be the de-facto way of configuring windows, with hundreds of DSC modules coming out (wave after wave of them).

There are other alternatives, CA's Nolio and <a href="https://octopusdeploy.com" target="_blank">Octopus Deploy</a> being some that seem to be getting a reasonable amount of purchase (and Puppet can use DSC modules if you're in a hybrid environment). Indeed Octopus Deploy has recently open sourced its configuration modules (which someone will make callable from Puppet &amp; DSC no doubt).

And just recently MicroSoft has announced their first steps of <a href="http://blogs.msdn.com/b/powershell/archive/2015/05/06/powershell-dsc-for-linux-is-now-available.aspx" target="_blank">Linux support for Powershell DSC</a>. Puppet really will have competition!

(Interestingly Windows getting built-in support for SSH will make things like Puppet on Windows easier to set-up - this can only be a good thing!)

<hr />

Why am I not talking about Windows Nano server and Docker in this article? It's because you need to be able to automate building an image before you deploy it across lots of servers.

You wouldn't take a build from a developers machine and put it in production, you'd take it from the CI server. It's the same here - don't put an image you can't recreate into production - it will bite back. (Let's call this the George's Marvelous Medicine principle - reproducibility is key! )

&nbsp;

Once you can do this, it's time to move up the stack and have <a href="https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/manage_powershell" target="_blank">fun with containers</a>. |
| Deployment is a subject dear to anyone's heart who's current deployment system is sub-optimal. Safe rapid deployment is at the heart of the dev-ops movement.

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

For Windows the landscape is changing rapidly. It started with <a href="http://nget.org" target="_blank">NuGet</a> which is a dll dependency finder for .Net, but which has now been used as a distribution mechanism by <a title="Install system for Windows" href="https://chocolatey.org/" target="_blank">Chocolatey</a>.  This then gives us a package manager for Windows, with dependencies thrown in.

It's good, but it's not enough to install MSIs, we have to ensure the other bits like setting up shares, configuring firewalls and the like are also done if we're going to truly have one click deployment.

<h4>Enter stage left, Powershell DSC.</h4>

Powershell is a puppet-esk declarative config for specifying how a machine should be configured (think /etc for windows).  It can install Chocolatey packages and configure the other bits and pieces.

The down side: It's lacking a UI / website, which means the barrier for entry is still a bit high. On the plus side it looks like this will be the de-facto way of configuring windows, with hundreds of DSC modules coming out (wave after wave of them).

There are other alternatives, CA's Nolio and <a href="https://octopusdeploy.com" target="_blank">Octopus Deploy</a> being some that seem to be getting a reasonable amount of purchase (and Puppet can use DSC modules if you're in a hybrid environment). Indeed Octopus Deploy has recently open sourced its configuration modules (which someone will make callable from Puppet &amp; DSC no doubt).

And just recently MicroSoft has announced their first steps of <a href="http://blogs.msdn.com/b/powershell/archive/2015/05/06/powershell-dsc-for-linux-is-now-available.aspx" target="_blank">Linux support for Powershell DSC</a>. Puppet really will have competition!

(Interestingly Windows getting built-in support for SSH will make things like Puppet on Windows easier to set-up - this can only be a good thing!)

<hr />

Why am I not talking about Windows Nano server and Docker in this article? It's because you need to be able to automate building an image before you deploy it across lots of servers.

You wouldn't take a build from a developers machine and put it in production, you'd take it from the CI server. It's the same here - don't put an image you can't recreate into production - it will bite back. (Let's call this the George's Marvelous Medicine principle - reproducibility is key! )

&nbsp;

Once you can do this, it's time to move up the stack and have <a href="https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/manage_powershell" target="_blank">fun with containers</a>. |
| Google Container Engine is The Product Version of Kubernetes and It’s Now Live <a href="http://thenewstack.io/google-container-engine-is-the-product-version-of-kubernetes-and-its-now-live/">http://thenewstack.io/google-container-engine-is-the-product-version-of-kubernetes-and-its-now-live/</a>                                                                                                                                                                                                                                                                                                                                      


                                                                                                                                                                                                                                                                                                         |
| Deployment Management Tools: Chef vs. Puppet vs. Ansible vs. SaltStack vs. Fabric <a href="http://www.javacodegeeks.com/2015/08/deployment-management-tools-chef-vs-puppet-vs-ansible-vs-saltstack-vs-fabric.html">http://www.javacodegeeks.com/2015/08/deployment-management-tools-chef-vs-puppet-vs-ansible-vs-saltstack-vs-fabric.html</a>     





# Docker


                                                               |
| There's something in the air this year, first it was node.js 4 io.js and now Docker have made friends with CoreOS. The announcement of the open container foundation presents a way for everyone to play together and avoid the vendor lock-in that was the instigator of all this in the first place.

Read more about the <a href="http://blog.docker.com/2015/06/open-container-project-foundation/" target="_blank">open container foundation</a>.

<h3>Tell me again why any of this matters?</h3>

Why is it important to me? Far more than just an image format, the speed of it due to caching of the layers and the start up times mean that for once we can do micro end-to-end testing. I've always argued for building a testbase that is grounded in the business problem rather than in implementation details. What we're aiming for is trying to test as much of the hooked up end-to-end system as possible quickly. There are naysayers (google) that say end-to-end testing is broken, and if it's slow and brittle then I'd agree. But by being able to spin up quickly our ecosystem as a set of interacting docker containers I think we may just be able to have our cake and eat it. And by keeping the tests grounded in the business space, a broken test really means something to someone. It's not an arbitrary broken test that may or may not be worth investigating, it's a bonefide business use case that is broken - that's one you can have a discussion about with everyone, not just the developers.

If it's not possible to specify the business functionality that you'd like to see in code, then you've got bigger problems.

In many ways I'm arguing for the <a href="https://en.wikipedia.org/wiki/Behavior-driven_development" target="_blank">BDD</a> given / when / then style (as this avoids the implementation being in the test), but really focusing on the top layer of the onion. By focusing on that layer you're testing a cohesive system which should have few dependencies.

<h3>Getting started</h3>

Find out more at <a href="https://www.docker.com/whatisdocker" target="_blank">Docker</a>.

See also: Convert Any Server to a Docker Container <a href="https://zwischenzugs.wordpress.com/2015/05/24/convert-any-server-to-a-docker-container/">https://zwischenzugs.wordpress.com/2015/05/24/convert-any-server-to-a-docker-container/</a>

<h3>Security</h3>

With Docker, like everything else being more secure requires having less attack surface area. <a href="https://news.ycombinator.com/item?id=10998667">Docker are now moving to a Linux distoro that fits into 5MB</a>. As you can imagine there's a lot less that an attacker can use in an OS image that small! A company called Iron.Io are leading this with <a href="https://github.com/iron-io/dockers">images</a> for most languages.

If that's not enough security / simplicity, then the final leap is to merge kernel mode and user mode - i.e. run the operating system merged with the program. This is called a 'unikernel'. |
| There's something in the air this year, first it was node.js 4 io.js and now Docker have made friends with CoreOS. The announcement of the open container foundation presents a way for everyone to play together and avoid the vendor lock-in that was the instigator of all this in the first place.

Read more about the <a href="http://blog.docker.com/2015/06/open-container-project-foundation/" target="_blank">open container foundation</a>.                                                                                                                                                                                                                   