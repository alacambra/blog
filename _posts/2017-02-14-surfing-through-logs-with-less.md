---
ID: 81
post_title: Surfing through logs with less
author: alacambra
post_date: 2017-02-14 19:16:21
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2017/02/14/surfing-through-logs-with-less/
published: true
---
<div><strong>shift g</strong>: goes to end.</div>
<div><strong>shift f</strong>: tails the file.</div>
<p style="padding-left: 30px;">  - <strong>ctrl+c:</strong> switch to normal mode (no tails)</p>

<div><strong>?:</strong> search upwards</div>
<div><strong>/:</strong> search downward</div>
<div style="padding-left: 30px;"> -<strong> n:</strong> search next match in current direction</div>
<div style="padding-left: 30px;"> -<strong> shift n:</strong> search next match in counter direction</div>
<div></div>
<div>Also useful to find 2 or more words in one line is the regex:</div>
<div style="padding-left: 30px;">- <strong><em>Word1</em>.+<em>Word2</em></strong> finds both words in the same line</div>
<div></div>
<div></div>
<div>As an extra to review logs, it is also useful the command grep with options <strong>after and before:</strong></div>
<div><strong>grep -A: </strong>lines after match</div>
<div><strong>grep -B:</strong> lines before match</div>