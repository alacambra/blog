---
ID: 125
post_title: >
  Run docker commands on all or some
  containers
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=125
published: true
post_date: 2017-11-07 09:15:09
---
<ul>
 	<li class="161022">Use the ps command with the q param to fetch the insance id and then apply the command:
<ul>
 	<li class="161022"><strong>docker {COMMAND TO RUN} $(docker ps -a -q)  -&gt; for containers</strong></li>
 	<li><strong>docker {COMMAND TO RUN} $(docker images -q) -&gt; for images</strong></li>
</ul>
</li>
 	<li>Examples:
<ul>
 	<li>Delete all stopped containers: docker rm $(docker ps -a -q)</li>
 	<li>Delete all unused images: docker rmi $(docker images -q)</li>
 	<li>Start all stopped containers: docker start $(docker ps -a -q)</li>
 	<li>Restart all containers: docker restart $(docker ps -a -q)</li>
</ul>
</li>
</ul>
<ul>
 	<li class="161022">For more elavorated filters:
<ul>
 	<li class="161022">docker  {COMMAND TO RUN} $(docker ps -a |grep {TEXT-TO-CAPTURE}|awk '{ print $1 }')  where awk '{ print $1 }' captures the container id value.</li>
 	<li class="161022">Remove all images with  "pattern" in name: docker rmi $(docker images -f="reference=*pattern*" -q)</li>
</ul>
</li>
</ul>