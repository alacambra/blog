---
ID: 112
post_title: Read docker logs
author: alacambra
post_date: 2017-10-26 10:59:46
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=112
published: true
---
<ul>
 	<li>Take the path to the logs file:
<ul>
 	<li> docker inspect --format='{{.LogPath}}' <b> </b><b><i>containerName</i></b></li>
</ul>
</li>
 	<li>To use less:
<ul>
 	<li>sudo less <b>$(</b>docker inspect --format='{{.LogPath}}'   <i>containerName</i><b>)</b></li>
 	<li>docker logs <i>containerName</i> 2&gt;&amp;1 |less –R <em>(Where –R is to interpret colors)</em></li>
</ul>
</li>
</ul>