---
title: "AWS IoT Garage Opener"
layout: post
date: 2019-11-15
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- raspberry pi
- photography
- projects
star: false
hidden: false
projects: true
category: blog
author: varunmehta
description: AWS IoT Garage Opener
---

As part of the [Slalom IoT hackathon](https://hackathon.slalom.com/hackathons/internet-of-things), I formed a [team with my colleagues](https://hackathon.slalom.com/teams/open-sesame), revived an old project, and extended it to be cloud enabled. This code uses aws-iot-core and other libraries to communicate with the server. For now it's a simple repo, will break it down to smaller sections once the lambda and other pieces of code take shape.

Using the AWS IoT API, the Pi stays local to your network, and also due to the whole certificate exchange and other IoT core security measures you know how the data is traveling b/w your pi and the n/w.

[The project is covered in detail on the README page of the project](https://github.com/varunmehta/aws-iot-garage-controller).

![Demo](/assets/images/projects/garage/garage_demo.gif)