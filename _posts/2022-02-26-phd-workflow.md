---
layout: post
title: PhD Tools and software
date: 2022-02-26
# description: 
img: DSF8893.jpg
fig-caption: Get out of that!
fig-attrib: Nick Hood
published: true
katex: yes
tags:
- Markdown
- PhD
permalink: phd-workflow-22
---

I responded to a Twitter conversation about software used to write a thesis:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Markdown, Pandoc to pdf with Mendeley. I edit in VSCode, and config manage using GitHub. If anyone at <a href="https://twitter.com/MorayHouse?ref_src=twsrc%5Etfw">@MorayHouse</a> wants a demo/tutorial, let me know.</p>&mdash; Nick Hood (@cullaloe) <a href="https://twitter.com/cullaloe/status/1494320531436228613?ref_src=twsrc%5Etfw">February 17, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

[@Christina_Mik](https://twitter.com/Christina_Mik) asked for a demo, which I am happy to do in person but haven't the time to make a video of. What I have done instead is to adapt notes from the online thesis to describe the workflow and tools I am using.

---

## Platform

I try as much as possible to eliminate duplication of both effort and data and have learned that text-based files free me from the tyranny of proprietary idiosyncracies. All of what follows can be achieved on pretty much any modern computing platform: Windows, Linux, whatever. The main platform I use is a MacBook Air running macOS Big Sur 11.

## Workflow

I have three kinds of document to produce. The first kind are short, maybe only one to a few pages, or a presentation file, usually in the form of a printable pdf. Next, are the public articles such as the one you are reading. Finally, there are extended works which should be kept private but sharable until they are ready, like a thesis.

For all three kinds of document, I use plain text files which are readable across many platforms, and which are easily backed up and managed. I absolutely do not care about formatting whilst I am writing, it is just a distraction: I can get a machine to make it pretty when I am ready to publish or share. Here is a graphic of my writing workflow:

{% mermaid %}
graph TD
    subgraph Literature
    A([Reading])-->B[Citation & References]-->C[/Mendeley Desktop/]-->E(Bibtex file)
    B-->D[/Mendeley Web Importer/]-->DD-->C
    C-->DD[(Mendeley library)]
    end
    subgraph Writing
    A-->F([Thinking and analysis])-->G(Writing)-->H[/Visual Studio Code or MacDown /]-->X(Markdown text file)
    X-->L[(GitHub repository)]-->X
    end
{% endmermaid %}

Notice that the net output is in two files: the **markdown text file**, and the **bibtex file** containing all of the sources I have cited.

## Citation and referencing
[Mendeley](https://www.mendeley.com/) is a reference manager suite that includes a [desktop application](https://www.mendeley.com/reference-management/mendeley-desktop) to access and manage your own library of references, and generates [bibtex](http://www.bibtex.org/) files which can be used by text processors. Note that the desktop application is not being supported now: there is a newer and much less useful [Mendeley Reference Manager](https://www.mendeley.com/download-reference-manager). Many users have been lobbying Elsevier, who own Mendeley, to reinstate the Mendeley Desktop app or add its functionality to the new Reference Manager.

The most useful feature of Mendeley Desktop, apart from importing and managing my reference library, is the automatic creation and update of a `.bib` file of the entire library, or optionally, separate bib files for each folder. The bib file is used by $$\LaTeX$$ and pandoc when generating your document output, to insert correctly formatted citations and your bibliography.

## Document production

All of my documents are written in some form of [Markdown](https://daringfireball.net/projects/markdown/).

For writing casual or stand-alone documents (reports, presentations, articles), I may use the [Macdown](https://macdown.uranusjr.com/) open source Markdown editor for macOS, but more often there are several documents "on the go" at once within the same folder, when I find the [Visual Studio Code](https://visualstudio.microsoft.com/) IDE [^wssat] easiest to use for editing. It can be used to edit csv [^wassat2] files with [Janis DD](https://marketplace.visualstudio.com/publishers/janisdd)'s [Edit CSV](https://marketplace.visualstudio.com/items?itemName=janisdd.vscode-edit-csv) plugin.

[^wssat]: Integrated Development Environment
[^wassat2]: Comma-separated variables. Very simple data format that R Studio loves to turn into beautiful graphics.

Here's a visual of how the three types of document are produced from the markdown source file and the bibtex file:

{% mermaid %}
graph LR
    T(Bibtex file) --> J
    U(Markdown text file) --> J
    subgraph "Stand alone"
    J[/Pandoc/]-->K(.pdf or .docx)
    end
    T-->Q
    U-->Q
    subgraph Public/blog
    Q[/Jekyll/]-->R(.html)-->S("Website (GitHub Pages, public)")
    end
    T-->M
    U-->M
    subgraph Extended
    M[/R Studio/]-->P[Bookdown]-->N(.html, .pdf or .docx)-->O("Website (Static, secure)")
    end
{% endmermaid %}

### Stand-alone documents

[pandoc](https://pandoc.org/) is used to generate stand-alone documents from markdown source with [pandoc-citeproc](https://github.com/jgm/pandoc-citeproc) taking care of linking to bibliographies. Diagrams in these documents (like the graphics in this post) are produced using the [mermaid](https://github.com/raghur/mermaid-filter) filter for pandoc.

Documents written in markdown often include a short [YAML](https://yaml.org/) header containing information about it and instructions for pandoc, etc. Here is an example markdown document, with a YAML header:

```markdown
---
title: My amazing document
author: Nick Hood
bibliography: /path/to/your/library.bib
date: \today
---

# My heading
Here is some text which is very interesting. Here is some text which is very interesting. Here is some text which is very interesting. Here is some text which is very interesting. Here is some text which is very interesting.

## A subheading
Here is some text which is very interesting but more detailed. Here is some text which is very interesting but more detailed. Here is some text which is very interesting but more detailed. Here is some text which is very interesting but more detailed. Here is some text which is very interesting but more detailed. 

## A paragraph with a reference in it
Here is some text which is my interpretation of what someone else wrote about [@OxfordEnglishDictionary]. 

# References

```

To make a pdf of this document using pandoc, we type this in a terminal window:

```sh
$ pandoc -s filename.md -o filename.pdf --citeproc
```
It produces [this file](/assets/docs/filename.pdf).

### Extended documents, not public (e.g. Thesis)

[R](https://www.r-project.org/) and the [RStudio](https://www.rstudio.com/) IDE are used for larger documents and data processing {% cite RCoreTeam2021 %}, mostly within `RStudio`. My (non-public) thesis website is made using the [Bookdown](https://bookdown.org/) R package {% cite Xie2016 Xie2020 %}, which itself uses pandoc to generate HTML, Word and pdf documents. Read more about how I do this [in this post](/deploy-bookdown-site-plesk/).

### Public web articles (like the one you're reading)

This site is hosted on [GitHub Pages](https://pages.github.com/) which renders files uploaded and hosted there. It is possible to have GitHub use [Jekyll](https://jekyllrb.com/) but I prefer to build the pages on my local machine and have GitHub render static HTML. I have found this to be more stable and less prone to attack. Read more about that [here](/jekyll-update-via-rake) and [here](deploy-jekyll-site-from-github).

## Broadcast acquisition 

Not related to general projects but certainly useful in mine is the ability to capture for my own use, BBC radio programmes. [get_iPlayer](https://github.com/get-iplayer/get_iplayer) is a command-line programme written in Perl which downloads TV and radio programmes from BBC iPlayer/BBC Sounds {% cite notnac2021 %}.

## Configuration management/backup

Source documents and data files, all in text format, are retained in a [GitHub private repository](https://github.com/NixImagery). Not only does that mean that everything is backed up against loss or damage to a computer, it is also protected against me: I can roll back changes if I need to, or launch my computer off a cliff without losing my work. Not likely, but you wear a seat belt, don't you?

## Notes and references

This post originally appeared as [PhD Workflow](/phd-workflow) in July 2019 and has been updated with links and references to describe my current model. I hope it's useful.

{% bibliography --cited %}