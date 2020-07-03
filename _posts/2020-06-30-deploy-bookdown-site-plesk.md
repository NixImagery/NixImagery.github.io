---
layout: post
title: Deploying a Bookdown site securely
date: 2020-07-03 09:10
# description: 
img: R0000570.JPG
fig-caption: Braefoot Bay
fig-attrib: Nick Hood
published: true
tags:
- R
- Linux
- Git
- Bookdown
# permalink:
---
I have been writing documentation for a project in markdown using [RStudio](https://rstudio.com/), which provides a nice way of packaging it all as a static (html) website. I wanted to share this work with colleagues securely.

## Writing workflow
The documents exist within an RStudio project and are built to a folder containing static files. That folder is by default `_book`,  but I change this to `docs` to make it easy to deploy as a github site if I wish[^how]. Configuration management is a crucial element to proper productivity, not just in software but also in all walks of life where documentation is important. Because of this, I use [github](https://github.com/) to store my work safely, should I lose a laptop or suffer some other first-world calamity. It's one of the reasons I use markdown when writing: configuration management is well-suited to text-based documents because it is easy to track and manage changes.

Although I keep the source files on github, I haven't published this project to github pages because it should not be publicly available: instead, I deploy to a VPS (Centos/Apache/Plesk), putting it all behind a login.

[^how]: In `bookdown.yml`, add the line `output_dir: "docs"`.

## The domain
I set up a specific domain `static.cullaloe.net` for this project, and secured it with an SSL certificate. 

## The files
Clone the GitHub repository into a new folder somewhere behind the web-facing directory (i.e. not in *httpdocs*). In this example, both the repository and the local folder are called "foobar":

```sh
$ git clone https://github.com/githubuser/foobar.git /var/www/vhosts/[domain]
```

It is not necessary to specify the target directory, you'll get that as default. It is not possible[^afaik] to selectively clone a github project: it's all or nothing. `/var/www/vhosts/[domain]/foobar` now contains all of the source files of the project.

[^afaik]: As far as I know, anyway.

## Permissions
You need to create a `.htpasswd` file in the server somewhere, containing the username and password you wish to grant access to your files to:

```bash
$ /path/to/htpasswd -c /var/www/vhosts/[domain]/.htaccess user1
```
This prompts you for the password you wish to set for this user. Adding another user is the same command without the `-c` option.

## The server
You need to tell the Apache, using `Alias`, where to find the files, and with `<Location>`, control who can access files at the URL you are trying to protect. In the Plesk control panel, *Apache & nginx Settings for static.cullaloe.net ···*:

```
Alias /foobar /var/www/vhosts/[domain]/foobar/docs
<Location /foobar>
	AuthType Basic
	AuthName "Restricted access"
	AuthUserFile /var/www/vhosts/[domain]/.htpasswd
	Require user user1
</Location>
```

## Outcome
I can easily continue to work on my project documentation, updating it from time to time for colleagues who are interested in seeing what I'm doing. I make (neurotic) use of github for configuration management and safekeeping of all my hard work anyway, so updating the site just requires ```$ git pull``` from the repository folder on the web server. They can then view the documentation in a browser, or download a pdf or docx that is up-to-date with my current progress.

## Notes