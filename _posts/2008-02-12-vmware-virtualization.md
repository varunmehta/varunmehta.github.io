---
title: "Agile environment using virtualization"
layout: post
date: 2008-02-12
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- program management
- vmware
- virtualization
- continuous integration
star: false
hidden: false
category: blog
author: varunmehta
description: Agile environment using virtualization
---
> This article is aimed more towards Java & VMWare, but the same can be replicated for any other language & environment

## Abstract

You have a team of developers working on different modules for a project-product which are inter-dependant. Each developer diligently writes unit & integration tests supporting their code. You want to set-up an agile test environment to run the unit tests & staging server for integration test, but purchasing hardware for multiple machines is a constraint.

The following article provides a guide on how virtualization tools like VMware can be used to set-up staging or QA environment (Agile), with approximate minimum hardware & time investment.

## Hardware Sizing

The hardware sizing performed here is not an exact calculation, but an educated guess at the approximate system requirement to run the application.

| Application | RAM |  CPU | 
| Revision Control (SVN or CVS) | 512MB - 1GB | Single |
| Continuous Integration (Cruise Control or Bamboo)	| 1GB - 2GB | Single |
| Database (MySQL*) | 2GB - 4GB | Single-Dual |
| Webserver (Wiki, Bugzilla, JIRA) | 1GB | Single |

> *MySQL on VMware has some serious performance issues for production environments, if your application is very database intensive with thousands to millions of I/O per second, you might want to avoid virtualization all together. For testing purpose (application sanity, NOT performance) VM is decent.

Considering the above list of applications, and the assumption, each physical core can support 2 virtual cores.

### Hardware configuration
* Quad-core processor CPU
* 8GB of RAM
* 5 HDDs (1 OS + 4 HDD with RAID**)
* Other basic required components
> **Setting up RAID and the type of configuration suiting your needs is a separate chapter all together, We consider mirrored and stripped there are loads of articles available on the internet on this topic.

The approximate cost of the above system is roughly $2,500.00 - $3,500.00 (as the date of this article)

## Set-up

You can either install Windows or Linux (we are on an Ubuntu system) as the HostOS. Since you have 8GB of RAM on the physical machine, 32 bit OS's are not capable of using above 3-4GB. Use 64-bit distributions.

Download VMWare server from [http://www.vmware.com/products/server] select the distribution type depending on your OS. The guest and the host OS can be completely different, they need not be same there is no relation between them.
eg: You can install Windows as host and Linux as guest or vice-versa.

You can either create the virtual machines all by yourself using the VMware step-by-step wizard, or download 'appliances' created by others from the VMware site [http://www.vmware.com/appliances], this saves you the initial installation effort.

When you create a new VM, you are also asked the default networking connection type. NAT and Bridged are the most common options one selects from. Use NAT if you want the VM to talk within its own subnet only, or Bridged if you want other machines on the same subnet as the host access them.
eg: Your host machine is on `192.168.10.50`

> **Tip**: If you installing the guest yourself, you can create one master guest, with all the common applications configured (eg: OpenSSH server would be great to have on all the guests for remote management or java), you'll have to change the host name after that.

Power up each of the VM's and install the required applications for which they've been set and use them like any other machine on the network.
* Your source files are versioned on the Revision Control Server
* Your tests are run nightly on the Cruise Control Server
* Your team documents the whole project and process on the Wiki, and file bugs in Bugzilla
* Your MySQL server is used for running the DB & the supporting DBs for other apps (bugzilla, wiki)

These VM's need to be maintained like any other normal physical machine on the network.

## Pitfalls
 * Putting all your eggs in one basket, if the main VMware server fails, all the "machines" (VM's) fail.
* Since the server is dependant on the native OS it sits on, the capabilities of the VMServer is restricted by the OS
* Solution: Use commercial ESX Server or other alternatives

## Alternatives

You can use the Xen for virtualization. I've heard pretty good things about it too, with a few short comings & advantages over VMServer (that's a separate topic all together).

There is an article dedicated to Virtual Machines on Wikipedia, you can refer that depending on your needs and fix upon a solution that suits your needs better

## Glossary

**Virtualization** - The virtual machine simulates enough hardware to allow an unmodified "guest" OS (one designed for the same CPU) to be run in isolation

**Continuous Integration** - Continuous integration describes a set of software engineering practice's that speed up the delivery of software by decreasing integration times

**Revision Control** - Revision control (also known as version control (system) (VCS), source control or (source) code management (SCM)) is the management of multiple revisions of the same unit of information

**Host OS** - The operating system installed on the physical machine running VMware Server.

**Guest OS** - The operating system installed on the virtual machine.

## Bibliography
  1. [http://en.wikipedia.org/wiki/Agile_software_development](http://en.wikipedia.org/wiki/Agile_software_development)
  1. [http://en.wikipedia.org/wiki/Xen](http://en.wikipedia.org/wiki/Xen)
  1. [http://en.wikipedia.org/wiki/Comparison_of_virtual_machines](http://en.wikipedia.org/wiki/Comparison_of_virtual_machines)
  1. [http://en.wikipedia.org/wiki/Virtualization](http://en.wikipedia.org/wiki/Virtualization)
  1. [http://en.wikipedia.org/wiki/Continuous_Integration](http://en.wikipedia.org/wiki/Continuous_Integration)
  1. [http://en.wikipedia.org/wiki/Revision_control](http://en.wikipedia.org/wiki/Revision_control)
  1. [http://it20.info/blogs/main/archive/2007/11/26/83.aspx](http://it20.info/blogs/main/archive/2007/11/26/83.aspx)
  1. [http://mysql-dba-journey.blogspot.com/2007/11/mysql-and-vmware.html](http://mysql-dba-journey.blogspot.com/2007/11/mysql-and-vmware.html)