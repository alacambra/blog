---
ID: 271
post_title: 'Solve Intellij Idea &#8220;Finished, saving caches&#8221; latency'
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=271
published: true
post_date: 2018-12-19 10:41:23
---
Just include the following line in your <code>/etc/hosts</code> file:
<pre class="lang-java prettyprint prettyprinted"><code><span class="lit">127.0</span><span class="pun">.</span><span class="lit">0.1</span><span class="pln">       localhost     </span><span class="pun">&lt;</span><span class="pln">your hostname goes here</span><span class="pun">&gt;.</span><span class="pln">local</span></code></pre>
And for IPv6 resolving, the same:
<pre class="lang-java prettyprint prettyprinted"><code><span class="pun">::</span><span class="lit">1</span><span class="pln">             localhost     </span><span class="pun">&lt;</span><span class="pln">your hostname goes here</span><span class="pun">&gt;.</span><span class="pln">local</span></code></pre>
Sources:

<a href="https://stackoverflow.com/questions/20658400/intellij-idea-hangs-while-finished-saving-caches">https://stackoverflow.com/questions/20658400/intellij-idea-hangs-while-finished-saving-caches</a>
<a href="https://stackoverflow.com/questions/30625785/intellij-freezes-for-about-30-seconds-before-debugging">https://stackoverflow.com/questions/30625785/intellij-freezes-for-about-30-seconds-before-debugging</a>
<a href="https://youtrack.jetbrains.com/issue/IDEA-157303">https://youtrack.jetbrains.com/issue/IDEA-157303</a>