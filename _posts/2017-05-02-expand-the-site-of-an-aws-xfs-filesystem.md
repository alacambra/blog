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
Once a volum has been enlarged then, we need
<ol>
 	<li>to extent the filesystem:<em> growpart /dev/xvda 1</em></li>
 	<li>resize file system to grow all the way to fully use new partition space:
<div class="161022"><em>sudo resize2fs /dev/xvda1</em></div></li>
</ol>
If we want to see space available of a volum and the used by the partition, we can run the command <em>lsblk</em>