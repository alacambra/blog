---
ID: 141
post_title: Remove local merged branches
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=141
published: true
post_date: 2017-12-07 09:01:43
---
To remove merged local branches:
<pre>bash: git branch -d $(git branch --merged)
windows cmdr: git branch --merged | grep -v '^* master$' | grep -v '^  master$' | xargs git branch -d</pre>
and in case you want to remove inexistent trackings too:
<pre>git pull --prune
</pre>