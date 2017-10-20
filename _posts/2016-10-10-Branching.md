                                                                       |
| To branch or not to branch - it's not even a question.

Not branching prevents you taking risks, but branching isn't free so there's a tradeoff.


<table>
<tbody>
<tr>
<td>Strategy</td>
<td>What is it?</td>
<td>Advantages</td>
<td>Disadvantages</td>
</tr>
<tr>
<td>Branch by abstraction

(aka feature flags)</td>
<td>Have configuration turning your branch on and off dynamically at runtime.</td>
<td>
<ul>
    <li>No merging</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td>Feature Branches</td>
<td> A branch for a specific story/feature, reintegrated into trunk when it's 'done'.</td>
<td>
<ul>
    <li>Team is isolated from the firehose.</li>
</ul>
</td>
<td>
<ul>
    <li>More costly than branching by abstraction due to merge overhead.</li>
</ul>
</td>
</tr>
<tr>
<td>Merge Only Release Branch</td>
<td>No checkins to release branches are allowed. Everything change on a release branch must be merged in.</td>
<td>
<ul>
    <li></li>
    <li>No way to regress changes as everything is applied to the trunk branch before it gets into prod,</li>
</ul>
</td>
<td></td>
</tr>
</tbody>
</table>

&nbsp;

http://nvie.com/posts/a-successful-git-branching-model/ |