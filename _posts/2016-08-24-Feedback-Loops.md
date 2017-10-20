# Feedback Loops aka Cycle Time                                                                                                      |
| The key to Programming like running any business is about one thing only.

<!--more-->Feedback loops.

With good feedback even if you start in completely the wrong direction you will be able to correct your course early on. With good feedback loops you can take risks, and risks allow you to have simpler designs and happier customers.

Without good feedback you have fear. Fear of breaking what you already have, fear of building the wrong thing (create a massive specification document that is signed off and locked down to mitigate this ;-)).

<blockquote>
<p style="text-align: right;">I must not fear. Fear is the mind-killer. Fear is the little-death that brings total obliteration. I will face my fear. I will permit it to pass over me and through me. And when it has gone past I will turn the inner eye to see its path. Where the fear has gone there will be nothing. Only I will remain.
Frank herbert</p>
</blockquote>

How tight can you make yours?

<a href="http://www.ncrunch.net" target="_blank">NCrunch</a> and <a href="http://karma-runner.github.io/0.12/index.html" target="_blank">Karma</a> can make the TDD cycle pretty tight - the tests are running while you're still typing! (Check out <a href="https://blog.jetbrains.com/dotnet/2015/11/19/continuous-testing-in-dotcover-and-resharper-ultimate/" target="_blank">JetBrain's take</a> on it)

CI allows lots of integration tests to run. ( CD gets the results in front of a real user (human or otherwise).

Keep things simple - keep branching to a minimum so the above is easier (1 branch is best) - branch by abstraction instead.

Maybe we should be taking a step back and monitoring our development feedback curve,

<h2>Dev feedback loops</h2>

<ol>
    <li>How long to incremental compile? (compile a second time when you didn't change anything )</li>
    <li>How long to run the quick tests?</li>
    <li>How long for the CI built to go green?</li>
    <li>How long to deploy a system to an environment ?</li>
    <li>How long to determine whether a deployed system works? potentially <a href="http://spectrum.ieee.org/view-from-the-valley/computing/software/yahoos-engineers-move-to-coding-without-a-net" target="_blank">Drop independent QA</a> like Yahoo! have.</li>
    <li>How long to ship it?</li>
</ol>

Where does Pair Programming fit in? - for me it's at 0 as you're constantly improving, not being lazy, staying focused and coming up with hybrid ideas that neither of you would have had on your own.

<h2>Production feedback loops</h2>

It doesn't stop there, feedback from the live system is also critical - whether you are using <a href="http://Splunk.com" target="_blank">Splunk</a> or <a href="http://aarvik.dk/a-bit-on-elasticsearch-logstash-kibana-the-elk-stack/" target="_blank">ELK</a>, to collect that data allows you to see how a new system reacts compared with the previous version.

<ol>
    <li>Health checks - are the power on self tests and heartbeats working?</li>
    <li>Memory,  disk access,  processor, exceptions, disk usage - does the uat version have a better profile than the current prod? How does one hour / day / week differ from another?</li>
    <li>Performance bottlenecks - where's the current kink in the system?</li>
    <li>Capacity and trending - do you need more hardware / disk space?</li>
</ol>

<h2>UX</h2>

Having a good user experience when using a website / app is all about getting good timely feedback - the difference between half a second and a full second can make all the difference in terms of having a flowing experience.

<h2>Personal feedback loops</h2>

I'm not sure all of these quite classify as feedback loops (except perhaps to make the processes more streamlined for the next guy that joins)

<ol>
    <li>How fast can a new person get permission and installs to work on the project?</li>
    <li>How quickly can new joiners become productive?</li>
    <li>How often do you have a retrospective?</li>
    <li>Statutory Performance appraisals (too long a loop!)</li>
</ol> |



# Zoning -  Minimise Distractions

                                                    |
| Minimise Distractions
Pair
KanBan
Listen to music - Don't listen to other peoples phone conferences!
Stay in the zone - if things are going well, keep the ball rolling as long as possible!

When not to be focused?

If you are stuck, let your unconscious mind work on the problem while you do something completely different (whether that's helping a colleague or having a gym session).

Solving problems the hard way
You're going to get stuck on a gottcha, and you can keep banging your head on the brick wall until it gives way and you figure out what the slight tweak was that makes it all work. This can easily take days if you're not careful!

Solving problems the smart way
Rather than let the gotch turn into a GumptionTrap, 
 - there's almost always a way around your problem if you back up a bit, in fact there's usually a large set of alternatives you could try (some of these will be better than what you were proposing to do anyway). By backing up and solving the problem a (potentially sub-optimal) way it keeps your momentum going.

The great news is that quite often (days / weeks / months) later you'll stumble on what you were doing wrong originally and (if that way was better than the workaround) you'll be able to switch back to it. Asynchronous gotcha optimisation?

Either way, cache your experience - leave a trail for you or others to follow so if they do walk into the same problem later on (whether as a comment or a stack overflow answer) they'll fix it sooner... 