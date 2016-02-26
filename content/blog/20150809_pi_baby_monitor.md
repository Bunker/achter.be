+++
author = "Bunker"
categories = ["raspberry pi", "mumble", "mjpeg", "motion", "baby-monitor", "babyPi"]
class = "post"
date = "2015-08-08T08:02:44+02:00"
draft = true
tags = ["raspberry pi", "mumble", "mjpeg", "motion", "baby-monitor", "babyPi"]
title = "20150809_pi_baby_monitor"
type = "post"

+++

Since a 2 weeks I'm the proud father of a daughter. As every baby she needs a baby monitor. I'm a geek, so I was looking for the perfect baby-monitor. First I was amazed by the price of those devices. The most simple one starts at 49 euro and one that comes close to what I would want/need is about 200-300 euro. So I when a little while ago I started playing with the [Raspberry pi][1] I quickly realised I can make my own baby-monitor. 

Me and my girlfriend had some requirements for a baby monitor:

* reachable from the bottom of our garden
* near instant sound
* video possibility, but not necessary to see it all the time
* no extra device to carry around/charge
* not to many wires
* able to move it to other locations

I went out to see if nobody else had done that before and low and behold of course there were other people that made one already. I found several solutions with Darkice and icecast or ffmpeg and so on. I started playing around with those solutions, but they all had quite a big delay. 

Then I found the [PiFM][2] project and because everybody said it was that easy to get it working I thought I'd give it a try. However there was no mention of it not working at all on a Raspiberry 2 model B. Once you start investigating any further you quickly find out, that there are several problems with it:

1. It's highly illegal to send out signals on the FM-band without a proper license
2. It creates loads of interference on other bands then the FM band, especially traffic control, emergency and armed forces reserved bands.
	* which is not a good idea, as I'm living near a military airbase. 
3. It's simply doesn't work on the RPI 2 Model B, the developers don't have an intention of porting it to RPI 2

[TODO: actual install]

Install raspbian jessie with gui.
boot from usb
configure wireless (edimax EW7811-un)
shrink raspbian install to fit on 4gb usb-stick

### Install X11VNC

install x11vnc to run vnc on display 0, so you can run headless

see https://melgrubb.wordpress.com/2014/08/01/raspberry-pi-home-server-part-5-remote-desktop/


### Mumble-server

[TODO: config and automatisation]

https://sharpygoesoff.wordpress.com/2013/05/20/setting-up-a-mumble-server-on-a-raspberry-pi/

### Mumble

    sudo apt-get install mumble

configure mumble via vnc

### Motion

    sudo apt-get install motion

config file


## Install in Polaroid camera

[TODO: show and explain the integration of the case]
