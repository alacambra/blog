---
ID: 206
post_title: AWK useful commands
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=206
published: true
post_date: 2018-05-27 16:27:39
---
<ol>
 	<li>print column <em>n</em>: <strong>awk ‘{print $<em>n</em>}’</strong></li>
 	<li>print column 3 of lines that start with a number.: <strong>awk '/^[0-9]/ {print $3}'</strong></li>
 	<li>Variables:
<ul>
 	<li>NF: number of fields</li>
 	<li>NR: Number of record being processed
<ul>
 	<li>Avoid first record(row) and print last field (columnd): <strong>awk ‘{if(NR&gt;1) print $NF}’: </strong></li>
</ul>
</li>
</ul>
</li>
</ol>