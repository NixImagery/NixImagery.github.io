---
layout: post
title: Statistics and Visualisation with R
date: 2020-05-28 15:40
# description: 
img: pirate-ship-at-sea.jpg
fig-caption: Pirates
fig-attrib: Public Domain
published: yes
tags:
- Data
- R
- CPD

# permalink:

# Session 1 will take place on Monday 1 June, 13:00 – 14:30, via the Blackboard Collaborate virtual classroom. You can join the session remotely from 15 minutes before the start time.
 
# Here are links to the join the Collaborate sessions:
# Session 1: https://eu.bbcollab.com/guest/edf7955cbca94e80ad7686b3b0022d6d
# Session 2: https://eu.bbcollab.com/guest/200cbd9eca474f4dad74fa9858af270e 

# Slack password aThA7b2FSB4sJLP
---
These are my notes from a course on Statistics and (data) Visualisation with R, presented by [Lucia Michielin](https://edinburgh.academia.edu/luciamichielin) of the University of Edinburgh. The course ran two days a week in June and July.

**Contents**

* Do not remove this line (it will not be displayed)
{:toc}

## The learning environment
The course was presented in a blended form using Collaborate, Blackboard Learn and Slack. These represent three key elements in a remote learning environment:

* Synchronous, whole-class activity, usually instructor-led, but may include "break-out" sessions for students to work together in groups.
* A resources repository for files, course outlines, presenter's notes and assignments.
* A back-channel for students to interact in, and for interaction with the course leader. This may be synchronous and asynchronous, but Slack is only used in this course for offline use. Collaborate chat is used in the live sessions.

The offline chatter and forum space is useful in courses like this, which is why Slack is such a useful tool here. Microsoft teams has been suggested as an equivalent to Slack but I really don't find it intuitive or useful in the same way as Slack. The UI, as with all Microsoft products I have ever used, is difficult and intrusive.

## Preparation
The pre-course task is to [install R](https://www.r-project.org/) and the [R-Studio IDE](https://rstudio.com/). I painlessly installed on my Mac R 4.0.0 "Arbor Day" and R-Studio 1.3.959, and downloaded the data files for the first week.

## Programme overview

Class|Date and time|Title
:------|:------|:------
Class 1|01 June 13:00-14:30|Intro to R and R studio 
Class 2|02 June 13:00-14:30|Types of data and Grammar of graphs
Class 3|08 June 13:00-14:30|Intro to statistics and descriptive stats
Class 4|09 June 13:00-14:30|Boxplot and playing with Colours
Class 5|15 June 13:00-14:30|Data Collection Bias, Probability, and Distribution 
Class 6|18 June 13:00-14:30|Hypothesis testings and the main tests 
Class 7|22 June 13:00-14:30|Barcharts and cleaning  the sample
Class 8|23 June 13:00-14:30|PCA and Cluster analysis
Class 9|29 June 13:00-14:30|Covariance, Regression, Similarity and Difference coefficients
Class 10|30 June 13:00-14:30|Recap and Bring your dataset class 

## Class 1
This began with an introduction on [The Edinburgh Centre for Data, Culture & Society (CDCS)](https://www.cdcs.ed.ac.uk/) and their other courses and research projects, followed by an introduction to our course leader, Lucia, and a walk around the VLE folders and files. Then, an overview of the first session:

* Intro to Quantitative methods in Research
* The R and R studio Interface
* How to organise your work in R efficiently
* How to install packages

This is fairly self-explanatory but an essential levelling for all delegates on the course, who come from a range of backgrounds. Most seemed to be researchers.

### R and R-Studio
R is the language, and R-Studio is a graphical IDE for working with projects and data using R. Lucia said that the key skill in acquiring a new language is knowing how to Google: R is widely used and has a large user base and the forums are very helpful in quickly overcoming problems.

### Scientific method
We heard about the scientific method and in particular the issue of correlation vs. causation. This, in context of remaining close to the process, and the meaning of the data, whilst engaging deeply with the IDE.

* Define a research question
* Explore the evidence
* Define working hypotheses
* Translate hypotheses → statistical models
* Compare models to evidence
* Interpret results

![](/assets/img/correlation.png)

### Getting our hands dirty
Finally we got to open R-Studio and follow Lucia through opening the script for today and take a walk around the IDE. We started with creating a new project and setting up a folder organisation for the course, then played with settings to make the IDE more comfortable for us.

Comments and header syntax was explained, then using an immediate mode of running commands in the console (by pressing cmd-enter). Outputs are presented in vectors: index 1.

```R
# THIS IS A LEVEL 1 HEADER #################################

## This Is a Level 2 Header ================================

### This is a level 3 header. ------------------------------

print('Hello World!')

## Define Variables ================
x <- 1:5 #Put the numbers between 1-5 in the variable x (alt- is a short code for <- in the IDE)
x #Displays the values we have set in x
```
### Packages

Packages are installed and activated thus:
```R
install.packages("ggplot2")
?install.packages  # Get help on installing packages

## Activate packages ==========================
library(ggplot2)
```
We ended the session by installing something called the "Tidyverse", which seems to be a collection of useful packages. It calls itself an "opinionated collection of R packages designed for data science".

## Class 2

* Data type
* Load dataset in R studio
* How to decide which Graph to use
* Type of Graphs
* Ggplot syntax
* Working with Ggplot


## Notes and references

