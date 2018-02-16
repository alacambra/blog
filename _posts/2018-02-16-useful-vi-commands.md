---
ID: 173
post_title: Useful vi commands
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=173
published: true
post_date: 2018-02-16 08:27:39
---
<a href="https://www.cs.colostate.edu/helpdocs/vi.html">https://www.cs.colostate.edu/helpdocs/vi.html</a>
<ul>
 	<li><strong>0 (zero), $</strong>: cursor to start of the line, cursor to end of the line</li>
 	<li><strong>w, b</strong>: beggining of next word, beginning of preceding word</li>
 	<li><strong>:<em>n</em> (where n is a number) or nG</strong>: move cursor to line <em>n</em></li>
 	<li><strong>:$ or G:</strong> Move cursor to last line</li>
</ul>
<ul>
 	<li><strong>^f,^b:</strong> move forward / backwards one screen</li>
 	<li><strong>^d, ^u</strong>: move down (forward)/up (back) one half screen</li>
</ul>
<ul>
 	<li><strong>u</strong>: undo</li>
</ul>
<ul>
 	<li><strong>yy</strong>: copy line</li>
 	<li><strong><em>N</em>yy</strong>: copy the next <em>N</em> lines</li>
 	<li><strong>p</strong>: paste</li>
</ul>
<dl></dl>
&nbsp;
<table border="">
<tbody>
<tr>
<th>*</th>
<th align="LEFT" nowrap="nowrap"><tt>x</tt></th>
<td><i>delete single character under cursor</i></td>
</tr>
<tr>
<th></th>
<th align="LEFT" nowrap="nowrap"><tt>Nx</tt></th>
<td><i>delete N characters, starting with character under cursor</i></td>
</tr>
<tr>
<th></th>
<th align="LEFT" nowrap="nowrap"><tt>dw</tt></th>
<td><i>delete the single word beginning with character under cursor</i></td>
</tr>
<tr>
<th></th>
<th align="LEFT" nowrap="nowrap"><tt>dNw</tt></th>
<td><i>delete <tt>N</tt> words beginning with character under cursor;
e.g., <tt>d5w</tt> deletes 5 words</i></td>
</tr>
<tr>
<th></th>
<th align="LEFT" nowrap="nowrap"><tt>D</tt></th>
<td><i>delete the remainder of the line, starting with current cursor position</i></td>
</tr>
<tr>
<th>*</th>
<th align="LEFT" nowrap="nowrap"><tt>dd</tt></th>
<td><i>delete entire current line</i></td>
</tr>
<tr>
<th></th>
<th align="LEFT" nowrap="nowrap"><tt>Ndd</tt> <i>or</i> <tt>dNd</tt></th>
<td><i>delete <tt>N</tt> lines, beginning with the current line;
e.g., <tt>5dd</tt> deletes 5 lines</i></td>
</tr>
</tbody>
</table>
&nbsp;