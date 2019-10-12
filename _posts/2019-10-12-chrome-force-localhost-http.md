---
layout: post
title: How to stop Chrome fetching localhost over https
date: 2019-10-12 20:55
# description: 
img: rainbow-cloud.jpg
fig-caption: Rainbow cloud over the Forth
fig-attrib: Nick Hood
published: true
tags:
- Chrome
- http
- Jekyll
- development
# permalink:
---
Whilst developing Jekyll sites locally, the Chrome browser will sometimes try to fetch the page over ```https```, rather than ```http```. This is problematic, because the browser just renders a protocol error:

![screenshot](/assets/img/chrome-https.png)

This is caused by a security policy **HSTS**, or HTTP Strict Transport Security. We have to tell Chrome to forget that it wants to fetch localhost over a secure connection. To do this, visit [chrome://net-internals/#hsts](chrome://net-internals/#hsts) and find the field called **Delete domain security policies**. Enter ```localhost:4000``` (or whatever address you are using for the local jekyll server) and click delete. Chrome will now fetch the site over http again.

Once again, I am grateful to the responses over at [Stack Overflow](https://stackoverflow.com/questions/25277457/google-chrome-redirecting-localhost-to-https). If this doesn't fix your problem then that's the next place you should look.