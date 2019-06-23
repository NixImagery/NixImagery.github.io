---
layout: post
title: Pro Git and more MX DNS
date: 2013-09-15 13:15:38.000000000 +01:00
# description: 
img: bridge.jpg
# fig-caption: 
# fig-attrib: 
published: true
tags:
- DNS
- Git
- Linux
- MX
- OSX
- Plesk
- VPS
# permalink: "/blog/2013/09/15/pro-git-and-more-mx-dns/"
---
Continuing the summer of code into the early autumn, I have been developing, enhancing and debugging the new server. New and migrated sites are stable and responding well within the resource limits I've chosen of 10GB disk, 50GB traffic (although we're close to whacking this one) and 256/512 MB RAM/Swap space. Uptime has been 100% for over 60 days now.

Within the suite of services running on the server are database, web server, CGI, mail, stats and monitoring. What is not, is the DNS service, which I have learned to keep in a different place, with the registrar. Setting up reverse DNS for the mail service to work correctly is important: I discovered that one client had been having difficulties receiving mail from just one of his friends. This was because the MX DNS entry for his domain pointed to an IP address which some service providers will reject as it doesn't comply with the RFC. Changing it to the host domain of the server's IP, however, stopped all mail getting through to the client. This was finally resolved by pointing the MX record for the domain to the domain itself:

```
example.com. A     192.0.2.1
@            MX 10 example.com.
```

If you want to know how the Internet works, by the way, a really good place to start is the Internet Engineering Task Force (IETF). They have a good introduction [here](https://ietf.org/tao.html). Many internet standards are defined in RFC documents.

Other services on the server operate as database-driven php suites such as the Wordpress CMS, Moodle, LimeSurvey or phpBB. All of these are subject to modifications, code hacks and tweaks to make them work to the needs of the site owner. Whilst the Parallels Plesk Panel allows install-at-a-click for many application suites, I prefer to manage the installation and customisation of these myself. Until now, I had used the download-unzip-upload over FTP method but I'm going to try using the more elegant command-line facility offered by Git. I'm getting started by using their [excellent online documentation](http://git-scm.com/book). This should allow me a much faster update route and potentially a way to be a better contributor to open source than the consumer I have been.
