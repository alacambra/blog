---
ID: 20
post_title: >
  Use multiple parameters with jjs in
  linux shebang script
author: alacambra
post_date: 2016-09-18 14:03:15
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2016/09/18/use-multiple-parameters-with-jjs-in-linux-shebang-script/
published: true
---
If you try to use multiple parameters in the script on a linux OS like this,
<code>#!/usr/bin/jjs -strict -scripting -fv
</code>
you will see something like this:
<code>"-strict -scripting -fv" </code><em>is not a recognized option. Use "-h" or "-help" to see a list of all supported options.</em>

That happens because the linux interpreter is using all the parameters as a unique parameter.
The workaround is to use the *-J-Dnashorn.args* like

<code>#!/usr/bin/jjs -J-Dnashorn.args= -strict -scripting -fv
</code>
If you try to use multiple parameters in the script on a linux OS like this,

<code>#!/usr/bin/jjs -strict -scripting -fv
</code>

you will see something like this:

<code> "-strict -scripting -fv" is not a recognized option. Use "-h" or "-help" to see a list of all supported options. </code>

That happens because the linux interpreter is using all the parameters as a unique parameter.
The work around is to use the <code>-J-Dnashorn.args</code> like
<code>#!/usr/bin/jjs -J-Dnashorn.args= -strict -scripting -fv</code>
and it will work like a breeze.