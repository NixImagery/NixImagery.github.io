---
layout: post
title: Invalid active developer path after upgrade to Catalana
date: 2019-10-10 14:11
# description: 
img: edinburgh.jpg
fig-caption: Edinburgh from Pettycur Bay
fig-attrib: Nick Hood
published: true
tags:
- OSX
- Catalana
- "10.15"
- git
# permalink:
---
After allowing my MacBook Air to upgrade itself to OSX 10.15 Catalana, git commands throw an error:

```sh
$ git status
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
```

This is because OSX updates remove the developer tools. You need to re-install them (and agree the license again).

```sh
$ xcode-select --install
xcode-select: note: install requested for command line developer tools
```

I am grateful to the contributors on [Stack Exchange](https://apple.stackexchange.com/questions/254380/why-am-i-getting-an-invalid-active-developer-path-when-attempting-to-use-git-a) for the solution to this problem.