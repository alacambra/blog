---
ID: 254
post_title: Analyze TCP traffic on windows
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=254
published: true
post_date: 2018-09-27 10:00:12
---
use RasCap.exe (https://www.netresec.com/index.ashx?page=RawCap):

RawCap.exe -f 127.0.0.1 dumpfile.pcap

open it with wireshark.