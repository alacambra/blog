---
ID: 242
post_title: List current java PIDs and vm status
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=242
published: true
post_date: 2018-08-12 15:59:15
---
<pre>jps [-q] [-mlvV] [&lt;hostid&gt;]</pre>
Most useful:
<pre>jps -v</pre>
then use jstat:

jstat -&lt;option&gt; {jpid}
<pre>jstat -options
-class
-compiler
-gc
-gccapacity
-gccause
-gcmetacapacity
-gcnew
-gcnewcapacity
-gcold
-gcoldcapacity
-gcutil
-printcompilation
</pre>