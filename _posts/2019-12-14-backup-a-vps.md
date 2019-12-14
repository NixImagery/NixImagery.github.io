---
layout: post
title: Backing up a VPS
date: 2019-12-14 18:40
# description: 
img: forth-bridge.jpg
fig-caption: The Forth Road Bridge
fig-attrib: Nick Hood
published: true
tags:
- VPS
- bash
- rsync
- backup
# permalink:
---
I regularly back up the files on my VPS[^1]. I do this using a script run from the terminal on any convenient machine, usually a MacBook laptop. This is the script:

```sh
#!/bin/bash
[ ! -d ~/Downloads/VPS_rsync ] && mkdir -p ~/Downloads/VPS_rsync
cd ~/Downloads/VPS_rsync
rsync -avz user@server.tld:/path/to/vhosts/ .
date >> VPS_rsync.date
```
The first line tells OSX that what follows is a bash script and should run in the Bourne Again Shell (bash). Next, a folder is created in the current user's download directory, which is then made the current working directory.

The sync command is then issued with a username and the name of the server to be backed up - in this case ```server.tld```, and the directory on the server to be backed up. I am backing up the ```vhosts``` directory which contains all of the files and folders that my VPS serves. The dot at the end of that line tells ```rsync``` to download the data to the current directory. The server will issue a login challenge

The last line of the script prints the current timestamp to a file. Once complete (it can take a while) the files can be relocated to an offline storage.

[^1]:(Virtual Private Server. A rented computer that contains, manages and serves websites and other services on the Internet. Mine is in London.)