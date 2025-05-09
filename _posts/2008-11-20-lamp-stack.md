---
title: "Setup a LAMP stack on your local system"
layout: post
date: 2008-11-20
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- technical
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

This is an old post I had written on google docs, before VMware Server was free for the general user. Thought could be still more relevant to the general developer for testing in Linux environment. VMPlayer I believe is lighter than VMware Server.

There are 2 stages of setting up the development & testing environment for yourself. The preferred work environment is Linux. If you already on Linux then you can safely skip Stage I, you can directly proceed to Stage II, also if you have Linux already installed, just cross check if you have the LAMP (Linux + Apache + MySQL + PHP) server installed.

## Pre Installation Software Download Links
* [VMPlayer](http://www.vmware.com/download/player/)
* [Ubuntu](http://www.ubuntu.com/getubuntu/download)

### STAGE I: Setting up Ubuntu on VMWare.
* Download Ubuntu/Xubuntu/Kubuntu Desktop edition ISO, what ever you like... all the same just different file-managers (Gnome/Xfe/KDE resp.). If you are comfortable with command line, then you can also install the Server edition with no XWindows and only commandline.
* Download and install VMPlayer for your system.
* Download qemu for your operating system and extract in any directory you like.
* Open your commandline to go ahead to bin folder of qemu and type
```qemu-img create -f vmdk ubuntu.vmdk 3G
```
* Here we are creating a 3GB, virtual hard drive in VMWare format. This file will now act as our hard drive for VMWare to install an OS on it. The name of the file is ubuntu.vmdk, you can name it what ever you wish to.
* Now the main vmx file (The VMWare configuration file). change the highlighted paths as per your system.
 
 {% highlight bash %}
 #!/usr/bin/vmware
config.version = "8"
virtualHW.version = "4"
ide0:0.present = "TRUE"
ide0:0.filename = "ubuntu.vmdk"
# The amount of RAM you want to allot to the Operating system. For Desktop use 512 and server just 256.
memsize = "512"
MemAllowAutoScaleDown = "FALSE"
ide1:0.present = "TRUE"

#ide1:0.fileName = "auto detect"
#ide1:0.deviceType = "cdrom-raw"

ide1:0.fileName = "ubuntu-7.04-server-i386.iso"
ide1:0.deviceType = "cdrom-image"

ide1:0.autodetect = "TRUE"
floppy0.present = "FALSE"
ethernet0.present = "TRUE"
usb.present = "TRUE"
sound.present = "TRUE"
displayName = "Ubuntu LAMP Server"
guestOS = "ubuntu"
nvram = "ubuntu-server-three.nvram"
MemTrimRate = "-1"

ide0:0.redo = ""
ethernet0.addressType = "generated"
uuid.location = "56 4d ce 99 e0 d2 2b bf-73 47 ac 62 65 13 57 86"
uuid.bios = "56 4d ce 99 e0 d2 2b bf-73 47 ac 62 65 13 57 86"

tools.syncTime = "TRUE"
ide1:0.startConnected = "TRUE"

uuid.action = "create"

checkpoint.vmState = "ubuntu-lamp-server.vmss"

isolation.tools.hgfs.disable = "TRUE"
virtualHW.productCompatibility = "hosted"
tools.upgrade.policy = "manual"

tools.remindInstall = "TRUE"

usb.autoConnect.device0 = ""
{% endhighlight%}

* After setting all the paths correctly, if you have VMPlayer installed, just save the vmx file, (call it ubuntu.vmx) and double click on the file.
* If all the paths are set correctly, the VMPlayer will boot up the virtual drive and show the ubuntu installation menu. This is easier than windows a million times.
* At the end of the installation (server or desktop) the process will ask you, if you want to install LAMP server. Select it and let it install the LAMP server.
* Reboot the system, and you are good to go. You have successfully installed Ubuntu on VMWare.

### STAGE II: Check the configuration setup of Apache/MySQL/PHP

Now we'll check if PHP and Apache have been successfully installed on your system. Go the /var/www folder, you should be seeing a apache2-default folder out there. If you see these then apache seems to be installed. Just open the browser and type http://localhost you should be able to see the apache-default folder over there. If you a receive a page not found then apache is not running or installed properly.

If things look good, next stage is to check PHP installation. Create a file named index.php and type the following there.

```
 <?php phpinfo(); ?> 
 ```

Just refresh the localhost (place the file in /var/www) That should give you loads of PHP info on the screen in blue, purple and a huge table. If that happens you are good to go!!! Else something is wrong!!!.

#### MySQL Check
Open the command line and type

```mysql -uroot
```

If it opens up with a mysql> prompt then it's good else something is wrong. Your mysql password is blank.

If all sounds good, now go to Stage III

### STAGE III: Applications to setup.

Download
 * JOOMLA
 * WORDPRESS

Extract them to the `/var/www` folders and access them using [http://localhost/joomla](http://localhost/joomla) and [http://localhost/wordpress](http://localhost/wordpress) respectively if you extracting them to the folders on these names.

How to go about setting them, start the index.php or read the readme file and you should be good to go.