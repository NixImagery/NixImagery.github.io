---
layout: post
title: Zettelkasten, or connecting ideas
date: 2022-06-09
# description: 
img: DSF9026.jpg
fig-caption: Sur la plage
fig-attrib: Nick Hood
published: true
katex: yes
tags:
- Markdown
- PhD
- CPD
- Data
- Research
- Software
# permalink: phd-workflow-22
---

I have been struggling with stuttering engagement with reading in my PhD, with the consequence that I feel as if I do not yet have a coherent overall picture of the concepts I am trying to master, nor that I am making meaningful connections in the literature. A friend and colleague introduced me to the notes and ideas tool [Obsidian](https://obsidian.md/), based on Luhmann's *Zettelkasten*, or card index system of connecting ideas {% cite Schmidt2016 Schmidt2018 %}.

## Capturing information

The point of reading, at least in the context of a research project, is to assimilate interesting ideas and findings into your particular context. For the researcher, this context may be defined by the research question(s), or the topic of a literature review. Early attempts at this might involve highlighting passages of interest, or making marginal notes or underlining in the text. These "captures" are not much more useful than merely downloading interesting papers as pdf: all you end up with is a large collection of files, at best organised in folders. Referencing tools like Mendeley offer the ability to store notes with the files, which still avoids the intellectual engagement required to make sense of a broad literature base, or indeed, of trying to identify what is not there -- the elusive "gap in the literature" that the research aims to fill. More is required: key ideas are needed to be processed and understood in order for meaning to be made. 

> "One cannot think without writing." -- Niklas Luhmann {% cite Ahrens2022 %}

## Capturing thought

This processing requires effort and the deployment of language: ideas from reading may be paraphrased and meaningfully summarised as short notes. These are more than a simple statement of the "essence" of a paper, although this may be considered the minimum example. One academic has described as "thesisable prose", the notes taken from a reading, paraphrased and restated within the reader's context. This infers that what you write down at the time of reading needs to make sense at the level you are working, not only to others but also to your future self. How many times have I read my own notes and cursed myself for being too terse, too clever, or too sloppy? The advice I have from my supervisors is to read with the research question in view -- to help sustain focus and avoid rabbit-holes, but also to keep the questions themselves under constant critical evaluation. This advice is meaningful at my early stage of a research project like this.

## The discipline of metadata

Organisation and structure of this library of collected thoughts and summaries is crucial for it to become useful. The usefulness goes beyond simply offering rapid retrieval of ideas and a tidy desk: it offers a reflective surface with which to interact, to provide deeper understanding, to make new meaning, to notice and make new connections, and to see your topic in the literature more comprehensively, complete with its gaps and inconsistencies. 

Descriptive words may be used to categorise and group notes: academic readers are already familiar with *title*, *abstract*, *author* and *keywords* as descriptive metatdata about a published paper. Hashtags are a modern take on this, to associate information and ideas around a theme. These tags make searching easy, collecting [#birds of a #feather](https://twitter.com/search?q=%23birds%20%23feather) together. A unique number or code for each note allows them to be referenced in other notes, connecting ideas.

## Zettelkasten

In Niklas Luhmann's method of making such notes, each is written on a uniquely-numbered paper slip (in German: *zettel*) and placed in order in a box (*kasten*, plural *kästen*). Although Luhmann's card numbering was used only to uniquely identify each card[^rbdms], the numbering used may suggest a hierarchy of ideas; cards may reference others by the number of the referenced card; tags may be applied to collect and group ideas across hierarchies. 

The numbering system of Zettelkasten is illustrated by {% cite Schmidt2016 -l 301 %}:

```
1/1 Card with notes 
    1/1a Card containing notes referring to a concept/idea from card 1/1 
    1/1b Continuation of notes from card 1/1a 
        1/1b1 Card containing notes referring to a concept/idea from card 1/1b 
        1/1b2 Continuation of notes from card 1/1b1 
1/2 Continuation of notes from card 1/1
```

The design of this is to deliberately avoid imposing structure on the notes as they are made, so as not to force thinking into a one-time-and-for-ever way of thinking. The principle is to allow the author to have [a conversation](https://luhmann.surge.sh/communicating-with-slip-boxes) with the collection of ideas, as they are made, and later, as they connect to existing thought. Luhmann called the system his "secondary memory" {% cite Schmidt2016 -l 295%} to almost infer a thinking partner in the process of reflecting on and interrogating his own ideas.

Luhmann was famously very productive, writing over 60 books over 40 years, from 90,000 hand-written notes which he organised in boxes, and indexed. The index or register provides a list of **entry points** for each topic or keyword and is the first of four kinds of links used in the Zettelkasten system, only two of which are useful in a digital implementation. The other type of link is card-to-card, or **hyperlinks** between related ideas. This makes the cards, texts that refer to other texts: they are *hypertext* {% cite Berners-Lee1992 %}.

## Obsidian

There [are several programs](https://takesmartnotes.com/tools/) with which one may use Zettelkasten but I was specifically pointed at Obsidian and so tried it. The cards in this program are individual Markdown files, which sits well with my existing working habits. All of the written work I do, pretty much is in markdown (including the document you're reading). I already have 20,000 words in my PhD files in the form of markdown, so this provided a rapid leg-up into Luhmann's methodology, although not as immediate as I thought at first. This is because one the principal features of Zettelkasten is its atomicity: each card holds a single piece of knowledge, if you can picture such a thing. The cards are not chapters of books, nor papers on a topic: they are ideas, which may be linked to other ideas or classified in some meaningful way. The first task I had to do with (a copy of) my various pieces of writing around the subjects in my PhD is the break them into little pieces, each piece a detail, or aspect, of something larger: the hard work in creating and sustaining this workflow, and which Luhmann said occupied much of his productive time, is in connecting new cards into the exisiting deck. Here we can see that the process of engaging with reading is not a trivial task at all, but one in which all of one's mental faculties are brought to bear.

Luhmann added references directly as he created a new card {% cite Schmidt2016 -l 303 %} but also regularly refreshed and updated them. There were "hub" cards which arise where cards have a higher number of links to other cards: we might picture these as nodes in the Obsidian graph view of our collection of ideas. 

![](/assets/img/IMG_9690.PNG)

This image was a screenshot from the mobile version of Obsidian, which allows me to use the program in the same way as I do on the desktop: I can edit, link and even dictate new notes on the fly: it's not necessary to buy the [Obsidian Sync](https://obsidian.md/sync) subscription if you work in the same virtual space: for Apple infrastructure users, this means the iCloud Drive [^ic-fix]. My Zettelkasten is pushed from there on the desktop to its home in a GitHub private repository. The program does quite a lot of the work for us, without excusing the author from tending to proper tagging and referencing. An example from my own "card" collection:

[^ic-fix]: Be careful that iCloud doesn't get stuck syncing. You can tell this by the presence of the little dotted cloud icon in Finder, which on mouse-over, tells you that the file or folder is "Waiting to Upload". The program that gets stuck is bird, the backend process behind iCloud Drive, which can be unstuck by typing `% pkill -f 'Support/bird'` in a terminal. Give it a minute and all should sync OK.

```markdown

## Chronotope
William Benjamin recognised the significance of time in his [radio pedagogy](Radio%20pedagogy.md), as an essential part of the power of the medium. The setting of a story in space and time has been called the chronotope [@Bakhtin1981 119].

 #chronotope
  ```
## Next steps

This has been just an introduction for me to this "way in" to better writing productivity in my PhD. The tip came at the right time for me, at a point where I was struggling with momentum. I am thankful Ramsey Affifi for sharing his practice with me, and to Sönke Ahrens, whose book has just arrived and is the subject of my close attention for the next few days.

## Further reading

1. https://en.wikipedia.org/wiki/Zettelkasten
1. https://sociologica.unibo.it/article/view/8350/8272
1. https://zettelkasten.de/introduction/
1. https://www.sloww.co/zettelkasten/
1. https://luhmann.surge.sh/communicating-with-slip-boxes
1. https://takesmartnotes.com/, companion site to Sönke Ahrens' excellent book {% cite Ahrens2022 %}, now in second edition.

There's also more information in this blog about my [PhD Workflow](/phd-workflow-22) if you are interested.

## References

{% bibliography --cited %}

## Footnotes

[^rbdms]: A relational database is made up of tables of records; each record in a table may be uniquely identified by a *key*, often an `ID` field. The database tables are boxes or *kästen* and each record in a table is a card or *zettel*. Seeking patterns and relationships in a relational database management system ([RDBMS](https://en.wikipedia.org/wiki/Relational_database)) demands skills in [SQL](https://en.wikipedia.org/wiki/SQL). Databases are behind billions of websites and computer systems in use today.