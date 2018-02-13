---
ID: 169
post_title: Mango queries for couchdb
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=169
published: true
post_date: 2018-02-13 09:44:38
---
Match any using regex search:
<code>
{
"selector":{
"_id":{
"$regex":"${REGEX_EXPRESSION}"
}
}
}
</code>