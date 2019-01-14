---
ID: 283
post_title: Refactor a class to use flow pattern
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.tech/?p=283
published: true
post_date: 2019-01-14 16:01:40
---
How o convert public void setX to become a public SomeClass setX(...)?
Apply regex:
<pre>public void set([\w]+.+\{(\n\s+).+)
</pre>
to be replaced by
<pre>public SomeClass set$1$2return this;
</pre>
It Transforms
<pre>public void setX(int x){
this.x;
}
</pre>
to
<pre>public MyClass setX(int x){
this.x;
return this;
}
</pre>
Tested with Intellij.