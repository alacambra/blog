---
ID: 5
post_title: Run Vert.x app from intellij
author: alacambra
post_date: 2016-09-18 08:49:50
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2016/09/18/run-vert-x-app-from-intellij/
published: true
---
To run Vert.x on intelliJ, it is only required to create a standard application Launcher with the following parameters:
<ul>
 	<li>Main class: the vert.x main class, i.e. io.vertx.core.Starter or whatever it is for your version.</li>
 	<li>VM options: whatever you need or empty</li>
 	<li>Program arguments: run de.lacambra.vertx.MyFirstVerticle</li>
 	<li>Working directory: normally your project directory</li>
</ul>