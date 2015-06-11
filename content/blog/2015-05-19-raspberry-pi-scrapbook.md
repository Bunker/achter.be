---
title: Raspberry Pi scrapbook
author: Bunker
type: post
date: 2015-05-19
url: /20150519_raspberry-pi-scrapbook/
categories:
  - Uncategorized
---
I'm trying to setup a sort of internet of things sensor network at home.

For this project I'm using raspberry pi and Arduino boards.

As I already had to start over, I'm going to use this post as a scrapbook:

**Pi setup:**

  1. install Noobs on Raspberry Pi
  2. Select Raspbian as OS
  3. apt-get: 
      * tightvncserver
      * upstart
  4. reboot
  5. this probably gives a weird Login screen, ssh to Pi and chown pi:pi .Xauthority in home dir.
  6. reboot again
  7. apt-get: 
      * arduino
      * python-pip
  8. install adafruit webide
  9. install pyserial: 
      * by downloading latest version (atm 2.7) in tar.gz ->
      * untar -> install with `sudo python setup.py install`
 10. Make startup script for scripts: 
      * doorbell.py

**Startup scripts:**

  * `cd /etc/init`
  * `nano scriptname.conf`
  * copy/paste this code and fill in 
        
        # Program_explanation
        
        description "Your_description"
        author "User"
        
        start on runlevel [2345]
        stop on runlevel [016]
        chdir path_to_dir_with_script
        exec python path_to_script.py
        respawn

  * start script with sudo service scriptname start, it starts every reboot and when it quits it respawns.