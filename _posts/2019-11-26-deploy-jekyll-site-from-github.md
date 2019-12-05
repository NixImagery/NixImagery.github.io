---
layout: post
title: Deploying a Jekyll site from GitHub
date: 2019-11-26 20:10
# description: 
img: pattiesmuir.jpg
fig-caption: Pattiesmuir in the frost
fig-attrib: Nick Hood
published: false
tags:
- VPS
- Jekyll
- GitHub
- deployment
# permalink:
---
I've been building a site using Jekyll and hosting the code on GitHub. The site is available on GitHub pages from the ```docs``` folder in the ```master```branch, but I wanted to deploy it to a server running Centos and Apache.

On the VPS, from the ```httpdocs``` folder, clone the GitHub repository into a new folder (here, called "mysite"):

```sh
$ git clone https://github.com/<githubuser>/<repository>.git <mysite>
```
You'll need to change the folder permissions so Apache can serve the pages and find the css, etc:

```sh
$ cd mysite
$ chown -R webserver:webserver docs
```
Now we need to redirect the server requests to the docs directory by creating ```.htaccess``` with these redirects:

```sh
RewriteRule ^subdirectory/(.*)$ /anotherdirectory/$1 [R=301,L]
```