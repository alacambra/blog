---
ID: 27
post_title: Run nano on docker ubuntu image
author: alacambra
post_date: 2016-09-18 14:16:25
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2016/09/18/run-nano-on-docker-ubuntu-image/
published: true
---
I have tried to run nano on an ubuntu docker image and after installing it I always have this error:
<code>Error opening terminal: unknown.</code>

The solution is so easy as to run into the docker image <code>export TERM=xterm<code></code></code>

Problem is that it does not survive the restart, as in any bash session actually. I will try to add it on the Dockerfile but why that the term is set on the run command I am not very optimistic with it.

I have tried to run nano on an ubuntu docker image and after installing it I always have this error:
<code>Error opening terminal: unknown.</code>

The solution is so easy as to run into the docker image <code>export TERM=xterm</code>