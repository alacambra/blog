---
ID: 97
post_title: Expand the site of an AWS xfs filesystem
author: alacambra
post_date: 2017-05-02 21:37:48
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=97
published: true
---
Once a volum has been enlarged, we need to extent the filesystem:

<em> growpart /dev/xvda 1</em>

If we want to see space available of a volum we can run the command <em>lsblk</em>