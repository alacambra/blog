---
ID: 230
post_title: >
  Bootstraping Spring core using the
  context
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=230
published: true
post_date: 2018-07-21 11:50:03
---
<pre>AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
context.scan("cat.lacambra.prototype.statesmachine");
context.refresh();</pre>
At this point al found beans has been registered and can be used. As an example code would go further as follows, taking care that ExStateMachine.class  is annotated as @Component :
<pre>ExStateMachine machine = context.getBeanFactory().getBean(ExStateMachine.class);
machine.doSignals();

System.out.println("done!");</pre>
They are several available conext, all implementing the interface:
<pre>org.springframework.context.ApplicationContext</pre>
<pre>org.springframework.context:
ConfigurableApplicationContext.java

package org.springframework.context.annotation:
 AnnotationConfigApplicationContext.java

package org.springframework.context.support:
 AbstractApplicationContext.java
 AbstractRefreshableApplicationContext.java
 AbstractRefreshableConfigApplicationContext.java
 AbstractXmlApplicationContext.java
 ClassPathXmlApplicationContext.java
 FileSystemXmlApplicationContext.java
 GenericApplicationContext.java
 GenericGroovyApplicationContext.java
 GenericXmlApplicationContext.java
 StaticApplicationContext.java

package org.springframework.jca.context:
 ResourceAdapterApplicationContext.java
</pre>