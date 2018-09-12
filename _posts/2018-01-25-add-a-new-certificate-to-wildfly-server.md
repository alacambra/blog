---
ID: 154
post_title: Add a new certificate to wildfly server
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=154
published: true
post_date: 2018-01-25 12:58:28
---
- <strong>Add a realm for the new certificate</strong>:
/core-service=management/security-realm={<em>NEW_REALM_NAME</em>}:add()

- <strong>Set path to keystore</strong>:

/core-service=management/security-realm={<em>NEW_REALM_NAME</em>}/server-identity=ssl:add(keystore-path=ssl-keystore.jks, keystore-relative-to=jboss.server.config.dir,keystore-password=changeit, alias=myhostname.local, key-password=changeit)

or

/core-service=management/security-realm={<em>NEW_REALM_NAME</em>}/server-identity=ssl:write-attribute(name=keystore-relative-to,value=jboss.server.config.dir)

- <strong>Set keytore</strong>:
/core-service=management/server-identity=ssl:add(keystore-password={<em>KEY_STORE_PASSWORD</em>}, keystore-path={<em>KEY_STORE_FILE_NAME.jks</em>})

- <strong>Add realm to the https listener</strong>:
/subsystem=undertow/server=default-server/https-listener=https:write-attribute(name=security-realm,value={<em>NEW_REALM_NAME</em>})