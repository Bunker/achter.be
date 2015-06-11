+++
author = "Bunker"
categories = ["git", "cheat sheet", "terminal"]
class = "post"
date = "2015-06-11T17:40:37+02:00"
draft = false
tags = ["git", "cheat sheet", "commands", "terminal"]
title = "Terminal: Git commands cheat sheet"
type = "post"

+++
To start a repository from the command line:

```
git init
git add .
git commit -m "initial import"
```

When files are added to .gitignore and are not removed, use following commands and commit.
```
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
```
