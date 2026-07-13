---
layout: default
title: "Living with NuGet"
date: 2016-09-25 00:00:00 +0000
---



## Living with NuGet

As NuGet packages are immutable I'm really interested in using a shared package directory for NuGet as suggested here:

http://stackoverflow.com/questions/24617112/storing-nuget-packages-in-alternate-location-on-build-server

As well as time, this would save a ton of diskspace on build agents.

<h4>Death to Dll Hell</h4>

.Net assembly versioning has always been 'tricky'. The GAC solves this problem but as many find out the GAC is wac. An alternative to mandatory strong naming of the world is to embed the version in the assembly name (which you bump the version number on each breaking change).

At least with Nuget this gets a bit easier when you're then upgrading references to the next version.
P.s. Don't forget klondite
