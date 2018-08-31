---
ID: 247
post_title: Replace to upper/low case with regex
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=247
published: true
post_date: 2018-08-31 19:19:42
---
\U$1 will set all chars contained into group $1 to upper case.

\U$1 will set the first char of the group $1 to upper case.

\L$1 will set all chars contained into group $1 to upper case.

\l$1 will set the first char of the group $1 to lower case.

E.g.

SOME_TEXT against regex _([a-z]+) replaced by \l$1 will produce SOME_tEXT

SOME_TEXT against regex _([a-z]+) replaced by \L$1 will produce SOME_text

&nbsp;

&nbsp;