# Cache by Hash

| Cache by hash has been on my mind for a while, but I saw <a href="http://security.stackexchange.com/questions/29696/content-hashes-to-help-protect-resources-being-fetched-from-a-cdn" target="_blank">this</a> and it makes me convinced that the web is going to head in this direction for scaling. Maybe we won't get quite as far as <a href="http://ipfs.io/" target="_blank">IPFS</a> hopes, but I'm sure we're heading in that direction.

&nbsp;

There's a great free e-book on how git works (<a title="Pro Git" href="http://git-scm.com/book/en/v2">Pro-Git</a>). For me the biggest take-away was the beauty of storing data by it's hashcode (SHA256 in git's case).

If you can exclude mutable things like the filename and timestamps, then when you have multiple copies of the same file (or chunk of data) you'll naturally save them under the same location. You could call this 'hash based compression' as the same chunk of data is never stored twice.

You'd need to reference count the pointers to this chunk of data (file) if you wanted to delete it (unless you're using a time based clean up).

<h3>Ok, so no dupe, but what about load balancing?</h3>

It turns out that the <a title="Chord" href="https://en.wikipedia.org/wiki/Chord_(peer-to-peer)">chord algorithm</a> is perfect for this (or pick any other <a title="Distributed Hash Table" href="https://en.wikipedia.org/wiki/Distributed_hash_table" target="_blank">DHT algo</a>). You can split up where you store the data and can store it n-times for redundancy.

<h3>Key Gotcha</h3>

There's still the question of how to get the hash if you don't have the original. The hash makes a perfect immutable key for the data, but you still need to map from your mutable key (filename/timestamp) to the immutable key.

The good news is you have split the problem into two distinct problems:

<ol>
    <li>Mapping from a small mutable key to a small immutable hash.</li>
    <li>Distribution of the (heavy) data.</li>
</ol>

Once you've keyed by hash you can't get the wrong / out of date contents. It is at this stage very error-proof. (And you can always verify that the data you have does indeed match the hash).

<h3>Versioning</h3>

So far, so good, but how do you have a version 1, version 2 etc of an object? If we're storing the object under its hashed address we can hash the hash (or just add one to the hash) and store the pointer there to the next hash. (For a more in-depth discussion on this topic see <a href="http://joearms.github.io/2015/06/19/Mutable-Value_Chains.html" target="_blank">Mutable Value Chains</a>)

&nbsp;

<h3>Additional references:</h3>

<a title="Single instance storage" href="https://en.wikipedia.org/wiki/Single-instance_storage">Single Instance Storage</a>

<a href="http://www.w3.org/TR/SRI/" target="_blank">W3C's SRI working draft</a> (Supported by Chrome and FireFox)

<a href="http://blog.jsdelivr.com/" target="_blank">SRI CDN jsdelivr</a>

<hr />

&nbsp;

UPDATE

I see Docker has finally moved to using cache via hash for their layers and images ("<a href="https://blog.docker.com/2016/02/docker-1-10/" target="_blank">content addressable image ids</a>" they call them.). |
| Cache by hash has been on my mind for a while, but I saw <a href="http://security.stackexchange.com/questions/29696/content-hashes-to-help-protect-resources-being-fetched-from-a-cdn" target="_blank">this</a> and it makes me convinced that the web is going to head in this direction for scaling. Maybe we won't get quite as far as <a href="http://ipfs.io/" target="_blank">IPFS</a> hopes, but I'm sure we're heading in that direction.

&nbsp;

<hr /