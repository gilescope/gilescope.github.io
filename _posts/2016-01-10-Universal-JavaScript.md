# Universal JavaScript

People laughed when I told them that the future of the enterprise is JavaScript. I told them it's inevitable...and with ES6 ratified we're one step closer.


<h3>Performance?</h3>

They perceive JavaScript circa 1990s performance, with rough edges and a text editor as an IDE. It's a world away from the truth now, with the raw speed of <a title="asm.js - high performance javascript" href="http://asmjs.org/" target="_blank">asm.js</a> at the cutting edge, and standard JavaScript performance is 'good enough' (almost every Java hotspot technique has been ported across to the JavaScript VMs). In 90% of business cases it's not performance that's stopping JavaScript.

<blockquote>JavaScript is a platform, not just a language.</blockquote>

And it's only going to get better. Speed up Java or .Net and it helps a bit, but speed up JavaScript and you've just added a fraction onto the world's GDP. There's far more money backing speeding up JavaScript than anything else. (Remember JavaScript is a platform, not just a language.)

<blockquote>Check out the new <a href="https://brendaneich.com/2015/06/from-asm-js-to-webassembly/" target="_blank">WebAssemby movement</a> (backed by all the right people) we might have a way to gradually migrate towards Javascript as a Platform.</blockquote>

<a href="https://hacks.mozilla.org/2015/12/compiling-to-webassembly-its-happening/">Latest news on WebAssembly front</a> - they're getting there.

<h3>JS @ Front</h3>

The days of fat clients and WinForms/WPF are largely over. There's little justification for not going HTML5 in a business setting. The UI I think we're all agreed is going to be HTML and JavaScript for the foreseeable future.

<h3>JS @ Back</h3>

While Java and .NET back ends (and even some C++) will be around indefinitely, they are going to have to roll over and let JavaScript take its fare share of the bed. It started with Node.JS getting the ball rolling, but I'm sure there will be many other server side JavaScript platforms (it's great to see <a href="https://iojs.org/en/index.html" target="_blank">io.js</a> is going to merge back with node.js soon). We hope they will learn from the lessons and pain Java went through with J2EE.

<h3>Tooling</h3>

The days of textpad are numbered. JavaScript has almost as good IDEs as the static languages have thanks to Chrome's developer tools and JetBrain's excellent WebStorm. Add in a little <a title="Karma test runner" href="http://karma-runner.github.io/0.8/config/coverage.html" target="_blank">Karma</a> and you've got a TDD platform that's arguably better than today's C# can manage.

But there's more - Chrome's next step in DevTools development is to allow you to use the Chrome devtools to debug <em>both</em> the client and the server from the comfort of your browser. This should lead to a very compelling and tight development loop. Read more about the <a href="https://developers.google.com/web/updates/2016/06/devtools-digest">Chrome Dev tools plans</a>.

And it's only going to get better.

<h3>The Future</h3>

JavaScript's not a static language, it's dynamic and evolving at a good pace. One thing that's clear to me is that the future is <a title="Strong typing in a dynamic world" href="http://definitelytyped.org/" target="_blank">definitely typed</a> - with ES6 approved, the next big leap for the language in ES7 is giving people the option to type. FaceBook, Google and Microsoft are all rallying around definitely typed as a standard, and with those backers I wouldn't want to bet against it.

<ul>
    <li>A look into <a href="https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2/" target="_blank">ES6 string templating</a></li>
    <li>For now you'll still have to <a href="https://babeljs.io/" target="_blank">transpile</a> to ES5 until there's <a href="https://kangax.github.io/compat-table/es6/" target="_blank">browser support</a>.</li>
</ul>

<h3>Round up</h3>

All this JavaScript on the server - is it such a bad thing? Having one language on the client and server is an advantage. But it doesn't stop there, JavaScript's async nature means that it's tilted in the direction of large parallel processing, and at its heart it's a functional language (though a far cry from Haskall) with not too many bells and whistles.

Whether you think it's a great or a terrible idea, as sure as eggs is eggs we're going to see a whole lot of JavaScript on the server. So while some of you might not like the idea, it's time to get used to it.

I for one welcome our new overlord. Given EJS is inevitable, are you ready?

<hr />

UPDATE: here's a great writeup on the current <a href="http://engineering.widen.com/blog/future-of-the-web-react-falcor/">best of breed enterprise JavaScript stack</a>. - React, node and some cute transport between them. - A great starting place.

<hr />

&nbsp;

UPDATE: A wonderful talk on Redux demonstrates the power of immutable state - it's so nice to see how simple powerful things can be when you get it right, and React and Redux have definitely got it spot on - really recommend watching this - it's worth every min:

https://www.youtube.com/watch?v=xsSnOQynTHs

(If you can't watch the video, this <a href="https://code-cartoons.com/a-cartoon-intro-to-redux-3afb775501a6">cartoon</a> will have to do.)

<hr />

Check out <a href="https://github.com/dthree/cash">CASH</a> - a JavaScript shell for windows to give you cyg-win like powers...this is the beginning of something big.

<hr />

Testing rocks as well in JavaScript - combining <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign">Object.assign</a> and

<pre><a href="https://github.com/michelsalib/chai-shallow-deep-equal">chai-shallow-deep-equal</a> allows you to assert many properties of an object at once in an elegant manner by just specifying the JSON you'd expect to be there. (How I wish we had this in c#!)</pre>