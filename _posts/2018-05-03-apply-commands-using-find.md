---
ID: 201
post_title: Apply commands using find
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=201
published: true
post_date: 2018-05-03 22:03:37
---
find . -name *.class -type f -exec rm;

find . -type f |grep java|xargs sed -i -e 's/pattern/replace-for/g'