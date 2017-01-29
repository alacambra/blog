---
ID: 75
post_title: >
  Pass parameters to java main method
  using graddle
author: alacambra
post_date: 2017-01-29 08:21:41
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2017/01/29/pass-parameters-to-java-main-method-using-graddle/
published: true
---
To pass for example a param "-a" with value "192.168.99.100:7051" to the static void main method that tha graddle task will run,  you will need to run graddle on the following form:  gradle  run  -PappArgs="['-a',  '192.168.99.100:7051']"