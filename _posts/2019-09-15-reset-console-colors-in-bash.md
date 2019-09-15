---
ID: 391
post_title: Reset console colors in bash
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.tech/?p=391
published: true
post_date: 2019-09-15 10:06:15
---
If after some logs the color of your console do not return back to white, use the following command:
<pre class="lang-bsh prettyprint prettyprinted"><code><span class="pln">echo </span><span class="pun">-</span><span class="pln">e </span><span class="str">"\033[0m"</span></code></pre>