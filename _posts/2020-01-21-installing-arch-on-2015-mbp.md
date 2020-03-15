---
layout: post
title: Installing Arch Linux on a 2015 MacBook Pro
# date: 2019-11-26 20:10
# description: 
img: durham.jpg
fig-caption: Durham
fig-attrib: Nick Hood
published: false
tags:
- Linux
# permalink:
---
I have one of those old MacBook Pro laptops laying about that I have tried to revive with various flavours of Linux. Here, I describe how I put Arch Linux on it for development and experimentation.

## Sticking Arch on a Stick
On a current OSX machine, I downloaded the [current Arch](https://www.archlinux.org/download/) iso image from one of the UK mirrors. Of course I checked the integrity with the hash file.

Next, I followed [Gerhard](https://blog.tinned-software.net/create-bootable-usb-stick-from-iso-in-mac-os-x/)'s helpful guide on transferring this to an unused 8GiB USB stick. The ```dd``` command failed with permission denied first time, but worked OK prepending ```sudo```.

## Booting
Insert the USB stick into the laptop and power up, holding down the ```alt``` key. Select the applicable EFI Boot option when the Apple boot manager appears.

