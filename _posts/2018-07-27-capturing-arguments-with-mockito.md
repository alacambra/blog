---
ID: 235
post_title: Capturing arguments with mockito
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=235
published: true
post_date: 2018-07-27 15:15:01
---
<pre><code>ArgumentCaptor argument = ArgumentCaptor.forClass(ClassToBeCaptured.class);
Mockito.when(someInstance.method(argument.capture())).thenAnswer(invocation -&gt; argument.getValue());

cut.splitSlot(toSplit, splitter).getNextSlot();
ResourceSlot splitterNext = argument.getAllValues().get(1);
</code></pre>