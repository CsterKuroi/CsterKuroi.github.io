---
layout: post
title: "Quick start of Mongo"
description: ""
category: 技术分享
tags: [mongo]
---
{% include JB/setup %}
# Quick start of Mongo
---

## Install
1.  `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6`
2.  `echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list`
3.  `sudo apt-get update`
4.  `sudo apt-get install -y mongodb-org`

## Start
1.  `sudo mkdir -p /data/db`
2.  `sudo chmod -R 700 /data/db`
3.  `sudo mongod --replSet=bigchain-rs`
4.  `sudo mongod --fork --logpath /var/log/mongodb/mongod.log --logappend  --replSet=bigchain-rs`

## Clinet
1. Download Robo 3T `https://robomongo.org/`
2. Connect to Mongod (e.g. xx.xx.xx.xx:27017)

## CLI
1. `mongo`
2. `show dbs`
3. `use bigchain`
4. `db`
5. `show collections`
6. `db.getCollection("bigchain").find().pretty()`

