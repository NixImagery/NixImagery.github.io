---
layout: post
title: Connecting to eduroam on Arch
date: 2019-08-22 18:00
# description: 
img: Arch-eduroam.png
# fig-caption: 
# fig-attrib: 
published: true
tags:
- Linux
# permalink:
---
Students on Initial Teacher Education programmes are beginning their studies this week. One of the students asked me to help get her connected to the eduroam academic wireless network. She had got the technical people in the library to look at it and they had got it going by doing some voodoo with a USB stick, but the connection would not re-establish later in the day.

The voodoo was to provide a root Certificate file, downloadable from the [University](https://www.ed.ac.uk/information-services/computing/desktop-personal/wifi-networking/wlan-root-ca), but the wireless configuration app had not imported the certificate as the tech person had evidently assumed it would do. All I had to do was copy the certificate to the student's laptop (an old Acer) and configure the network connection to point to the new location of the file.

The laptop had had its old Windows OS replaced by the student's dad by Arch Linux. Not my first choice for a day to day operating system but the student's dad had done a great job in setting it up with all the apps she needed, and apart from the wireless connection, everything was working sweetly. A classic case for a cheap and sustainable computing solution!