---
layout: post
title: Chicago author-date with ibid
date: 2022-03-23
# description: 
img: DSF8831.jpg
fig-caption: Glendevon
fig-attrib: Nick Hood
published: true
katex: yes
tags:
- CSL
- PhD
- Mendeley
- Software
- Writing
# permalink: 
---

One of my supervisors recently suggested:

> "Just a stylistic thing going forward, but where you have recently cited the same author, you can use Ibid (e.g. (Ibid: 2) or similar), rather than include their names again"

This is great advice and something I had seen before. I use [Mendeley Desktop](https://www.mendeley.com/DOWNLOAD-DESKTOP/) as my academic library and reference manager, which plays nicely with my [writing workflow](/phd-workflow-22). I am used to using the so-called "Harvard" citation style, otherwise known as "author-date" because it looks like this: {% cite bresson1999the %} but had not worked out how to have the software automatically detect when *ibid.* is appropriate. 

The key to it is in the [citation style](https://citationstyles.org/) or `.csl` file that tells your typesetting program how to format citations. There are thousands of these, publicly accessible over at the [Zotero Style Repository](https://www.zotero.org/styles) or [Github](https://github.com/citation-style-language/styles). I wanted to use a popular `csl` style using the globally recognised [Chicago Style Manual](https://www.chicagomanualofstyle.org/) but the use of *ibid* has been deprecated there. They favour the use of a short form citation which is well suited to the numbered footnote alternative to author-date.

With a little leg work I found that it is quite easy to adapt [the current Chicago author-date](https://www.zotero.org/styles/chicago-author-date) `.csl` file to include the *ibid* feature from [its numbered footnote sister](https://www.zotero.org/styles/chicago-note-bibliography-with-ibid).

## The adaptation

Starting with a copy of the author-date `.csl` file (obviously change the name), find the `<citation>` tag and merge the equivalent code from the fullnote with ibid `.csl` file. It should look like this:

```xml
<citation et-al-min="4" et-al-use-first="1" disambiguate-add-year-suffix="true" disambiguate-add-names="true" disambiguate-add-givenname="true" givenname-disambiguation-rule="primary-name" collapse="year" after-collapse-delimiter="; ">
    <layout prefix="(" suffix=")" delimiter="; ">
      <group delimiter=", ">
        <choose>
        <if position="ibid-with-locator">
          <group delimiter=", ">
            <text term="ibid"/>
            <text macro="point-locators-subsequent"/>
          </group>
        </if>
        <else-if position="ibid">
          <text term="ibid"/>
        </else-if>
        <else>
            <group delimiter=", ">
              <text macro="contributors-short"/>
              <text macro="date-in-text"/>
              <text macro="point-locators"/>
            </group>
        </else>
        </choose>
      </group>
    </layout>
</citation>
```
It is also necessary to pull in the `point-locators-subsequent` macro. Paste it below the other macros in the `.csl` file. 

## Usage

All that is required now is to point the rendering software to the style file, in my case, by editing the `yaml` header in my markdown document, or the `_config.yml` file for this site.

I don't feel that I should push this back to the open source repositories because it's just my own hack that works for me, but you can download my version of [chicago-author-date-with-ibid.csl](/assets/docs/chicago-author-date-with-ibid.csl) to adapt for your own use.

## References

{% bibliography --cited %}