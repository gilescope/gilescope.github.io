It's been here for some time, but after a few false starts 
(the not-so-simple SOAP protocol and WS-BS*) 
it seems the world has finally agreed on Json/REST as the 
de-facto protocol or lingua franca of the web.

<h2>Discovery</h2>

How do we discover it? Discover has always been an after-thought with REST, but these days most rest frameworks come with built in discovery (at least for human).

But as devs, we always like consistency, - that's where things like <a title="REST API Documentation" href="http://swagger.io/" target="_blank">Swagger</a> come in - read <a title="Swagger Spec" href="https://github.com/swagger-api/swagger-spec/blob/master/versions/2.0.md" target="_blank">spec 2.0 here</a>.

<h2>Strong-ish Typing</h2>

Swagger stands on the shoulders of the <a title="Json Schema" href="http://json-schema.org/latest/json-schema-core.html" target="_blank">Json Schema</a> project. With the types announced it's a stones throw to auto-generate bindings for all the strongly typed languages out there.

<h2>Testing</h2>

Having all these services out there that we rely on is great, but we need to be able to stub them out with fakes. This is where open source projects like <a title="Mock Rest APIs" href="http://mockbin.org/" target="_blank">mockbin</a> come in. By being able to record and then replay you can isolate yourself from your other (micro)services.

<h2>Versioning</h2>

Swagger supports marking bits of your API as deprecated which gives your users a warning they should be upgrading.

<h2>Final thoughts...</h2>

Simple is good, it keeps everything very mashable. If the de-facto services interface is Json/REST, doesn't that make <a title="Why Enterprise JavaScript is inevitable…" href="http://gilescope.ninja/ejs/">Enterprise JavaScript inevitable</a>?

<hr>

Examples of 'Universal JavaScript' (yes now JavaScript on the server has a cool name - well better than 'Isomorphic JavaScript') :

<a href="http://techblog.netflix.com/2015/08/making-netflixcom-faster.html">NetFlix</a> |