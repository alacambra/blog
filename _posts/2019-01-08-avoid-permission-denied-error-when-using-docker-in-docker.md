---
ID: 280
post_title: 'Avoid &#8220;permission denied&#8221; error when using docker in docker'
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.tech/?p=280
published: true
post_date: 2019-01-08 08:19:26
---
When having the following message:
<pre>Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get <a href="http://%2Fvar%2Frun%2Fdocker.sock/v1.38/images/json" rel="nofollow noreferrer">http://%2Fvar%2Frun%2Fdocker.sock/v1.38/images/json</a>: dial unix /var/run/docker.sock: connect: permission denied
</pre>
you need to assure that the user running in the container has the correct uid and gid than a user on the host with access to docker. That means that into the container  the user must belong to the docker group in the host.

You can use the docker parameter <em>--group-add </em>to the docker command to enforce that the user running in docker is also added into the given GID
<pre>docker run -d -v /var/run/docker.sock:/var/run/docker.sock -p --group-add 999 ...
</pre>