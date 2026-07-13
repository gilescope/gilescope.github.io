---
layout: default
title: "Beautiful Tests"
date: 2016-03-02 00:00:00 +0000
---


## Beautiful Tests

I can't dictate what a beautiful test looks like, there are too many of them. But they all have several attributes in common:

<ul>
 <li>They're Quick</li>
 <li>They are repeatable</li>
 <li>They aren't flakey.</li>
 <li>They don't have side effects </li>
 <li>Works on someone else's machine.</li>
</ul>

Now rather than assume people are going to write awesome tests, how about we set ourselves up for success by having an environment where only tests that meet the above criteria ever pass?

<h3>How to</h3>

<ol>
<li>We can run the tests from Jenkins / TeamCity to prove that it<strong> works on someone else's machine</strong>.</li>
<li>To help make the tests quick before running the tests, we can turn off the network:</li>
</ol>

For example on Windows (if your admin) this should do the trick:

<pre><code>wmic path win32_networkadapter where NetConnectionID="Local Area Connection" call disable &lt;&lt; run tests &gt;&gt;
wmic path win32_networkadapter where NetConnectionID="Local Area Connection" call enable</code></pre>

This would ensure that it wasn't using non-local databases or web-services.

<ol>
<li>I'm not sure if we can set NUnit to do this by default, but we can add the attribute [<span class="typ">Maxtime</span><span class="pun">(1</span><span class="lit">000</span><span class="pun">)] to the test to cancel it and mark as a failure if it takes too long. (It would be good to be able to automatically categorise slow running tests! - google do this, so should we! A slow test should be sent to 'test purgatory'.)</span></li>
</ol>

<h3>Oh, the fun we could have!</h3>

With NUnit 3 there's the ability to run tests in parallel. It's well overdue functionality. But I want to take a different direction.

Just how much can we squeeze out of one test?

<ul>
 <li>We can run it multiple times to detect memory leaks.</li>
 <li>We can run multiple times to check caching works.</li>
 <li>We can run the same test concurrently to detect race conditions.</li>
</ul>

(I feel at the moment we still live in a land where tests are imperative - gurkin needed.)
