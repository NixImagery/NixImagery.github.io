---
layout: post
title: PhD Workflow
date: 2019-07-19 18:00
# description: 
img: alfie.jpg
fig-caption: Alfie, PhD assistant
# fig-attrib: 
published: true
tags:
- education
- Research
- Science
- AI
- GitHub
- markdown
- YAML
- PhD
# permalink:
---
I've been setting up document repositories and workflows for a potential new research project which will consider teaching approaches for the understanding of complex ideas. In the project, there will be criticism of social constructivism as a default pedagogy and examination of intelligent automation of teaching.

# Workflow
## Tools and software
Documents will be retained in a GitHub private repository, and written in markdown either using the [OSX MacDown app](https://macdown.uranusjr.com/) or the cross-platform [Visual Studio](https://visualstudio.microsoft.com/). Masters will be kept in pdf, converted using [pandoc](https://pandoc.org/) with [pandoc-citeproc](https://github.com/jgm/pandoc-citeproc) taking care of linking to bibliographies. These will be produced and managed using [Mendeley](https://www.mendeley.com), which itself serves as a multi-device reader.

## Making the documents
Most of the documents are in markdown, with a YAML header containing information about it. You can make pdf, docx, or html versions of these documents in one of two ways:

* In Visual Studio, with appropriate settings, using the [vscode-pandoc](https://github.com/dfinke/vscode-pandoc) extension. Issue the command by pressing cmd-K, then P. Select the format you need. pdf is default, so hit return.
* On the command line, in the source folder, type:

```sh
$ pandoc filename.md -o filename.pdf --bibliography="Users/nickhood/Dropbox/Bibliographies/PhD.bib"
```
# The research project
## Previously
Between 2014 and 2016 I engaged in a PhD project that was looking at **the characteristics of the transaction space between teacher and learner in traditional and technology enhanced education.** The idea for this came about from the use of a modified form of the traditional Cambridge Tutorial method and developed to consider teaching spaces that are characterised by the absence of the teacher such as the MOOC. The project didn't get to data gathering before it was abandoned for lack of time and funds to continue.

## Early ideas
In the early stages of this revisit, I wanted to look at this space as being mediated by some graphical image as stimulus for deep, disruptive, and enriching learning. The space may be adversarial, and is is designed to be social and creative. This approach is applied where the learning relates to understanding of some known topic of a complex nature.

## Development
As of July 2019, I have rejected these ideas as I begin to recognize that perhaps that which I peddle is Snake Oil, or at least, not without serious faults. This is not to say that I reject the importance of the social dimension in certain learning spaces, just that it is neither necessary nor sufficient for learning.
