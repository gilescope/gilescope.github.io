
# Living with NuGet

As NuGet packages are immutable I'm really interested in using a shared package directory for NuGet as suggested here:

http://stackoverflow.com/questions/24617112/storing-nuget-packages-in-alternate-location-on-build-server

As well as time, this would save a ton of diskspace on build agents.

&nbsp;

<h4>Death to Dll Hell</h4>

.Net assembly versioning has always been 'tricky'. The GAC solves this problem but as many find out the GAC is wac. An alternative to mandatory strong naming of the world is to embed the version in the assembly name (which you bump the version number on each breaking change).

At least with Nuget this gets a bit easier when you're then upgrading references to the next version.
P.s. Don't forget klondite&nbsp;

&nbsp;                                                                                                                                                                                                                                                     |
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

If that's not enough security / simplicity, then the final leap is to merge kernel mode and user mode - i.e. run the operating system merged with the program. This is called a 'unikernel'. (Quite a few of the unikernel guys are working for Docker so expect more to come on this front!) |
| runtime.js — JavaScript library OS

&nbsp;

versus Chrome.OS

versus Firefox.OS

or just a cash shell?                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           