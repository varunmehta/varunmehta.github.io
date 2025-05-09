---
title: "Hot Deployment via Hudson"
layout: post
date: 2010-03-16
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- technical
- continuous integration
- deployment
star: false
hidden: false
category: blog
author: varunmehta
description: Hot Deployment
---
The build always makes it to the staging and production server after a series of rigorous tests. This ensures the build is complaint with the requirement and that none of the old features have been compromised in any way. Once in a while, a rare, but an annoying "Scope Creep" scenario does happen.

Just minutes before the demo some one would realize a missing feature or patch which missed the commit deadline and did not make it to the server. So as a quick temp fix we just deploy that file to ensure the code does not have to go through the grueling tests again. Some of the smart developers don't commit these hot patches to SVN or merge it with the patch branch, losing the feature again. 

Writing a shell script or a program which can check the MD5sum of all the files deployed, with the files about to be deployed can give us an idea if anything had been hot deployed. Hudson has a neat trick called as fingerprints for jar files, which is similar in the same aspect of checking MD5, so you know if you need to redeploy all the jar files or only the changed ones.