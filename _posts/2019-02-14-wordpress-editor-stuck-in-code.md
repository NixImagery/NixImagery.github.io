---
layout: post
title: Wordpress editor stuck in code
date: 2019-02-14 15:58:21.000000000 +00:00
# description: 
published: true
img: analogies.png
# fig-caption: Analogies
# fig-attrib: xkcd
tags: [WordPress]
# permalink: 
---
The new Wordpress editor, Gutenberg, has had a mixed reception. For users that are only occasional editors on a site, it can be a pain to get to grips with, especially as the implementation is still quite buggy.

One of my clients tried to add a post to a site he hadn't contributed to for some time and ran straight into a difficulty: the visual editor wasn't working for him at all. His view should have been this:

![should](/assets/img/Screenshot-2019-02-14-at-16.06.03.png)

...but what he got instead was this:

![did](/assets/img/Screenshot-2019-02-14-at-16.07.36.png)

In other words, his interface was stuck in the code editor. Unfortunately, he had no way of changing this (and neither did I as admin) in the UI. We changed a lot of variables, suspecting first his browser choice (Edge) and then OS choice (Windows). Long story short, the fix is to add an entry into the user's meta table setting the rich_editing variable true.

```sql
INSERT INTO `wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`) VALUES (NULL, '999', 'rich_editing', 'true')
```