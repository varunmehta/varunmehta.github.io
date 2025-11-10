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
category: blog
author: varunmehta
description: Using GitHub to store python and block code from spike prime
---

After spending more than 2 weeks with kids coaching them on how different sensors and motors work, and trying to explain `f = ma` and `d = vt`, along with `circumference` of a circle and distance traveled by a wheel. They were finally down to building their first bot, and write some code. The team religiously after every class was uploading the `llsp3` file to github. I've also joined the Facebook group [**FLL Challenge: Share and Learn**](https://www.facebook.com/share/g/1F88RjiSYk/?mibextid=wwXIfr), and they have been a really helpful resource for new coaches. The site [FLLTutorials](https://flltutorials.com/) has a lot of learnings new coaches can leverage to help navigate with their teams. One common theme I've seen being posted on the facebook group was loss of code, due to accidentally not downloading the file or saving it when they started coding, or the code was lost due to crash, or they have no way to go back to an older version. The most common recommended solution was to use Google Drive or OneDrive to store the `llsp3` files after the code has been downloaded, and rename the file with the date of creation.

# Enter SpikePrimeGit

[SpikePrimeGit](https://varunmehta.github.io/spike-prime-git/) is a Chrome extension that helps students and coaches automatically save LEGO SPIKE Prime projects to GitHub. This makes it easy to:

* Version Control: Keep track of changes to your projects over time
* Backup: Never lose your hard work - everything is safely stored in the cloud
* Collaboration: Share projects with teammates and coaches
* Portfolio: Build a portfolio of your robotics projects

Developers for a long long time have been using some type of version control system to work on the same code base, allowing them to be collaborative with other developers and also having the freedom to go back to an older version in case of a mess up. The current flavour of version control in use is GitHub. So I decided to spend time learning to write a Chrome plugin. [Claude Code](https://www.claude.com/product/claude-code) did make the process a lot faster and easier to work with. The plugin is still under review from Chrome Web Store and GitHub Marketplace teams (which I did not know have a long process to approve plugins!). 

Checkout the [documentation](https://varunmehta.github.io/spike-prime-git/) and feel free to provide any feedback.

## Wishlist features

* AutoSync on every save (worried about GitHub rate limits)
* Use Issues for keep track of features kids plan to build for their robot
* Documentation of plans for their robot
