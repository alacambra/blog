---
ID: 131
post_title: Refresh command using watch
author: alacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=131
published: true
post_date: 2017-11-07 09:27:29
---
To rerun automatically a comand use:
<pre>watch -n 1 --differences {COMMAND TO REFRESH}
</pre>
For example, to see creation of docker containers:
<pre>watch -n 1 --differences docker ps</pre>