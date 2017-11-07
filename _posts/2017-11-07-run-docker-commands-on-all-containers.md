---
ID: 125
post_title: Run docker commands on all containers
author: alacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=125
published: true
post_date: 2017-11-07 09:15:09
---
<div class="161022">Use the ps command with the q param to fetch the insance id and then apply the command:</div>
<div class="161022"></div>
<div class="161022">docker {COMMAND TO RUN} $(docker ps -a -q)</div>
<div class="161022"></div>
<div class="161022">For more elavorated filters:</div>
<div class="161022">
<div class="161022">docker  {COMMAND TO RUN} $(docker ps -a |grep {TEXT-TO-CAPTURE}|awk '{ print $1 }')</div>
</div>
<div class="161022">wehre awk '{ print $1 }' captures the container id value.</div>