---
layout: post
title: Jekyll development in zsh
# date: 2019-11-26 20:10
# description: 
img: Ilford-Delta-3200-20201127_20085880.jpg
fig-caption: Yester Castle
fig-attrib: Nick Hood
published: true
tags:
- Jekyll
- Git
- Rake
# permalink:
---

[Link](/jekyll-update-via-rake)


```sh
$ rake publish["Example updates"]
(in /your/path/to/GitHub/projectname/)
Configuration file: /your/path/to/GitHub/projectname/_config.yml
D	docs/yyyy/mm/dd/some-files.html
....
Reset branch 'master'
Your branch is up to date with 'origin/master'.
[master abcdefg] Example updates
 n files changed, p insertions(+), q deletions(-)
Enumerating objects: r, done.
Counting objects: 100% (nn/nn), done.
Delta compression using up to x threads
Compressing objects: 100% (mm/mm), done.
Writing objects: 100% (mm/mm), 1234 bytes | 123.00 KiB/s, done.
Total mm (delta nn), reused 0 (delta 0)
remote: Resolving deltas: 100% (nn/nn), completed with nn local objects.
To https://github.com/YourGHName/projectname.git
   0aa7f2g..abcdefg  master -> master
Already on 'master'
Your branch is up to date with 'origin/master'.
Finished.
```
Notice a call to publish will also generate the site for you. If you're in a hurry, just issue `rake` to get the default *Commit via Rake* commit message.