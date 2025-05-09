---
title: "Reindex Elasticsearch"
layout: post
date: 2016-01-28
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- technical
- elasticsearch
star: false
hidden: false
category: blog
author: varunmehta
description: script to reindex elasticsearch
---

We started off with the default 5 shards of Elasticsearch and then suddenly realized, it was way beyond what we warranted for. After a conversation with the ES support team (which by the way is awesome! I definitely recommend them), we decided to downsize our shard level to 1.

I've used [elasticdump](https://www.npmjs.com/package/elasticdump) to carry out the task. It is fairly quick and versatile tool.

The script assumes you have modified elasticsearch.yml to have the desired shard/index size, and have restarted the cluster for the property to take effect. The script is just a general reindexing script, it backups up the data, deletes the indices backed up and then restores from the backup.

## The Script
{% gist varunmehta/d0553071dad4171e4dd7 %}
