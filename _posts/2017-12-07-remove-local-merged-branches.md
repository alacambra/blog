---
ID: 141
post_title: Remove local merged branches
author: alacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=141
published: true
post_date: 2017-12-07 09:01:43
---
To remove merged local branches:
<pre>git branch -d $(git branch --merged)</pre>
and in case you want to remove inexistent trackings too:
<pre>git pull --prune
</pre>