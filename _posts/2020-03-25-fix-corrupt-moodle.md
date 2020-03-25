---
layout: post
title: Fix corrupt Moodle installation
# date: 2019-11-26 20:10
# description: 
img: Harlow.jpg
fig-caption: Harlow water
fig-attrib: Nick Hood
published: true
tags:
- Moodle
- Git
- Linux
# permalink:
---
I wanted to update my Moodle 3.8 installation for the latest security patches but discovered that the repository on my VPS was corrupted. I rather suspect that I had done this myself during a recent ```rsync``` backup, when I had lost patience with a large file and deleted it. I know, stupid is as stupid does. Anyway, Stack Overflow and [Zoey Hewll](https://stackoverflow.com/users/6112457/zoey-hewll) to the rescue. Zoey had posted a really smart way to re-set your .git to match the remote:

```sh
$ mv -v .git .git_old &&            # remove old git
$ git init &&                       # initialise new repo
$ git remote add origin "${url}" && # link to old repo
$ git fetch &&                      # get old history
$ git reset origin/master --mixed   # force update to old history
```
This leaves your working tree intact, and only affects git's bookkeeping.

Zoey's post included [a bash script](https://gist.github.com/Zoybean/8db78966abea5d974934bb0e8e5f4e42) to do this, but I went with typing the git commands above, one step at a time.

Once this was done and my local repository had been unfunged, I had to reset the tracking information to the latest branch, reset it and then pull:

```sh
$ git branch --set-upstream-to=origin/MOODLE_38_STABLE master
$ git reset --hard origin/MOODLE_38_STABLE
$ git pull
```

The last command confirmed there was nothing to do, so the code was recovered and up to date. I could then run the update within the Moodle admin interface OK. 

Thank you, Zoey.