---
layout: post
title: Rename Image Files in Folders
date: 2018-08-14 10:27:57.000000000 +01:00
# description: 
published: true
img: Screenshot-2019-06-21.png
fig-caption: Files
fig-attrib: by Nick
tags: [Python]
# permalink: "/blog/2018/08/14/rename-image-files-in-folders/"
---
This is a Python script to walk a directory tree, renaming .jpg and .JPG files. It was written for a client who had a directory containing multiple directories, each containing zero or more (up to 100) image files. Most of the images were named &lt;abitrary name 1&gt;.jpg or &lt;arbitrary name 2&gt;.JPG.

The client wanted each folder's images to be numbered 001.jpg to nnn.jpg for some further process.

```py
import os
import imghdr

def renamefiles(path):
rootstructure=os.path.abspath(path)
n = 0
for root, dirs, files in os.walk(rootstructure):
for f in files:
if os.getcwd() != root:
n = 0 # Reset the counter
os.chdir(root)

type = imghdr.what(f)
if type == 'jpeg':
n +=1
os.rename(f, str(n).zfill(3) + ".jpg")

# Specify the full path to the directory here.
renamefiles("/Users/myuser/Desktop/TheImageFolder")</pre>
```