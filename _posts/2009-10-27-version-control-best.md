---
title: "Version Control Policy: Best Practices"
layout: post
date: 2009-10-27
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- program management
- best practice
- continuous integration
star: false
hidden: false
category: blog
author: varunmehta
description: Version Control Policy, Best Practices
---

Your code base is always under version control (if it's not, it's high time you did!), and developers are always scared about taking updates or committing files, under some supernatural fear, that an update will wipe out their local changes. This causes a lot of trouble in the team, when some developers have not updated their code base since a long time. I've compiled below a checklist of best practices.

Before you check in your code to subversion, here are a few points to follow.

* Ensure that there are 0 (zero) serious CheckStyle, PMD, FindBugs error (warnings should be reviewed). If you need an exception
* Checked in Code must build with all dependencies (not just your module).
* Checked in Code must not break unit tests.
* Check-ins without comments should be noted as a build break caused by the developer. 
* Before committing your changes to repository, it is advisable to synchronize the files, run an update and then commit your changes.

### Some best practices for not getting your code out of date.
* Synchronize your local SVN repository using eclipse instead of external third party tools.
* Update all the projects religiously every morning, irrespective of you having to commit your code that day or not. This will ensure you are always working on the latest code base.
* Instead of blindly running an update from eclipse, follow the following steps.
* Right click on all the projects in the project explorer, which are under version control
* Team --> Synchronize with repository.
* If it asks you to open-up the team perspective view, say "yes".
* At the bottom right corner of your eclipse you should see these three icons in blue, grey and red.
* Blue stands for incoming changes, grey outgoing and red as conflicting.


> If you have the count of red more than 0, then your repository has conflicting files.

* Under Synchronize tab, select the similar "red arrow", the list below is filtered to show only conflicting files.
* Double click on the file to open in compare editor, fix the errors, and then update the files.
* You can safely run an update on all the files with the blue incoming arrow icon.
* Under any circumstances, NEVER copy the .svn file from another use to your repository. This folder contains the svn connection and credential information.

## Changesets

Most if the commits in the system span across sub-modules and generally contain multiple files. When "applying a patch", "fixing a bug", "adding a new features". Always commit these group of files as one commit and not individual files, with the same comment!

**Example**: Jira ticket: ABC-123, introduced a new feature which involved changes in totality of 15 files, don't commit the 15 files one by one, but commit them all together as one group (changeset) of 15 files with proper comments.

Every time you hit a commit, there is a new revision created. After committing 15 files separately you've created 15 versions (or changesets), and incase an issue occurs and you need to revert the changes, you'll have to revert the revisions one by one. If these changes were done as a group, all you need to revert the one big changeset. Group commit also reduce the noise level and useless incrementing of revisions in SVN (any version control).

BUT, Each ticket needs to have its own commit changeset, not grouped with other tickets, unless there is a dependency between the tickets.

Further reading: [http://subversion.tigris.org/faq.html#changesets](http://subversion.tigris.org/faq.html#changesets)