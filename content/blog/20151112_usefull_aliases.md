+++
author = "Bunker"
categories = ['linux', 'mac os x', 'alias', 'shortcut' ]
class = "post"
date = "2015-11-12T12:33:04+01:00"
draft = false
tags = ['linux', 'mac os x', 'alias', 'shortcut']
title = "Unix/OS X aliases I use frequently"
type = "post"

+++

This is a list of aliases I like to use on either Mac OS X and/or Linux.

add them in ~/.bash_profile to use over reboots.

* set ls -all to la
```alias la='ls -all'```
* Built in Raspberry pi temperature check
```alias checktemp='/opt/vc/bin/vcgencmd measure_temp'```
* Check your external IP through icanhazip.com
```alias ip='curl icanhazip.com'```
* Check your external IP details through icanhazip.com
```alias iplookup='echo $(curl -s ipinfo.io/$(curl -s icanhazip.com))'```
* Directly go to my dropbox folder on OS X
```alias dropbox='cd /Volumes/Macintosh\ HD/Dropbox/'```


