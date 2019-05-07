---
ID: 295
post_title: 'Extrapolate &#8220;run&#8221; command of docker container'
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.tech/?p=295
published: true
post_date: 2019-03-18 04:09:43
---
If you want to get a docker run command that emulates a running container, you can use <a href="https://github.com/lavie/runlike">assaflavie/runlike</a> :
<code>docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike YOUR-CONTAINER</code>

As an output you get a docker run command containg all required parameters to get the same result as "YOUR-CONTAINER".

E.g. To get the run command of a mariaDB container:
<code>docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike <strong>mariadb</strong></code>
and you get:
<code>docker run
--name=mariadb
--hostname=some-name
--env="MYSQL_ROOT_PASSWORD=passsword"
--env="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
--env="GOSU_VERSION=2.00"
--env="GPG_KEYS=XXXX XXXX XXXX XXXX"
--env="MARIADB_MAJOR=20.0"
--env="MARIADB_VERSION=1:10.3.13+maria~bionic"
--volume="/path/to/mariadb-data:/var/lib/mysql"
--volume="/var/lib/mysql"
-p 33333:3306
--restart=no
--detach=true mariadb:latest mysqld</code>