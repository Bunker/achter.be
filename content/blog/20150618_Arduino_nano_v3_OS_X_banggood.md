+++
author = "Bunker"
categories = ["Arduino", "Banggood", "OS X", "Yosmite", "ATmega328P Arduino Compatible Nano V3", "CH340G" ]
class = "post"
date = "2015-06-18T10:16:25+02:00"
draft = false
tags = ["CH340G", "ATmega328P Arduino Compatible Nano V3", "OS X Yosmite", "Banggood" ]
title = "Banggood: ATmega328P Arduino Nano V3"
type = "post"

+++

![ATmega328P Arduino Compatible Nano V3][6_img_link]

_This worked at the moment of writing, I can't guarantee it will work for future versions of the boards nor OS X_

**For those just wanting the tutorial, [go here][3_TLDR]**

I while ago I discovered the chinese website [Banggood][1_banggood], which has almost everything you want at low prices. Which is very good for my new arduino hobby.

So next to some other components I ordered the [ATmega328P Arduino Compatible Nano V3 5-pack][2_ATmega328P_nano_5pack] which means I got 5 Arduino nano clones for 15 euro + free shipping, which is just a steal. I have to be honest I was a bit scared to order them, because of all the mixed reviews on the net. On the other hand the max I would loose is 15 euro.

I knew however before ordering that the USB chipset was probably going to require some extra attention.

So once I received the order yesterday, I immediately tried the solutions offered in the comments on Banggood, but I did not manage to get it working. So I turned to google for the rescue. There were several other solutions, but none worked as it should. However the one that got it all working for me was the tutorial of [kiguino][4_kiguino]. 

I'm saying nothing new here, but just because it took me some time on google, I'm reblogging it here, for future reference and maybe help somebody else.

### <a name="TLDR"></a>Tutorial for install on Mac OS X Yosmite (latest test 10.10.3)

1. Download the driver at [the developers website][5_driver_osx] (!! Only the driver from december 2013, works with 10.10)
2. Unzip and install by right clicking and selecting open.
3. Do **NOT** restart yet
4. Open terminal and paste `sudo nvram boot-args="kext-dev-mode=1"`
5. Reboot 
6. The driver should be installed, on my arduino's it installed as /dev/cu.usbserialmodem1410 or /dev/cu.usbserialmodem1420 depending on the port it was connected to and the device I was using.

[1_banggood]: https://www.banggood.com/?p=IH030017233982015060
[2_ATmega328P_nano_5pack]: https://www.banggood.com/5Pcs-ATmega328P-Arduino-Compatible-Nano-V3-Improved-Version-With-USB-p-951782.html?p=IH030017233982015060
[3_TLDR]: #TLDR
[4_kiguino]: http://kiguino.com/2014/12/31/how-to-use-arduino-nano-mini-pro-with-CH340G-on-mac-osx-yosemite.html#continue
[5_driver_osx]: http://www.wch.cn/downloads.php?name=pro&proid=178
[6_img_link]: /images/blogposts/arduino_nano_compatible.jpg