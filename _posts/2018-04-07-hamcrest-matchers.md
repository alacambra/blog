---
ID: 191
post_title: Hamcrest matchers
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=191
published: true
post_date: 2018-04-07 18:58:59
---
<ul>
 	<li>Hamcrest collections:
<ul>
 	<li>Package: <em>org.hamcrest.collection</em></li>
 	<li>Javadoc: http://hamcrest.org/JavaHamcrest/javadoc/1.3/org/hamcrest/collection/package-summary.html</li>
 	<li>Check not empty collections:</li>
</ul>
</li>
</ul>
<pre>assertThat(someCollection, not(IsEmptyCollection.empty()));</pre>