---
layout: post
title: Deploying a Bookdown site securely
# date: 2019-11-26 20:10
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
I set up a specific domain `static.cullaloe.net` for this project, and secured it with an SSL certificate. Within Plesk, the root folder of the domain is made a password-protected directory. This hides the source files. 

## The files
In the domain root, clone the GitHub repository into a new folder (in this example, both the repository and the local folder are called "foobar"):

```sh
$ git clone https://github.com/githubuser/foobar.git foobar
```

It is not necessary to specify the target directory, you'll get that as default. It is not possible[^afaik] to selectively clone a github project: it's all or nothing. `foobar` now contains all of the source files of the project.

[^afaik]: As far as I know, anyway.

## The folder
Now, in Plesk, it's just a matter of sharing the `docs` folder by making it password-protected with a (different) username and password to share with colleagues, along with a link to the documentation, in this example, `static.cullaloe.net/foobar/docs`.

## Outcome
I can easily continue to work on my project documentation, updating it from time to time for colleagues who are interested in seeing what I'm doing. I make (neurotic) use of github for configuration management and safekeeping of all my hard work anyway, so updating the site just requires ```$ git pull``` from the repository folder on the web server. They can then view the documentation in a browser, or download a pdf or docx that is up-to-date with my current progress.

## Notes