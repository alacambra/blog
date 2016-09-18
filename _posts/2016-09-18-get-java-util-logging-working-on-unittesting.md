---
ID: 29
post_title: >
  Get java.util.logging working on
  UnitTesting
author: alacambra
post_date: 2016-09-18 14:22:20
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2016/09/18/get-java-util-logging-working-on-unittesting/
published: true
---
If you need to active the java.util.logging on your test, you can achieve it just adding the vm option
<code>-Djava.util.logging.config.file=/path/to/logging.properties</code>
where logging.properties can be something like

<code>handlers = java.util.logging.ConsoleHandler
.level=INFO
your.package.level = FINE
java.util.logging.ConsoleHandler.level = FINE
</code>

You can find a more complete example on <a href="\&quot;https://svn.apache.org/repos/asf/river/jtsk/skunk/surrogate/testfiles/logging.properties\&quot;">https://svn.apache.org/repos/asf/river/jtsk/skunk/surrogate/testfiles/logging.properties</a>

,