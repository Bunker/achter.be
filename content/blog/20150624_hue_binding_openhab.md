+++
author = "Bunker"
categories = ["Raspberry pi", "home automation", "install", "tutorial", "openhab", "Philips Hue"]
class = "post"
date = "2015-06-24T00:48:02+02:00"
draft = true
tags = ["Raspberry pi", "home automation", "install", "tutorial", "openhab", "Philips Hue"]
title = "[OpenHab] Philips Hue install"
type = "post"

+++

1. Install the openhab binding in the /opt/openhab/addons (if you followed the steps in [my previous tutorial][1], you have all bindings already)

2. Restart the openhab server with osgi console (again see previous [tutorial][1])

`sudo service openhab restart`

3. Watch the output in the OSGI console, because openhab will give you 100 seconds to push the button on your Hue controller to make a successful connection. You should normally only do this once.

4. Start configuring your items: (whenever I use [openhab_env], please use name of your openhab enviroment)
	`cd /opt/openhab/configurations/items
	nano [openhab_env].items`

	add the following lines to the item file
	
	`Group:Switch:OR(ON,OFF) Lights  "All Lights [(%d)]"     (All)
	Color   Light_GF_TV     "TV light"      <hue>   (GF_Living,Lights)              { hue="1" }
	Color   Light_FF_Office "Office Light"  <hue>   (FF_Office,Lights)              { hue="2" }`
		
	The first line defines all lights into on trigger, so that you can turn them all off at once.
	
	

[1]: /blog/20150610_openhab_raspberry_pi/