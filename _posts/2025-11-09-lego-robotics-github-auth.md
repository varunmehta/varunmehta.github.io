---
title: "SpikePrimeGit - Chrome and GitHub plugin"
layout: post
date: 2025-11-09
image: https://varunmehta.github.io/spike-prime-git/images/icon128.png
headerImage: true
tag:
- robotics
- FLL
- github
- authentication
- projects
- lego
- technical
- architecture
star: false
hidden: false
projects: true
category: blog
author: varunmehta
description: Using GitHub to store python and block code from spike prime
---

I joined the Facebook group [**FLL Challenge: Share and Learn**](https://www.facebook.com/share/g/1F88RjiSYk/?mibextid=wwXIfr), and it's a helpful resource for new coaches. Another site [FLLTutorials](https://flltutorials.com/) also has a lot of guides for new coaches, to help navigate the program with their teams. 

After spending more than 2 weeks with kids coaching them on how different sensors and motors work, and trying to explain `f = ma` and `d = vt`, along with `circumference` of a circle and distance traveled by a wheel. They were finally down to building their first bot, and write some code. The team religiously after every class was uploading the `llsp3` file to github. 

One common theme I see being posted regularly on the facebook group was frustration due to loss of code, due to accidentally not downloading the file or not saving it when they started coding. The code was lost due to system/browser crash, and they have no way to go back to an older version. The most common recommended solution is to use Google Drive or OneDrive to store the `llsp3` file. Download the code and rename the file with the date stamp of the day.

# Enter SpikePrimeGit

> **UPDATE**: *The Chrome plugin is now available on the web store!*

[![Available in the Chrome Web Store](https://developer.chrome.com/static/docs/webstore/branding/image/iNEddTyWiMfLSwFD6qGq.png)](https://chromewebstore.google.com/detail/spikeprimegit/ldiklhfinipoikhmfbnamjklkigcppoe)

[SpikePrimeGit](https://varunmehta.github.io/spike-prime-git/) is a Chrome extension that helps students and coaches automatically save LEGO SPIKE Prime projects to GitHub. This makes it easy to:

* Version Control: Keep track of changes to your projects over time
* Backup: Never lose your hard work - everything is safely stored in the cloud
* Collaboration: Share projects with teammates and coaches
* Portfolio: Build a portfolio of your robotics projects

Developers for a long long time have been using some type of a version control system to work on the same code base, allowing them to be collaborative with other developers and also having the freedom to go back to an older version in case of a mistake. The current flavour of the month for version control is `git` and GitHub it the best free cloud service to host repositories. 

I spent some time learning how to write a Chrome plugin. [Claude Code](https://www.claude.com/product/claude-code) did make the process a lot faster and easier to work with. There are 2 parts to a plugin, a GitHub Marketplace App, and a Chrome Web Store plugin. Both of which are under review and can take from 3 days to 6 weeks depending upon the level of scrutiny required.  

If you are a skilled developer, you can side load the plugin and test it. Checkout the [documentation](https://varunmehta.github.io/spike-prime-git/) and please provide any [feedback](https://github.com/varunmehta/spike-prime-git/issues).

