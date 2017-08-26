---
ID: 107
post_title: >
  Apprenders and formating a default
  java.util.logger
author: alacambra
post_date: 2017-08-26 12:32:09
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=107
published: true
---
<code>handlers=java.util.logging.ConsoleHandler
.level=INFO
java.util.logging.FileHandler.level = INFO
java.util.logging.FileHandler.pattern   = log.%u.%g.txt
java.util.logging.SimpleFormatter.format= %1$tl:%1$tM:%1$tS %1$Tp %2$s %4$s: %5$s%n
java.util.logging.ConsoleHandler.level=INFO
java.util.logging.ConsoleHandler.formatter=java.util.logging.SimpleFormatter
java.util.logging.FileHandler.formatter=java.util.logging.SimpleFormatter
</code>

More info about SimpleFormatter: <a href="https://docs.oracle.com/javase/7/docs/api/java/util/logging/SimpleFormatter.html#SimpleFormatter()" target="_blank" rel="noopener noreferrer">https://docs.oracle.com/javase/7/docs/api/java/util/logging/SimpleFormatter.html#SimpleFormatter()</a>

More Info about formatting params:
<a href="https://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html" target="_blank" rel="noopener noreferrer">https://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html</a>