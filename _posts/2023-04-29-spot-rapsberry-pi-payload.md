---
title: "Raspberry Pi - Spot Payload"
layout: post
date: 2023-04-29
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- technical
- spot
- boston dynamics
- raspberry pi
star: false
hidden: false
category: blog
author: varunmehta
description: Building a raspberry pi as a payload for Spot.
---

Slalom had already invested $70K in [purchasing Spot](https://www.linkedin.com/in/spot-slalom-420aa5224/), with all the camera accessories, getting the I/O on top was another 7K, which was out of budget for the year. Till now for any kind of missions, or scripts to be run on spot, we were connecting a laptop through a wired ethernet cable, and this was getting cumbersome. If run programs via RCP, and if the latency goes over 5ms, then Spot drops the connection.

![Spot](/assets/images/posts/spot/IMG_1104.jpeg)

In order to keep persistent connection, we need a device on spot, which can keep a consistent wired connection with Spot, and also allow it to be mobile and connected to the internet. I decided to leverage [Pi4](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/), see if we can connect the two and get it working with Spot. 

## Story so far
 * Connect Pi to IoT WiFi
 * Connect Pi to Spot via ethernet cable 
 * Create a [bridge network](https://www.willhaley.com/blog/raspberry-pi-wifi-ethernet-bridge/) between Pi & Spot, keeping them on separate networks 

Now we can run scripts on the Pi, which allows us to run missions on Spot.
