---
ID: 262
post_title: Recover from a messed rebase
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=262
published: true
post_date: 2018-10-05 08:59:16
---
<strong>from <a href="https://stackoverflow.com/questions/134882/undoing-a-git-rebase">https://stackoverflow.com/questions/134882/undoing-a-git-rebase</a></strong>

Find the head commit of the branch as it was before the rebase started:
<pre><code>git reflog
</code></pre>
and to reset the current branch to it.
<pre><code>git reset --hard HEAD@{<em>NUMBER</em>}
</code></pre>
(<em>Windows:</em> <code>git log "HEAD@{<em>NUMBER</em>}"</code>).<code></code>