---
title: "Raspberry Pi - Spot Payload + Mount"
layout: post
date: 2023-08-07
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- technical
- robotics
- spot
- boston dynamics
- raspberry pi
star: false
hidden: false
category: blog
author: varunmehta
description: Building a raspberry pi as a payload for Spot.
---

After creating the [Pi4 as a payload](/spot-rapsberry-pi-payload), we had good luck running things off the Pi. We `scp` our files over to Pi, then `ssh` in run our scripts. This was going great, but the power bank was a pain to lug around, and was also causing occasional [brown outs](https://en.wikipedia.org/wiki/Brownout_(electricity)). When ever the CPU load spiked, the Pi ended up rebooting, stalling the mission

I decided to build a [custom payload](https://dev.bostondynamics.com/docs/payload/readme) for spot. Time to tap the [payload port](https://dev.bostondynamics.com/docs/payload/robot_electrical_interface.html) on the back of spot, and see if we can mooch off the power from it

![Electrical Interface](/assets/images/posts/spot/spot_electrical_interface.png)

## Considerations 
 * The interface voltage never exceeds 72V, and can accept up to 9-13A total current combined across both ports.
 * The interface also allows you to tap into the network, which means I can get rid of the dangling ethernet cable. 

I had a couple of LM2596 DC-to-DC buck converters lying around, but the are limited to 35V/3A, but that was not going to suffice, I needed something more heavy duty.
 > Spot's Battery voltage ranges from 35V for a fully discharged battery to 58.8V for a full charge.

## Components

### [RS232 D-Sub Connector](https://www.amazon.com/dp/B09CPBRTKZ)

![D-Sub](/assets/images/posts/spot/IMG_1959.jpeg)

### [100W 6A DC-DC Buck Converter](https://www.amazon.com/dp/B09FNBSZTR)

![Buck Converter](/assets/images/posts/spot/IMG_1960.jpeg)

### [3D printed Case](https://www.tinkercad.com/things/3wuU3eND38z-spot-pi-peripheral-box-v4-direct-wire)
I designed the mount to have the Pi on the rails. This is a very crude model made in Tinkercad. Before I was comfortable with [OnShape](https://onshape.com/).

![Pi Mount](/assets/images/posts/spot/pi-mount.png)

![3D Printed](/assets/images/posts/spot/IMG_1961.jpeg)

Used M5 bolts and T-nuts we were able to mount the pi and power it off the payload port! 