---
layout: post
title: OSX Finder stuck in loop
date: 2019-10-25 08:55
# description: 
img: dunkeld.jpg
fig-caption: The Tay at Dunkeld
fig-attrib: Nick Hood
published: true
tags:
- OSX
# permalink:
---
I keep quite a lot of folders on my desktop - keeping the current work in view, and offloading completed projects rather than have them hanging about my laptop.

It seems that the Mac OSX desktop can be sensitive to what's on the desktop, which can cause the Finder app to get itself in a loop of locking up (wheel of death) and then crashing (or forced relaunch), only to repeat the cycle. This is frustrating for the user. Restarting the computer does not solve the problem.

A way to exit this is to move all of the desktop files to a new temporary location:

```sh
$ sudo mkdir /Users/username/Documents/tempfolder
$ sudo mv /Users/username/Desktop/* /Users/username/Documents/tempfolder
```

Here, ```username``` should be replaced with the affected account's username. This can be done from another logged in user's account but I was able to perform these commands from my usual account. Having restarted to allow Finder to get over its crisis, I was able to move them back again (drag 'n' drop) and delete the temporary folder without the problem recurring.

```sh
$ sudo rm -rf tempfolder
```
There's a useful thread with more details on possible causes over at [MacWorld](http://hints.macworld.com/article.php?story=20060308010111601).
