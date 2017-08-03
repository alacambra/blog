---
ID: 12
post_title: Clear the dns cache
author: alacambra
post_date: 2016-09-18 13:07:46
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=12
published: true
---
On Ubuntu:

As posted on http://askubuntu.com/questions/414826/how-to-flush-dns-in-ubuntu-12-04 nscd will do the job:
<pre><code>sudo apt-get install nscd
#Flush DNS Cache in Ubuntu by restarting the nscd
sudo /etc/init.d/nscd restart</code></pre>
&nbsp;

On Mac Sierra:

sudo dscacheutil -flushcache;sudo killall -HUP mDNSResponder;