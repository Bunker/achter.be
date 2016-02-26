+++
author = "Bunker"
categories = ["raspberry pi", "backup", "arch linux", "rsync", "linux", "Synology"]
class = "post"
date = "2015-11-11T20:10:19+01:00"
draft = true
tags = ["raspberry pi", "backup", "arch linux", "rsync", "linux", "Synology"]
title = "Synology to Raspberry Pi off site backup"
type = "post"

+++
## Purpose

As a photographer I have quite a large collection of data that I would prefer not to loose, at the moment we are talking about 5TB of data. I have an archive on a synology NAS, with a Synology raid with 1 disk failure protection.

This is nice, but not enough, to ensure my clients that I always have an backup of their photos, I wanted an off site backup. 

I tried [Crashplan][1], although not bad if you just want to backup your computer, but definitely not an option for large volumes.

So I starting thinking of the following:

* Full backup of at least 5TB and easily expandable
* Near instant (crashplan has only managed to backup 37% after 1 year)
* Automatic and at least once a day
* Install and forgot principle (crashplan on synology needed my attention on average every 2 weeks)
* Off site
* About 70 euro a year to maintain (which is what my crashplan costs)

As I have a darkroom in the garden that's at least 25m away from the house, but has a wired ethernet connection. I figured if I installed a Raspberry Pi with external drives over there, I'm pretty well protected against almost everything including: 

* Fire
* Flood
* Theft
* Power surges, as the Darkroom has it's own separate ground connection
* ...

However as a colleague pointed out I'm not protected in case of a lighting strike. I'm currently figuring out if I want to replicate this setup at my parents place so that I have another layer of redundancy.  


## Hardware

* 1 Raspberry pi 2 model B + power supply
* 1 sd-card minimum 2gb (I used a 4gb)
* 1 usb-stick min. 2gb (I used a spare 8gb)
* USB external HD (I used 2x3TB seagate backup plus)
* ethernet connection
* A synology system to backup

## Software

1. [Arch Linux][a1]
2. [Avahi][a2]
3. [Boot from USB][a3]

### 1. Arch Linux

I followed the official install procedure for RPI on the [Arch Linux wiki][2]. I used a card reader on another RPI to install and format the card.

For basic setup and config I followed [this guide from elinux.org][3]

### 2. Avahi

For the install of Avahi which makes for easy to remember access through a hostname, I followed [Vlad's tutorial][4]

### 3. Boot arch linux from USB

For booting for the usb we are using my own guide from my [previous blogpost][5]

### 4. Setting up the drives

partition
format
/etc/fstab UUID
permissions

http://gleenders.blogspot.be/2014/03/raspberry-pi-resizing-sd-card-root.html

### 5. Synology rsync script

SSH Keys
see http://www.vdsar.net/rsync-backup-synology-remote-raspberry-pi/
fix errors:
http://blog.pezcuckow.com/post/28763933464/rsync-permission-denied-13

### 6. Schedule Task on synology

commandline task scheduler shows if your script has an error

### 7. Test backup


### 8. Some tips and debugging

It can be useful to know the following things to help debugging:

1. first try to run the script from the console by typing:

    . /path/to/your/script/Rsyncscript.sh

this should give you error messages when something is not correct with the script

2. When you have a space in either source path, do the following to make the script work

in the line with rsync 

    rsync ... Exclude.txt "$SRC" "$DEST" >> $LOGFILE

3. When you get these type of errors:

    rsync: recv_generator: mkdir "" failed: Permission denied (13)

change the options to the following for your rsync command:

-avR --no-p --no-g --chmod=ugo=rwX





[a1]: #arch-linux
[a2]: #avahi
[a3]: #boot-from-usb

[1]: http://www.crashplan.com
[2]: http://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2
[3]: http://elinux.org/ArchLinux_Install_Guide
[4]: http://dovgalecs.com/blog/arch-linux-zeroconf-service-discovery-a-la-bonjour/
[5]: /blog/20151111_Arch_linux_boot_usb


