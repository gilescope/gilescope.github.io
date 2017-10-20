                                                                                                                              |
| Don't get savaged by your choice of logging library.

I feel a little pang of guilt calling out Log4Net specifically as this applies to NLog and all the other .net logging frameworks out there.

But I'm not going to feel too guilty given the vast amount of time and trouble that different Log4net versions have caused me over the years.

<h3>When to use a logging framework</h3>

Log4Net, NLog and other logging frameworks are fair game to use if you are the end user. If you're developing a UI or a website or you're writing a service then knock yourself out.

But even as you do so there's no harm in using framework logging and redirecting that framework logging into your favourite log distribution  / persistence framework.

<h3>When to use framework logging<a href="http://gilescope.ninja/wp-content/uploads/2015/06/UseTRACE.png"><img class="alignright wp-image-339 size-full" src="http://gilescope.ninja/wp-content/uploads/2015/06/UseTRACE.png" alt="Use System Diagnostics Trace  to feed Log4Net" width="160" height="600" /></a></h3>

If you're writing a component that other people will (or might) use then you want to minimise the dependencies you use to avoid version conflicts. For high profile common libraries like logging frameworks you can almost guarantee that with a few different teams using your component several of them will also be using the same one. Pain ensues which can be massaged with assembly binding redirects (or recompiling your logging framework under a different name and having the clients write a log4netTolog4net adaptor - seriously don't do this!).

Instead recall that the whole .net framework logs vast quantities of data to the system diagnostics tracing framework already.

<ul>
    <li>You'll find it's more than fast enough for your usage (you may even encounter new race conditions should you switch to using it as it seems to block less than log4net).</li>
    <li>You'll be shipping one less dll</li>
    <li>No chance of clashing with another logging framework (They all can redirect the native tracing).</li>
</ul>

Nay sayers will say you can't hierarchical listen with tracing, but direct these nay sayers <a href="https://github.com/clariuslabs/NuTracer/wiki/Hierarchical-Tracing" target="_blank">here</a>.

<h3>Recap:</h3>

There's no reason not to use System Diagnostics Tracing - with no drawbacks it should be your go to logger.

(Sorry couldn't resist pointing out that all the logs belong to Splunk (or ELK).) |