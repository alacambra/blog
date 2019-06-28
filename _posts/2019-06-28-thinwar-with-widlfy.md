---
ID: 363
post_title: ThinWar with Widlfy
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.tech/?p=363
published: true
post_date: 2019-06-28 11:17:29
---
I have heard the concept of ThinWars several years before in one of the airhacks workshop from Adam Bien.

Basically, the idea is that in any project packaged into a war should contain only business logic. No jar dependencies should be packaged with the business code. That reduces drastically the size of the final war file, improving build, package, delivery and start-up times.

So, to be able to remove all dependencies from our war artifact, we need to change the scope from compiled to provided, and then add those dependencies directly to our application server.
In a naive first approach, I have tried just to add those dependencies to the java classpath. However, the wildfly's class loading is much more complex than that.

To add new dependencies into the Widlfly application server, we need to add them creating a new module. That means that we must create a new module.xml file, declaring included jars and dependencies.

So, to create a new module we must follow the next steps.
<ul>
 	<li>Create the module directory:</li>
</ul>
mkdir -p $JBOSS_HOME/modules/my/module/name/main
<ul>
 	<li>Create a module.xml file with including our depenedencies. Required jars can be directly downloaded form <a href="http://Maven central repos">https://mvnrepository.com</a></li>
</ul>

[xml]
&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;
&lt;module xmlns=&quot;urn:jboss:module:1.1&quot; name=&quot;my.module.name&quot;&gt;
   &lt;resources&gt;
      &lt;resource-root path=&quot;{my-dependency-jar1.jar}&quot; /&gt;
      &lt;resource-root path=&quot;{my-dependency-jar2.jar}&quot; /&gt;
   &lt;/resources&gt;
&lt;/module&gt;
[/xml]

<ul>
 	<li>Declare the module as a global module into settings.xml so that it can be used by any deployed application. Under the <strong>&lt;subsystem&gt;</strong> section add:</li>
</ul>

[xml]
&lt;global-modules&gt;
&lt;modulename=&quot;my.module.name&quot;slot=&quot;main&quot;/&gt;
&lt;/global-modules&gt;
[/xml]