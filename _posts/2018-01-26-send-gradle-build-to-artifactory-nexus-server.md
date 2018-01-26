---
ID: 158
post_title: >
  Send gradle build to artifactory/nexus
  server
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=158
published: true
post_date: 2018-01-26 08:29:44
---
<code>
apply plugin: 'maven'
uploadArchives {
&emsp;repositories {
&emsp;&emsp;mavenDeployer {
&emsp;&emsp;&emsp;repository(url: "{PATH_TO_REPO}") {
&emsp;&emsp;&emsp;&emsp;authentication(userName: "{USER_NAME}", password: "{PASSWORD}")
&emsp;&emsp;&emsp;}
&emsp;&emsp;&emsp;pom.version = "{POM_VERSION}"
&emsp;&emsp;&emsp;pom.artifactId = "{ARTIFACT_ID}"
&emsp;&emsp;&emsp;pom.groupId = "{GROUP_ID}"
&emsp;&emsp;}
&emsp;}
}
</code>