---
layout: post
title: Grav Error 403 in Admin Panel
date: 2018-08-07 10:15:02.000000000 +01:00
# description: 
published: true
img: sky.jpg
fig-caption: Skye
fig-attrib: by Nick
tags: [Software]
# permalink: "/blog/2018/08/07/grav-error-403-in-admin-panel/"
---
I'm trying out [Grav](https://getgrav.org/), a flat file CMS, on my server. It looks promising, having just [installed it](https://photo.cullaloe.net/) with the admin plugin. It seems that there is a fairly [well-known problem](https://github.com/getgrav/grav-plugin-admin/issues/979) with false positives from apache's mod security web application firewall software, which manifests as an annoying 403 error banner in the admin pages (and the notifications panel not loading).

This is easily fixed by whitelisting [mod security rule 350147](https://wiki.atomicorp.com/wiki/index.php/WAF_350147). In Plesk, mod security rules can be whitelisted in the **Server Management** \| **Tools and Settings** \| **Security** \| **Web Application Firewall (ModSecurity)** page. Enter the security rule ID (in this case 350147) in the box at the end of the page and click apply.

There is a security risk associated with this and users should assess the risk to their servers before implementing this workaround.
