---
author: "Bunker"
categories: ["Raspberry pi", "home automation", "install", "tutorial"]
class: "post"
date: "2015-06-10T18:43:54+02:00"
draft: false
tags: ["diy", "tutorial", "home automation", "raspberry pi"]
title: "Openhab install on Raspberry Pi"
type: "post"
---

![Openhab logo][4_img_link]

This post is my guide for installing and configuring [Openhab][openhab_link] on the [Raspberry Pi][raspberry_pi_link]. 

# Install openhab


1. Upgrade and update apt-get
 `sudo apt-get update && sudo apt-get upgrade`

2. do a update of the firmware. These are 2 steps you should always do before installing something new.
  `sudo rpi-update`

3. make directory and download and unzip openhab (get link from [Openhab/downloads][openhab_downloads]). Replace x.x.x in the command below with the version number you copied.
  `sudo mkdir /opt/openhab && cd /opt/openhab/ && sudo wget "get download link" && sudo unzip distribution-x.x.x-runtime.zip && sudo rm distribution-x.x.x-runtime.zip `

4. Download and install bindings for openhab. This installs all possible addons available. Replace x.x.x in the command below with the version number you copied. 
  `cd addons && sudo wget "downloadlink addons" && sudo unzip distribution-x.x.x-addons.zip && sudo rm distribution-x.x.x.-addons.zip`

5. copy the config file and make the startup script executable
  `cd .. && sudo cp configurations/openhab_default.cfg configurations/openhab.cfg && sudo chmod +x start.sh`

6. Edit the config file and start the server.
  `sudo vi openhab.cfg
   sudo ./opt/openhab/start.sh`


[openhab_link]: http://www.openhab.org/
[raspberry_pi_link]: https://www.raspberrypi.org/
[openhab_downloads]: http://www.openhab.org/downloads.html
[4_img_link]: /images/blogposts/openhab-logo.png