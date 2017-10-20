# Clean Code
I've been reading some takes on <a href="http://www.amazon.co.uk/gp/aw/d/B00I0C46BO/ref=tmm_kin_title_0">tidying your house</a>.&nbsp;

The gist is:

<ol>
    <li>Decided if you need it</li>
    <li>Decide where to put it.</li>
</ol>

The twist is that you should only keep things that bring you joy - i.e. Decide what to keep not what to chuck. Everything else can go. I'm wondering how this applies to code bases.&nbsp;

One of the tricks to throwing out sentimental things is to say thank you for the use or insight they have given you before letting them go. This has direct parallels - we should happily delete the proof of concepts that have served their purpose.
<a href="https://blog.8thlight.com/uncle-bob/2014/04/03/Code-Hoarders.html">Uncle Bob</a>&nbsp;touches on this subject, but restates the problem - mess is bad, don't live with mess.
<b>How</b>

We have lived with mess a long time, and tried tidying a room at a time (project by project) but it keeps bouncing back to being messy.&nbsp;

The suggestion is to clean category by category across the whole house. Only by doing this can you truly see the full range of items you have and decide which things you love and which have to go. &nbsp;

To me this is suggesting that you crosscut all your projects and see exactly how many messaging systems / databases / authentication systems etc you have. Then decide which to keep, and then decom the others. By achieving consistency across the board not only will you feng shui be improved, but more likely than not the consistency will be maintained. You also are less likely to fall into the trap of optimising a subset of the full problem.

The other tip was to start with the least controversial categories first. Get better at it before tackling the trickier bits.

# Zombi Code

They call it 'dead code' if it's not used anymore. One would think that it can't 
be harmful if it's not used but far from it. There's been companies that have been put out of business by
accidentally re-referencing dead code. It's rare though.

A far more compelling reason for deleting the stuff is that if you
don't, someone else will maintain it. If they're upgrading X they 
will find every reference to X and make the appropriate conversions
usually without having the time to consider if any parts of the code
base are not used. Don't pay the dead code tax, delete your code and 
stop it coming back to life.

Don't bite off more than you can chew, but good luck!