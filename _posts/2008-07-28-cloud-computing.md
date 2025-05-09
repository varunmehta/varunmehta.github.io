---
title: "Cloud Computing on VMWare or Xen"
layout: post
date: 2008-07-28
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- technical
- cloud
star: false
hidden: false
category: blog
author: varunmehta
description: Cloud Computing 
---

What is Cloud Computing (CC)?
A lot has already been said and blogged about cloud computing. Just to give you a one liner about it;

It's the availability of system resources to allow scalability of the system as and when required by the application.

As and when required?
Consider an example of a build server running in our VM environment, now this server during it's peak instrumentation of code and all kinds of code analysis requires the power of a quad core machine with 4GB RAM, so when you perform your hardware requirement analysis for this server, you consider all these factors and build a VM fulfilling these requirements.

Over the period of time your system usage reports show a small spike in system resource usage every 3-4 hours (every commit build) and a peak spike for 2-2.5 hours every 24 hours (nightly builds), the remaining time the system is pretty much idle doing nothing, eating up precious RAM allocation and number of CPUs dedicated.

Now if we push this setup in a CC environment, the system will use bare minimum resources when idle and grab all the possible resources from the cluster, during peak cycles. This allows us to leverage the un-utilized system resources, during non-peak cycles.

VMWare has [DRS - Distributed Resource Scheduler](http://www.vmware.com/products/vi/vc/drs.html), which helps the VMs attain similar to cloud status to dynamically allocate the resources.

Now Xen also has something similar, but then is it available for a small start-up (read free)? Yes, [Nimbus@UC](http://workspace.globus.org/clouds/nimbus.html) is something we can look at, will try digging in more into it and see what we can achieve out of it. So let us see how we can leverage the existing hardware to allow maximum virtual resource utilization.

**Update**: Read this article http://highscalability.com/eucalyptus-build-your-own-private-ec2-cloud