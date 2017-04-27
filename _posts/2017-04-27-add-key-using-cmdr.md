---
ID: 95
post_title: add-key using Cmdr
author: alacambra
post_date: 2017-04-27 14:36:51
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=95
published: true
---
If the error from the ssh-agent comes, this script will activate it:

@echo off
set keyToAdd=%1
ssh-agent | grep -v echo | sed -e "s/^/@set /" | sed -e "s/;.*$//" - &gt; call.cmd
call call.cmd
del call.cmd
ssh-add "%HOME%\.ssh\%keyToAdd%"
@echo on