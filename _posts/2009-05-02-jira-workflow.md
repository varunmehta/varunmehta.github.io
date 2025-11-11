---
title: "Jira Workflow"
layout: post
date: 2009-05-02
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- program management
- jira
star: false
hidden: false
category: blog
author: varunmehta
description: Jira Workflow
---
[Operative](https://operative.com) like other companies use JIRA for issue tracking. We were impressed with [the article on using JIRA](http://confluence.atlassian.com/display/JIRACOM/JIRA+in+an+Agile+Environment). So decided to go a step ahead and implement JIRA not only for issue tracking, but also for development tracking (nothing new I know many companies do that!), but we decided to add some more intelligence in the normal 4 step JIRA workflow. JIRA gives you the option to customize your own workflow.

The steps are closely related to the ones in a normal development cycle of a module or a piece of functionality; something that comes naturally not only to the developer, but also helps the managers track them. So let's list them down;
 1. Capture Requirement
 1. Design Document
 1. Development
 1. Unit Test
 1. QA Testing
 1. Ship the feature.

These are the major steps involved. So we charted these with JIRA, and this is the final logical workflow in use.

1. Open Issue
1. In Progress
1. More Info Needed (optional step)
1. Development Complete
1. Unit Tested (or No Unit Test)
1. QA Approved
1. Resolve Issue
1. Close Issue

Once a developer gets the issue/feature to take care of; they go ahead and start the progress, when the requirement is complete. At any given point of time, one can point out the key features the developer is working on.

If there is any more information needed from the business analyst or the decision maker, reassign the issue to them and mark it as **More Info Needed** who when provides more info, assigns back to you. Why the run around; well helps you document the issue for future reference.

Back **In Progress** the developer continues with the quest to complete it. When finished, updates the status as **Development Complete**; and starts working on writing a **Unit Test** for it.

There are cases, when there are no unit tests needed or possible for a piece of code, so the developer has two paths (considering does not break anything else!)

Go to JIRA, create a copy of the existing workflow and add your points in between.

>There is some interesting debate about the Unit Test being written first and then the code, it's called TDD Test Driven Development; so you code knowing what to expect.
