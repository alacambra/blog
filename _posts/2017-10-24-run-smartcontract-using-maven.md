---
ID: 110
post_title: Run smartcontract using maven
author: alacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=110
published: true
post_date: 2017-10-24 11:43:56
---
<div class="161022">Normal execution:</div>
<div class="161022">mvn exec:java -Dexec.mainClass="path.to.chaincode" -Dexec.args="-a <em>pearIp</em>:<em>port</em>-i <em>chaincodeName</em>:<em>version</em>"</div>
<div class="161022"></div>
<div class="161022">Debug mode:</div>
<div class="161022">
<ul>
 	<li class="161022">On CommandLine: mvnDebug.cmd exec:java -Dexec.mainClass="path.to.chaincode" -Dexec.args="-a <em>pearIp</em>:<em>port</em>-i <em>chaincodeName</em>:<em>version</em>"</li>
 	<li class="161022">On intellij: new <strong>Remote </strong>connection.</li>
</ul>
</div>