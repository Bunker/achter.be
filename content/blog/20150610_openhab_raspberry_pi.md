---
author: "Bunker"
categories: ["Raspberry pi", "home automation", "install", "tutorial", "openhab"]
class: "post"
date: "2015-06-10T18:43:54+02:00"
draft: false
tags: ["diy", "tutorial", "home automation", "raspberry pi", "openhab"]
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
  `sudo nano openhab.cfg
   sudo ./opt/openhab/start.sh`

7. Make a startup item with screen, so that you can always access the OSGI console.

   `sudo nano /etc/init.d/openhab`
   
8.  Paste following code in there on line 14 change the user to your openhab user:

   `#! /bin/sh
	### BEGIN INIT INFO
	# Provides:   openHAB
	# Required-Start: $local_fs $remote_fs
	# Required-Stop:  $local_fs $remote_fs
	# Should-Start:   $network
	# Should-Stop:    $network
	# Default-Start:  2 3 4 5
	# Default-Stop:   0 1 6
	# Short-Description:    Start and stop openHAB in screen Session
	# Description:    This runs openHAB continuously in screen.
	### END INIT INFO
	# Set OH-User
	OHUSER=openhab
	# Set OH-Path
	OHPATH=/opt/openhab

	case "$1" in

	  start)
	        PID=`ps -ef | grep openHAB | grep -v grep | awk '{print $2}'`
	        if [ "${PID}" != "" ]
	         then
	          echo openHAB-Screen is already open, use: sudo -u openhab screen -r `pidof SCREEN`
	         else
	          echo "Starting openHAB"
	          cd ${OHPATH}
	          sudo -u ${OHUSER} screen -S openHAB -dm  sh ./start.sh
	        fi
	        ;;
	  stop)
	        echo "Stopping openHAB"
	        sudo -u ${OHUSER} screen -S openHAB -p 0 -X stuff "exit$(printf \\r)"
	        sudo -u ${OHUSER} screen -S openHAB -p 0 -X stuff "y$(printf \\r)"
	        sudo -u ${OHUSER} screen -S openHAB -p 0 -X stuff "exit$(printf \\r)"
	        PID=`ps -ef | grep openHAB | grep -v grep | awk '{print $2}'`
	        while [ `ps -ef | grep $PID | wc -l` -gt 1 ]
	         do
	          echo -n .
	          sleep 2
	         done
	        echo .
	        ;;
	  restart|force-reload)
	        echo "Restarting openHAB"
	        $0 stop
	        $0 start
	        ;;
	  *)
	        N=/etc/init.d/$NAME
	        echo "Usage: $N {start|stop|restart}" >&2
	        exit 1
	        ;;
	esac
	exit 0`
9.  Make the script executable and configure to run on boot
	
	`sudo chmod a+x /etc/init.d/openhab
	sudo update-rc.d openhab defaults`
	
	Whenever you want to use the OSGI console, just type
	
	`screen -x` and to leave the screen you do `ctrl+a d`
	
10. Normally your server should run now and you should be able to access the demo content through:
 	
	`http://<openHAB server ip>:8080/openhab.app?sitemap=demo`


[openhab_link]: http://www.openhab.org/
[raspberry_pi_link]: https://www.raspberrypi.org/
[openhab_downloads]: http://www.openhab.org/downloads.html
[4_img_link]: /images/blogposts/openhab-logo.png