---
layout: post
title: get_iplayer broken, version 3.00 available
date: 2017-05-01 07:50:37.000000000 +01:00
# description: 
img: g.png
# fig-caption: 
# fig-attrib: 
published: true
tags:
- BBC iPlayer
- get_iplayer
- perl
# permalink: "/blog/2017/05/01/get_iplayer-broken-version-3-00-available/"
---
For those of us who make use of the amazing <code>get_iplayer</code> program to obtain clips and other resources for classroom and other conveniences, it comes as a bit of a blow to find that in the past week or two, it has stopped working. Fortunately, there is a new version of the program available that with a little effort, gets the facility working again.

From <a href="https://github.com/get-iplayer/get_iplayer/wiki/release300">the release notes</a>:

>The BBC removed all the XML-based data sources used by get_iplayer on 2017-04-26, breaking a lot of get_iplayer functionality. That functionality has been restored, but there are changes to be aware of - get_iplayer has not survived unscathed.

Phil Lewis and the team have (once again) done a fantastic job of quickly responding to changes in the way the BBC delivers its content. Many, many thanks to all the devs and hacks involved in this release.

Finally, my advice to users is to read the release notes carefully. You may also hit issues installing the new dependencies including <a href="http://mojolicious.org/">Mojolicious</a> and Perl as well as the <a href="https://www.cpan.org/">cpan perl repository</a>. Persevere, there is lots of useful advice out there. Finally, finally, the cache updates are much slower than before, although they are now only updated weekly.
