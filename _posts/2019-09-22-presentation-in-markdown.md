---
layout: post
title: Presentations in Markdown
date: 2019-09-22 13:38
# description: 
img: _DSF5635-Sep 12 2019.jpg
fig-caption: Rumbling Bridge flowers
fig-attrib: Nick Hood
published: true
tags:
- pandoc
- beamer
- presentations
- Latex
# permalink:
---
I have needed a way to make a quick presentation that does not require the use of huge complex programs like PowerPoint or KeyNote. One way I have been using recently is to write the outline in markdown (as I would when sketching out a lesson plan) and then using the amazing pandoc to magic up a pdf. Here are the key elements of your markdown file and how to produce one for yourself.

## YAML Header

```ruby
---
title: Example
author: Nick Hood
date: "22nd September 2019"
classoption: "aspectratio=169"
---
```

## The presentation
The slide heading level is determined by the first heading that is followed by content. Any headings above that will be treated as section header slides.

Any references can be automatically expanded into a list at the end of the final slide. 

```
## Bullets and links

* First [Link](https://cullaloe.net)!
* No link
* Bullet

# Q & A

## References
```

## How to make the presentation
```bash
$ pandoc -t beamer Example.md -o Example.pdf \
    --bibliography="/path/to/bibliography.bib"
```
* add ```-V theme:Pittsburgh``` for non-default themes
* add ```-V colortheme:beaver``` for non-default colours
* add ```-V fonttheme:professionalfonts``` for non-default fonts
* Themes, etc. are [online](http://www.deic.uab.es/~iblanes/beamer_gallery/index_by_theme.html)

Have fun.