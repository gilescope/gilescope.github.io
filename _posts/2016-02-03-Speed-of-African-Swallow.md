---
layout: default
title: "Speed of African Swallow"
date: 2016-02-03 00:00:00 +0000
---


We've moved on from Prestel (<a href="https://tools.ietf.org/html/rfc1149">RFC1149</a>) to <a href="http://tools.ietf.org/html/rfc1945">HTTP/1.0</a>, <a href="https://www.ietf.org/rfc/rfc2616.txt">HTTP/1.1</a> and finally moved to <a href="https://tools.ietf.org/html/rfc7540">HTTP/2</a>.

This is the biggest step-change since moving off RFC1149. In a nutshell,

<ul>
 <li>It's secure by default. (SSL only, so no snoopers charter)</li>
 <li>It's faster (binary, pre-push, multiplexed)</li>
</ul>

We all know before we should start using something we should wait till version 3. - I think we'll make an exception in this case!

<hr />

Now we just need to wait till everyone's favorite webserver (<a href="http://nginx.com/blog/how-nginx-plans-to-support-http2/" target="_blank">Nginx</a>) supports HTTP2 (currently it supports HTTP2's prototype: SPDY 3.1).

It will also be interesting to see how Google's <a href="https://developers.google.com/speed/pagespeed/module" target="_blank">PageSpeed Module</a> adapts to HTTP2 as quite a few of the inlining optimisations are no longer required.

<hr />

<h3>Post-HTTP</h3>

Given HTTP has been around for 20+ years now, it's done very well to bootstrap the world into using common agreed interchange formats (mainly by keeping things very simple).

In the next 20 years we're likely to see the rise of the decentralised internet, one depending much more heavily on peer-to-peer for caching at the edge. One such effort is <a href="http://ipfs.io/" target="_blank">IPFS</a> which is taking the GIT-like content addressable direction (I.e. a file's key is its hash).
