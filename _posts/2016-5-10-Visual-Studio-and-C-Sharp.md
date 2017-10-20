# Visual Studio & C#

Recently I've found myself relying more and more on Visual Studio extensions. Here are my personal favorites:

<h3>Target FrameWork Migrator</h3>

https://visualstudiogallery.msdn.microsoft.com/47bded90-80d8-42af-bc35-4736fdd8cd13

How many times have you thought you've switched them all to the next version only to find a couple of stragglers? Not any more.

<h3>VSColorOutput</h3>

I find the Output window the best way to see what the first error was. This makes errors red, warnings yellow etc. Invaluable speedup!

<h3>Projects Output Path</h3>

https://visualstudiogallery.msdn.microsoft.com/77161518-ba4d-48d4-bb04-37fbe3f93dd3

If you want SPEED (and who doesn't?), setting common bin and obj dirs helps a lot with large projects. This gets you there faster.

<h3>Productivity power tools for Visual Studio</h3>

Why? Well the errors shown in the solution explorer are helpful but right now copy and paste of a reference is extremely useful.

<h3></h3>

<h3>VsFunnel</h3>

When you open up a solution you can select just the project(s) you care about and it will open up this and just the dependent projects making everything quick. Obviously not ideal for 'find references' situations, but if you're going to be working on a specific subsystem this is possibly a better alternative to having multiple overlapping solutions files.

http://vsfunnel.com/ |
| Machine (installs, registry)




# C Sharp's Journey / for considered harmful?
It's been a long journey that started with people coming from VB and Java, but looking at modern day C#, it's a different beast...

<!--more-->

F# is a fine language but hasn't taken off (and not just because of the lack of ReSharper support - if you want to help, <a href="https://github.com/jetbrains/fsharper" target="_blank">code here</a>) - it's unashamedly pragmatic as functional languages go (much I suspect to the jibing of Haskell evangelists), but even with a healthy dollop of pragmatism the gap for the majority of developers between C# and F# has been too wide to cross.

I think the C# language designers knew this, and have taken us on a journey gradually gentrifying the functional landscape bringing in Lambdas and  Linq, allowing us (should we choose to) to work on a collection as a whole, rather than iterating through the component parts (should 'for' be considered harmful?).

As an experiment, I think it's worked, in that many more developers are now confident in using and thinking in these higher level constructs. It's lead us down a path to making functional programming more socially acceptable.

The journey is still continuing, and hopefully we will see a tilt towards immutability being the norm (or at least supported at a language level) in C# 7.

Read the infoq article on some of the C# proposals in this area:

<a href="http://www.infoq.com/news/2015/05/CSharp-7-readonly">http://www.infoq.com/news/2015/05/CSharp-7-readonly</a>

Is the world ready yet for F#? It's certainly more receptive - the gap is smaller now than it has ever been... |
| <a href="http://www.infoq.com/news/2015/05/CSharp-7-readonly">http://www.infoq.com/news/2015/05/CSharp-7-readonly</a>

C                                                                                                                                                                                                                                                                                                                                                                                                                                                                         