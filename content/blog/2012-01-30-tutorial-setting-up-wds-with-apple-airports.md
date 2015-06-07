---
title: '[Tutorial] Setting up WDS with Apple airports'
author: Bunker
type: post
date: 2012-01-30
url: /20120130_tutorial-setting-up-wds-with-apple-airports/
categories:
  - technology
  - tutorial
tags:
  - airport express
  - airport extreme
  - apple
  - tutorial
---
**UPDATE: in minutes of me posting this tutorial, my airport utility got an update to v6.0 and all I said is obsolete, my WDS network still works, but I don&#8217;t know yet how to set it up correctly.**

[<img src="http://www.achter.be/wp-content/uploads/2012/01/Screen-Shot-2012-01-30-at-11.46.31.png" alt="" title="Airport_admin_utility" width="500"class="alignnone size-full wp-image-197" />][1]

Over here we have a nice setup for our wireless network and playing music in all the rooms of our house. It&#8217;s supported by Apple airports. As you can see in the above screenshot. We use an Airport extreme as the router and 3 Airport expresses as relays. Last saturday evening however, disaster struck and our Airport extreme died. Well it did not die completely, it stopped serving internet through the wifi connections and there was only connection via ethernet connections. The wifi clients however could still connect, authenticate and got an ip-address, but there it all stopped. I tried everything to restore the connections, but despite all my efforts for about 3 hours. Rebooting, resetting, hard resetting nothing worked. So I setup a temporary solution and went out today to get a new Airport extreme.

Let&#8217;s get to the technical part of this article. How do you setup a network of 4 airports across the house on the same network with wpa2 security enabled? The first and most important step is to hard reset all the airports, the only way to do that if the airports don&#8217;t come straight from the box is to hold down the little reset button while pluggin in the airport. If you don&#8217;t know how, check this <a href="http://support.apple.com/kb/ht3728" title="Reset airport" rel="none">support-page</a> on the <a href="http://www.apple.com/" title="Apple website" rel="none">Apple</a>.

### Configure the base station or WDS main

You start by selecting manual configuration in the airport utility, don&#8217;t use the wizard, as you will not be able to setup WDS. On the next screen, you&#8217;ll see a couple of tabs, but none of them shows WDS, at least when you have a recent airport extreme.

  1. Now setup your Base Station like always, fill out the name, choose a password, &#8230; under the Base Station tab.
  2. The next tab is the Wireless tab, this is 1 of the 2 tabs where all the magic will happen.   
    [<img src="http://www.achter.be/wp-content/uploads/2012/01/Screen-Shot-2012-01-30-at-21.35.43.png" alt="" title="Screen Shot 2012-01-30 at 21.35.43" width="500" class="alignnone size-full wp-image-203" />][2]  
    In the dropdown menu next to &#8220;Wireless Mode&#8221; select &#8220;Participate in a WDS network&#8221;, if you don&#8217;t see it, hold down the &#8220;option&#8221; key, it will magically appear.
  3. You setup your network as always, but make sure you select the checkbox &#8220;Allow this network to be extended&#8221;, leave the Radio mode on Automatic, choose WPA/WPA2 Personal, choose a password, go to the Wireless Network Options, set your country and leave all the rest. (_Hint:_ Write down all settings, we&#8217;ll need them later)
  4. Next is the WDS tab, that has appeared after you selected &#8220;Participate in a WDS network&#8221; in the previous step. Select &#8220;WDS main&#8221; in the dropdown from &#8220;WDS Mode&#8221;. Select the checkbox next to &#8220;Allow wireless clients&#8221;.
  
    [<img src="http://www.achter.be/wp-content/uploads/2012/01/Screen-Shot-2012-01-30-at-21.47.50.png" alt="" title="Screen Shot 2012-01-30 at 21.47.50" width="500" class="alignnone size-full wp-image-209" />][3]    
    Fill in the Airport ID&#8217;s of the soon to be remotes, you find the airport ID&#8217;s on the bottom of the airport it should be a string of 12 alphanumeric characters.

That are all the steps for the configuring the base station.

### Configure the WDS remotes

For configuring the remotes, repeat steps 1 till 3 exactly as in configuring the WDS main station. Make sure you have all the wireless settings exactly the same, as for the WDS main station. Make sure you did not miss any setting and if you must choose a channel set it to 11, because otherwise the remote station can&#8217;t connect with the WDS main. 

[<img src="http://www.achter.be/wp-content/uploads/2012/01/Screen-Shot-2012-01-30-at-22.16.46.png" alt="" title="Screen Shot 2012-01-30 at 22.16.46" width="500" class="alignnone size-full wp-image-211" />][4]

To finish the setup, go to the WDS tab and choose for &#8220;WDS remote&#8221; in the drop down next to &#8220;WDS Mode&#8221;. Select the checkbox next to &#8220;Allow wireless clients&#8221; and fill in the Airport ID of the &#8220;WDS main&#8221;, update and test.

Repeat the steps for the airport remote for as many times you need it. You should now be able to use the network and if you activated airplay under &#8220;Music&#8221; you should be able to play music through every airport with boxes or a headphone connected.

A last piece of advice, if you configured a airport and it doesn&#8217;t connect or shows up, put in a ethernet cable so that you can access it again. This will save you a lot of time, because the only other option is hard resetting the airport.

 [1]: http://www.achter.be/wp-content/uploads/2012/01/Screen-Shot-2012-01-30-at-11.46.31.png
 [2]: http://www.achter.be/wp-content/uploads/2012/01/Screen-Shot-2012-01-30-at-21.35.43.png
 [3]: http://www.achter.be/wp-content/uploads/2012/01/Screen-Shot-2012-01-30-at-21.47.50.png
 [4]: http://www.achter.be/wp-content/uploads/2012/01/Screen-Shot-2012-01-30-at-22.16.46.png