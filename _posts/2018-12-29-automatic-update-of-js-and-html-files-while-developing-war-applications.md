---
ID: 277
post_title: >
  Automatic update of js and html files
  while developing war applications
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.tech/?p=277
published: true
post_date: 2018-12-29 07:01:15
---
To automatic update client contents of a war app without to redeploy, it is just needed to copy changed files into the correct exploded war location.

To automaticallay perform the copy just use:
<pre>onchange 'path/to/watched/src/' -- cp -Rf path/to/watched/src/ /path/to/exploded/war/files
</pre>
you can install onchange with npm:
<pre>npm -g install onchange</pre>