---
ID: 226
post_title: Generate application fat jar
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=226
published: true
post_date: 2018-07-18 07:22:39
---
<pre>&lt;plugin&gt;
    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
    &lt;artifactId&gt;maven-assembly-plugin&lt;/artifactId&gt;
    &lt;executions&gt;
        &lt;execution&gt;
            &lt;id&gt;assembly&lt;/id&gt;
            &lt;phase&gt;package&lt;/phase&gt;
            &lt;goals&gt;
                &lt;goal&gt;single&lt;/goal&gt;
            &lt;/goals&gt;
        &lt;/execution&gt;
    &lt;/executions&gt;
    &lt;configuration&gt;
        &lt;descriptorRefs&gt;
            &lt;descriptorRef&gt;jar-with-dependencies&lt;/descriptorRef&gt;
        &lt;/descriptorRefs&gt;
    &lt;/configuration&gt;
&lt;/plugin&gt;</pre>