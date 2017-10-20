                                                                                                      |
| <strong>Markdown</strong>

Rust uses Markdown for it's documentation. Github goes further by allowing references to pull requests, mentions and issues.

&nbsp;

<strong>Software Archeology Rule 1: KISS</strong>

Ivan Moor's post on <a href="http://puttingtheteaintoteam.blogspot.co.uk/2014/02/making-life-easier-for-future-software.html">software archeology</a> has kept me thinking. Essentially they're suggesting a long lived project needs to contain in its source control system:

<ul>
    <li>Code</li>
    <li>Config</li>
    <li>Wiki</li>
    <li>Issues</li>
    <li>Dependencies.</li>
</ul>

With all of these key things in the same place, nothing will get lost. If they're separate and upgraded / changed every 3-4 years to the next newfangled thing, then things get lost.

<strong>Playtime</strong>

<a href="http://getgrav.org/">Grav</a> is a markdown flat file CMS that could happily live in your source repository.

Next you need to ditch JIRA and represent your tasklist in markdown:

<ul>
    <li>[ ] Todo Task1</li>
    <li>[x] Done Task 2</li>
</ul>

If you need to get fancier than that, you can have one page per issue, with your choice of metadata at the head of the page (in markdown 'definition' format).
