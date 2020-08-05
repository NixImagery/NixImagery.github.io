---
layout: post
title: Nextcloud calendar embedding
# date: 2019-06-23 15:42
# description: 
img: nextcloud-calendar.png
fig-caption: Connection refused
# fig-attrib: 
published: true
tags:
- Linux
- Nextcloud
- Content-Security-Policy
# permalink:
---
I needed to embed a [NextCloud](https://nextcloud.com/) calendar within another website. Next cloud offers an embed code block which looks like this:

```html
<iframe width="400" height="215" src="https://your.tld/index.php/apps/calendar/embed/50m3rAnD0mC0d3z"></iframe>
```
Because NextCloud sets some fairly intelligent security defaults, this results in the browser throwing a "refused to connect" error unless the site you embed the calendar iframe on is on the same domain as your NextCloud instance. See the header image for what this looks like.

The solution lies in allowing your target web server to connect to your NextCloud server. This is not done in NginX/Apache settings because these will be overridden by NextCloud anyway. Instead, edit the `ContentSecurityPolicy.php` file for NextCloud. This file is located in the `/lib/public/AppFramework/Http/` folder of your NextCloud installation.

```php
/** @var array Domains from which iframes can be loaded */
	protected $allowedFrameDomains = [
	'https://*.yourdomain.tld',
    ];
    
/** @var array Domains which can embed this Nextcloud instance */
	protected $allowedFrameAncestors = [
		'\'self\'',
    	'https://*.yourdomain.tld',
    ];
```
With the above edits (no server restart required), the calendar will embed quite happily. There is no need to implement the `X-Frame-Options` HTTP header documented elsewhere as this is obsolete. The `Content-Security-Policy` header delivered by the above fix from within NextCloud is enough.