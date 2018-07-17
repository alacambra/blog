---
ID: 221
post_title: Runing test from jar with Junit5
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=221
published: true
post_date: 2018-07-17 15:18:57
---
<div class="161206">java -jar <strong>junit-platform-console-standalone-1.3.0-M1.jar</strong> -n .*IT -scan-class-path -cp target\test-classes\(test.jar) -cp target\app-jar-with-dependencies.jar</div>
<div></div>
<div>where:</div>
<ul>
 	<li><strong>-n .*IT</strong> is a regex looking for files suffixed with <strong>IT</strong> <em>(default: ^(Test.*|.+[.$]Test.*|.*Tests?)$)</em></li>
 	<li><strong>-scan-class-path</strong> look for tests on classpath</li>
 	<li><strong>-cp</strong>: the classpath</li>
</ul>
<strong>Bonus:</strong>

to compile test classes:  mvn test-compile compile

to create test jar:
<pre>&lt;plugin&gt;
    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
    &lt;artifactId&gt;maven-jar-plugin&lt;/artifactId&gt;
    &lt;version&gt;3.1.0&lt;/version&gt;
    &lt;executions&gt;
        &lt;execution&gt;
            &lt;goals&gt;
                &lt;goal&gt;test-jar&lt;/goal&gt;
            &lt;/goals&gt;
        &lt;/execution&gt;
    &lt;/executions&gt;
&lt;/plugin&gt;</pre>