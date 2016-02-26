+++
author = "Bunker"
categories = ['hugo', 'git', 'gandi', 'simple hosting', 'bash scripting', 'github' ]
class = "post"
date = "2016-02-26T22:00:57+01:00"
draft = false
tags = ['hugo', 'git', 'gandi', 'simple hosting', 'bash scripting', 'github' ]
title = "Auto deploy hugo site"
type = "post"

+++

As some of you know, I'm running this site through with the [Hugo][1] site generator. Hugo has many advantages, but one big disadvantage is that to update my site it takes a lot of steps:

1. Write the markdown code
2. Generate the site through hugo
3. Commit the site to github
4. Connect to Gandi simple hosting through sftp and replace all files because all files are seen as new
5. Check permissions after upload

Although only 5 steps this usually takes around 20 minutes to complete.

Earlier this evening I stumbled upon a [blogpost on Gandi cookbook][2] about auto deploy sites through git on gandi simple hosting. I followed their tutorial and added an extra bash script so that now all it takes me is 1 command and a commit message.

To make sure that the info doesn't get lost and for those having using hugo, unix and gandi simple hosting all combined, these are the steps necessary:

## Bash script for automating hugo generation and git commit + push

First let's make a bash script to automate the hugo build and the git commit and push. 

We are using the ability of hugo to have a deploy directory specified, this is because I have my source code also in a git repository and I want my dev code separate from my live code.

create a file in your home dir on your local system. And paste the following code, change the file paths off course.

```
#!/bin/bash
cd FULL_PATH_TO_HUGO_DIRECTORY && \
rm -rf && \
hugo -d "PATH_TO_DEPLOY_DIRECTORY" && \
cd PATH_TO_DEPLOY_DIRECTORY && \
read -p "Commit description: " desc
git add . && \
git add -u && \
git commit -m "$desc" && \
git push
```

Now make a dir ~/bin if it doesn't already exists and copy the script to that directory.

After a reboot or after manually adding the ~/bin path to your ~/.profile you should be able to run the script from everywhere on your system as yourself, however not as root, sudo or another user.

## Auto deploy github to simple hosting

* Create a simple hosting instance, I had already one PHP/MYSQL version
* Go to the admin panel and activate ssh access in your simple hosting
* Connect to your ssh and navigate to the htdocs of the vhost you want to auto deploy

<code>cd /srv/data/web/vhosts/[replace with your vhost]/htdocs</code>

* Remove all existing files, make sure you have a backup if the instance is not new

```rm -rf *```


* Clone your github repository use the dot at the end of the line, to make sure the repository gets cloned without making a subdirectory

```git clone https://github.com/[username]/[repositoryname].git .```


* Check that the files are there

```ls -la```

* Make a php file with the following content, I named it pull.php

```nano pull.php```

* paste the following code in there

```<?php
`git pull`;                         // This will execute the `git pull` command on your instanceheader
("Cache-Control: max-age=1"); // Lower the cache while we're here so the changes take effect faster
echo "hello!";                      // So you can confirm the file is in the right place by browsing to the URL
?>```

* Make the php file executable

```chmod +x pull.php```

* Check if the file works by browsing to its URL, [domain]/pull.php
* Go to the settings of your github repository and select webhooks and services
* Create a new webhook, where you paste the url of the pull.php, leave all other settings at default
* Do an update to check if it works

*DISCLAIMER*: For me it all works very well, but don't change any of the files on the simple hosting without using git or you will have to restart the procedure.

[1]: http://gohugo.io
[2]: http://gnadi-cookbook.readthedocs.org/en/latest/paas/auto-git-deployment.html
