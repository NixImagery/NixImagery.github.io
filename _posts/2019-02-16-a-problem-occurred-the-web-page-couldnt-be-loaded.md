---
layout: post
title: A Problem Occurred. The web page couldn’t be loaded.
date: 2019-02-16 13:48:44.000000000 +00:00
# description: 
published: true
img: lubnaig.jpg
fig-caption: Loch Lubnaig 
fig-attrib: by Nick Hood
tags: [networking, OSX]
# permalink: 
---
This message appears in the pop-up dialog when trying to connect to new (mostly public) wifi routers using MacOS Mojave 10.14. I've been resorting to using my phone's personal hotspot but this is no good when there is a poor mobile signal.

The fix is to cancel the dialog, open a browser and navigate to <a href="http://captive.apple.com">http://captive.apple.com</a>. This forces the browser to open the captive login/service page (perhaps after a refresh), allowing a connection to the local wifi. 

Don't forget to connect to your <a href="https://protonvpn.com/">VPN</a>.
