# Beautiful Tests

| I can't dictate what&nbsp;a beautiful test looks like, there are too many of them. But they all have several attributes in common:

<ul>
    <li>They're Quick</li>
    <li>They are repeatable</li>
    <li>They aren't flakey.</li>
    <li>They don't have side effects&nbsp;</li>
    <li>Works on someone else's machine.</li>
</ul>

Now rather than assume people are going to write awesome tests, how about we set ourselves up for success by having an environment where only tests that meet the above criteria ever pass?

<h3>How to</h3>

<ol>
<li>We can run the tests from Jenkins / TeamCity to prove that it<strong> works on someone else's machine</strong>.</p></li>
<li><p>To help make the tests quick before running the tests, we can turn off the network:</p></li>
</ol>

<p>For example on Windows (if your admin) this should do the trick:

<code>wmic path win32_networkadapter where NetConnectionID="Local Area Connection" call disable &lt;&lt; run tests &gt;&gt;
wmic path win32_networkadapter where NetConnectionID="Local Area Connection" call enable</code>

This would ensure that it wasn't using non-local databases or web-services.

<ol>
<li>I'm not sure if we can set NUnit to do this by default, but we can add the attribute [<span class="typ">Maxtime</span><span class="pun">(1</span><span class="lit">000</span><span class="pun">)] to the test to cancel it and mark as a failure if it takes too long. (It would be good to be able to automatically categorise slow running tests! - google do this, so should we! A slow test should be sent to 'test purgatory'.)</span></li>
</ol>

<h3>Oh, the fun we could have!</h3>

With NUnit 3 there's the ability to run tests in parallel. It's well overdue functionality. But I want to take a different direction.

&nbsp;

Just how much can we squeeze out of one test?

<ul>
    <li>We can run it multiple times to detect memory leaks.</li>
    <li>We can run multiple times to check caching works.</li>
    <li>We can run the same test concurrently to detect race conditions.</li>
</ul>

(I feel at the moment we still live in a land where tests are imperative - gurkin needed.) |
| Almost all project management focuses on one project rather than the n competing projects. I understand at this larger level it's called 'program management'.
&nbsp;http://www.artofmanliness.com/2013/12/03/beyond-sissy-resilience-on-becoming-antifragile/                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |



# Tests are the Requirements

                       
| Requirements = Spec = Test.

I've talked before about specifying tests in gherkin and they provide a great way to communicate with stakeholders, but..

<!--more-->

We always want the maximum bang for buck, and while specific examples that can be talked through are great for conversations and getting the spec right, if you can specify properties that should hold true across a range of examples then we can use brute force of computers to check that they generally hold true.

<h2>Quick Check</h2>

Like JUnit, Haskell's QuickCheck library has been ported to pretty much every language now (<a href="https://en.wikipedia.org/wiki/QuickCheck" target="_blank">QuickCheck ports</a> inc, <a href="https://github.com/fsharp/FsCheck" target="_blank">FsCheck</a> and <a href="https://www.scalacheck.org/" target="_blank">ScalaCheck</a>).

That's a good enough reason for anyone to invest some time in trying to find out how it works for you.

<h2>Formal Proofs</h2>

QuickCheck and derivatives are not proof that your code works, but it's a step up from always running the same tests through the same path. The problem with provably correct programs has always been that while you might be able to prove the program meets the specification, there's nothing to stop there being bugs in the spec. |




# Code coverage



</ol> |
| Before you can measure something, you first have to define it. I don't think we can quantify quality, but the best definition of quality I've ever read is the book <a href="http://www.amazon.co.uk/Zen-And-The-Motorcycle-Maintenance/dp/0099322617" target="_blank">Zen and the art of motorcycle maintenance</a> (a must read for anyone).

<h2>Code Coverage</h2>

If we can't measure quality, what can we measure? We can measure code coverage and while every measure can be gamed (for code coverage just exclude most of the code), I think there's a lot of value in seeing that number go up.

How much code coverage is enough? If you're so confident in your coverage that you don't even need to measure it then that's a great place to be.

If you do feel the need to measure it - that's ok too. I like code coverage as a metric simply because it directly rewards people for deleting code. In a corporate environment there's lots of pressures for creating more code but far fewer pressures to get rid of code. It's seen as a 'nice to have' rather than essential to running a clean ship and reducing operational risk.

Tools to use:

<ul>
    <li>JS: <a href="https://github.com/gotwarlost/istanbul" target="_blank">Istanbul</a></li>
    <li>.Net:<a href="https://github.com/OpenCover/opencover" target="_blank"> OpenCover</a></li>
    <li>Java: <a href="https://github.com/gotwarlost/istanbul" target="_blank">JCov</a></li>
</ul>

<h3>Which coverage metric to choose?</h3>

If you're going to pick one coverage metric, then 'branch coverage' rather than file or statement coverage is best. This way less branches = better coverage - i.e. not only do you get rewarded for removing dead code, but you get rewarded for always doing something rather than optionally doing something. This brings down code complexity, makes it easier to test and makes the code easier to reason with.

To report cross-platform <a href="http://www.sonarqube.org/" target="_blank">SonarQube</a> will do the trick.

<h2>Legacy Coverage</h2>

If you're starting from a legacy codebase with a dilapidated or non-existent testbase, there's little point in writing scattergun unit tests and hoping for the best. When you're renovating an area it makes sense to put tests around it (ideally before hand so you can TDD it - I know there's a lot of dependencies everywhere because it wasn't written with testing in mind (doing the right thing is rarely the easy route)).

Using an issue tracking system such as JIRA you can associate your repository changes with an issue. It would be very interesting to see the coverage percentage for the code changes associated with specific issues. This might be a fair way to set a quality gate (but positive encouragement is always more motivating than negative) - you can fail a TeamCity build if code coverage drops by more than a certain percentage but with multiple commits it's not clear who's code didn't have enough tests around them.

<h2>Targeted Coverage</h2>

Let's assume the current program 'works' (a stretch for some programs for sure, but bear with me). There's little point in writing a unit test for a class that was written five years ago and hasn't changed since (unless your NASA in which case you really <em>should</em> have been doing TDD in the first place). Ideally you should be adding tests around the areas of your codebase that have the highest rate of change (as this is where you will most likely introduce a regression).

<h5>How to:</h5>

If you're after targeting your unit tests to get the most bang for buck it's quite simple to correlate the svn logs of how often (and recently) a file was changed with how much coverage that file has.

(Incidentally the main method of the program usually ranks as one of those high changing classes with low coverage. - I'll leave you to figure out how to unit test that one).

&nbsp; |
| How much code coverage is enough? If you're so confident in your coverage that you don't even need to measure it then that's a great place to be.

If you do feel the need to measure it - that's ok too. I like code coverage as a metric simply because it directly rewards people for deleting code. In a corporate environment there's lots of pressures for creating more code but far fewer pressures to get rid of code. It's seen as a 'nice to have' rather than essential to running a clean ship and reducing operational risk.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| How much code coverage is enough? If you're so confident in your coverage that you don't even need to measure it then that's a great place to be.

If you do feel the need to measure it - that's ok too. I like code coverage as a metric simply because it directly rewards people for deleting code. In a corporate environment there's lots of pressures for creating more code but far fewer pressures to get rid of code. It's seen as a 'nice to have' rather than essential to running a clean ship and reducing operational risk.

Tools to use:

<ul>
    <li>JS: <a href="https://github.com/gotwarlost/istanbul" target="_blank">Istanbul</a></li>
    <li>.Net:<a href="https://github.com/OpenCover/opencover" target="_blank"> OpenCover</a></li>
    <li>Java: <a href="https://github.com/gotwarlost/istanbul" target="_blank">JCov</a></li>
</ul>

And then to report cross-platform <a href="http://www.sonarqube.org/" target="_blank">SonarQube</a> will do the trick.                                                                      |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                  