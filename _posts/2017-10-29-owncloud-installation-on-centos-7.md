---
layout: post
title: ownCloud installation on Centos 7
date: 2017-10-29 21:12:09.000000000 +00:00
# description: 
img: cloud.jpg
fig-caption: Cramond
# fig-attrib: 
published: true
tags:
- Linux
# permalink: "/blog/2017/10/29/owncloud-installation-on-centos-7/"
---
For some time, I've wanted to have a calendaring tool independent of Google Calendar, which has become a central tool to my productivity and a source of concern as to how much data profiling results from it.

This afternoon, I installed the open source ownCloud file storage, calendar and contacts suite on my Centos VPS. It was a straightforward exercise:

* Create a subdomain on the server and switch it to use PHP 5.6. Add **/dev/urandom** to **open_basedir** in php settings.
* Make a data folder behind the web root, chowned to the web user.
* Create a MySQL database for the ownCloud service.
* In the web root folder, get the software:  
`curl -O https://download.owncloud.org/community/owncloud-10.0.3.tar.bz2`
* Check the MD5 hash, chown and extract. Copy the extracted files into the root folder  
(be careful to include dotfiles, e.g. `cp owncloud/* .` and `cp owncloud/.* .`
* Visit the domain to configure the installation.

What this server now provides is an independent calendar service, contacts, and secure file storage, at no additional cost and under my own secure control.
