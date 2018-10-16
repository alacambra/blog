---
ID: 266
post_title: >
  Add a new certificate to be accepted by
  maven
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=266
published: true
post_date: 2018-10-16 13:37:35
---
Add the cert:
.\{JAVA_HOME}\bin\keytool.exe -importcert -alias {certAlias} -file {file}.cer -keystore cacerts

Add the cacert path when running maven
set MAVEN_OPTS="-Djavax.net.ssl.trustStore=PATH\TO\cacerts"