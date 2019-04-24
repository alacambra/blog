---
ID: 319
post_title: >
  Automatic update of client static files
  without redeploying the WAR file
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.tech/?p=319
published: true
post_date: 2019-04-24 19:49:44
---
When creating web-applications in node.js a bunch of nice features is available. One of my favorites is that when a change has been performed, the change is immediately available on the browser.

In the case of Java EE, we will need to redeploy each type, an operation that with my MacBook takes about t2 seconds and with my corporate laptop about 10 seconds. Even not a complete disaster, I think that we can agree on that is not really optimal.

So what I would like is that <strong>once I have performed a change on a static file (js, </strong>html<strong>, </strong>css<strong>), this change is also immediately on the browser using my standard application server</strong> (I have tested it with Wildfly).

And so we can achieve it:

1. Create an exploded war.

2: Compile project to create the target folder with the deployed sources.

3: Using the <a href="https://www.npmjs.com/package/onchange" target="_blank" rel="noopener">onchange tool</a> synchronize the statics file folder under webapp with the location where your IDE is copying the exploded files. This command looks for changes under a given directory and then executes any passed command. In our case, we just copy all the static files to the exploded target directory.

<code>onchange 'path/to/watched/src/' -- cp -Rf path/to/watched/src/ /path/to/exploded/war/files</code>

4: Begin coding.

With these simple steps, we will get our browser in snyc with our code. However, we still need to click F5 to update the browser.