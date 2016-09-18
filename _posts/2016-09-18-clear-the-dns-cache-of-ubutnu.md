---
ID: 12
post_title: Clear the dns cache of Ubutnu
author: alacambra
post_date: 2016-09-18 13:07:46
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2016/09/18/clear-the-dns-cache-of-ubutnu/
published: true
---
It can be useful to flush your dns cache. For example if the IP of a domain is changing continuously like is the case of an EC2 instance.

As posted on http://askubuntu.com/questions/414826/how-to-flush-dns-in-ubuntu-12-04 nscd will do the job:
<pre><code>sudo apt-get install nscd
#Flush DNS Cache in Ubuntu by restarting the nscd
sudo /etc/init.d/nscd restart</code>
</pre>
Of course, if you have the possibility, it can be also a good idea, to just reduce the TTL time of the DNS record.