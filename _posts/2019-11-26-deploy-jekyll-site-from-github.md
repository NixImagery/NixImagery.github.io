---
layout: post
title: Deploying a Jekyll site from GitHub
# date: 2019-11-26 20:10
# description: 
img: pattiesmuir.jpg
fig-caption: Pattiesmuir in the frost
fig-attrib: Nick Hood
published: true
tags:
- VPS
- Jekyll
- GitHub
- deployment
# permalink:
---
I've been building a site using Jekyll and hosting the code on GitHub. The site is available on GitHub pages from the ```docs``` folder in the ```master```branch, but I wanted to deploy it to a server running Centos and Apache.

On the VPS, from behind the ```httpdocs``` or web-facing folder, clone the GitHub repository into a new folder (in his example, both the repository and the local folder are called "foobar"):

```sh
$ git clone https://github.com/githubuser/foobar.git foobar
```

Now we need to serve the site files from the docs folder in the repository. Include this in the Apache/Nginx configuration:

```apache
Alias /foobar /var/www/vhosts/thesite/foobar/docs
```

Updating the site just requires ```$ git pull``` from the repository folder on the web server. Depending on how you are logged in to the server, you may need to change the folder permissions so Apache can serve the pages and find the css, etc.
