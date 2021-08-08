---
layout: post
title: Jekyll development in zsh
# date: 2019-11-26 20:10
# description: 
img: R0001012.JPG
fig-caption: Culross
fig-attrib: Nick Hood
published: true
tags:
- Jekyll
- zsh
# permalink:
---

A [recent post](/jekyll-update-via-rake) on updating jekyll websites deployed on GitHub describes how this was done on a mac. Apple being Apple, and the advancement of technology being what it is, things have changed slightly such that the workflow needs a slight adjustment.

## zsh

Recent OSX (now called MacOS) updates have changed the default shell programme from the Bourne Again Shell `bash` to the extended version of this, the Z Shell `zsh`. The first impact of this is that the `rake` command (or any command passing square brackets) doesn't work any more:

```bash
% rake publish["Test update"]
zsh: no matches found: publish[Test update]
```
This is simply because `zsh` requires the square bracket characters to be escaped:

```zsh
% rake publish\["Test update"\]
Configuration file: /your/path/to/GitHub/projectname/_config.yml
D	docs/yyyy/mm/dd/some-files.html
....
```

## Two terminals

When developing, I use two terminal windows in the dev folder -- one do do file operations and the like, the other to run a local version of the site while I test. The quick way to get the second window open within your current working directory is to issue this commmand:

```zsh
% open -a Terminal .
```

