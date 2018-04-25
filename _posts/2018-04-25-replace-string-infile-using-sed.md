---
ID: 198
post_title: Replace string infile using sed
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=198
published: true
post_date: 2018-04-25 14:48:17
---
<div>Example: Change tag x86_64-1.0.1-javacc for x86_64-1.1.0 into json dockerfiles</div>
<div></div>
<pre class="161206">sed -i -e 's/x86_64-1.0.1-javacc/x86_64-1.1.0/g'  *.json</pre>