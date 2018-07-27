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
<pre>EncryptedFileInfo info = cut.storeEncryptedFile(encryptionSecret, plainContents, fileName);

ArgumentCaptor&lt;byte[]&gt; argument = ArgumentCaptor.forClass(byte[].class);

verify(cut).createFileAndAdd(eq(fileName), argument.capture());
byte[] encryptedContent = argument.getAllValues().get(0);</pre>
Where intercepted method is:
<pre>void createFileAndAdd(String fileName, byte[] encryptedContents);
</pre>