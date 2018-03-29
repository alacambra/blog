---
ID: 184
post_title: >
  Creating new Hyperledger Fabric material
  and other commands
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.de/?p=184
published: true
post_date: 2018-03-29 12:55:13
---
<strong>Create crypto-material:</strong>

cryptogen generate --config=./crypto-config.yaml --output="output-folder"

<strong>Create genesys block:</strong>

configtxgen -profile TwoOrgsOrdererGenesis -outputBlock ./test-channel-artifacts/genesis.block

&nbsp;