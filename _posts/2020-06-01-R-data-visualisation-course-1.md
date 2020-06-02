---
layout: post
title: Statistics and Visualisation with R
date: 2020-06-02 20:32
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
# Slack password aThA7b2FSB4sJLP
---
This is the first in a series of posts containing my notes from a course on Statistics and (data) Visualisation with R, presented by [Lucia Michielin](https://edinburgh.academia.edu/luciamichielin) of the University of Edinburgh. The course is running two days a week in June and July.

**First week**

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
Class 1|01 June 13:00-14:30|**Intro to R and R studio**
Class 2|02 June 13:00-14:30|**Types of data and Grammar of graphs**
Class 3|08 June 13:00-14:30|Intro to statistics and descriptive stats
Class 4|09 June 13:00-14:30|Boxplot and playing with Colours
Class 5|15 June 13:00-14:30|Data Collection Bias, Probability, and Distribution 
Class 6|18 June 13:00-14:30|Hypothesis testings and the main tests 
Class 7|22 June 13:00-14:30|Barcharts and cleaning  the sample
Class 8|23 June 13:00-14:30|PCA and Cluster analysis
Class 9|29 June 13:00-14:30|Covariance, Regression, Similarity and Difference coefficients
Class 10|30 June 13:00-14:30|Recap and Bring your dataset class 

## Class 1 - Intro to R and R studio 
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
Getting help is a matter of issuing a query command: e.g. `?datasets` displays help on the Datasets package.

### Packages

Packages are installed and activated thus:
```R
install.packages("ggplot2")
?install.packages  # Get help on installing packages

## Activate packages ==========================
library(ggplot2)
```
We ended the session by installing something called the "Tidyverse", which seems to be a collection of useful packages. It calls itself an "opinionated collection of R packages designed for data science".

## Class 2 - Types of data and Grammar of graphs

* Type of Data 
* How to load data 
* How to choose the right Graph
* Graph types
* The Grammar of Graphs
* Ggplot2  structure
* Graph settings

### Data types

Type|Description
:---|:-----------
Vector|One dimensional collection of data, like a column or row, all of the same type
Matrix|Two-dimensional collection of data, all of the same type
Array|Multi-dimensional collection of data, all of the same type
Data frame|Mixed type variables (similar to a table in spreadsheet)

Reading a table by convention has *variables* in columns, and the *observations* or data values are in the rows. Vectors, arrays and matrices in R all must contain the same data type, and a data frame is the only construct that allows mixed types.

### Keeping the environment clean

```R
# Clear environment
rm(list = ls())

# Clear console
cat("\014")  # ctrl+L
```

### Loading data
```R
df <- read_csv("data/RodentSimplified.csv")

# ... same, with selection and mutation of month column name:

df2 <- read_csv("data/RodentSimplified.csv") %>%
  select(mo,dy,yr,period,species) %>% 
  mutate(period = as.factor(period)) %>%
  rename(month = mo) %>%
  print()
```
What looks like a continuation line in the above code block is called a "pipe", written `%>%`. A pipe is much more than just for making the code look pretty: it really does work as a pipe to transfer a value between subsequent function calls. See [this](https://style.tidyverse.org/pipes.html) and [this](https://magrittr.tidyverse.org/) and [this](https://cran.r-project.org/web/packages/magrittr/vignettes/magrittr.html) for more details. 

### Graph types
After some warnings on selecting data presentation that is consistent with your intention to actually communicate something, and not to show off, Lucia introduced us to some of the graph types available with R. She gave us a really nice demonstration why many journals prefer data presentation (e.g. ratios) as a bar chart rather than a pie chart. Differences are sometimes clearer in the bar chart. Apparently, Florence Nightingale invented the pie chart!

### The Grammar of graphics
The `ggplot` function allows the creation of graphs according to the framework outlined by Wilkinson[^Wilkinson] in which the separate aspects of data presentation are dealt with separately. A basic template is described [here](https://homepage.divms.uiowa.edu/~luke/classes/STAT4580/ggplot.html) with examples for `ggplot`. My take on the framework is:

1. a **data** set
2. **aesthetics** = a set of scales and variables to be plotted
3. **geometry** = shapes to represent the data and the type of chart
4. a grid of subplots, or **facets**
5. **statistics** = summaries of the data
6. **coordinates** to define the plotting space
7. global **themes** and labels to make it look pretty

Some of these map into the `ggplot` function, from the most basic (using examples from the weekly challenge, below):

```R
ggplot(college, aes(x=sat_avg, y=admission_rate)) + geom_point()
```
Here, the `aes` part is the aesthetics definition of the variables for the plot; `geom_point` defines the type of chart (scatter plot), and `college` is the data set.

### The weekly challenge
I completely failed to get anything at all out of the challenge in the 5 minutes we were given for this task. My code just didn't produce any kind of plot, just barffing errors at me. This was entirely down to my inability to type or read carefully what I had typed. Later, I managed to make some progress:

```R
# Import CSV files from online repo
college <- read_csv('http://672258.youcanlearnit.net/college.csv')
college <- college %>%
  mutate(state=as.factor(state), region=as.factor(region),
         highest_degree=as.factor(highest_degree),
         control=as.factor(control), gender=as.factor(gender),
         loan_default_rate=as.numeric(loan_default_rate))
# Create a chart that would show the relationship between the SAT average and the admission rate 
ggplot(college, aes(x=sat_avg, y=admission_rate)) + geom_point()
```
Time is not in abundance at the moment, so I did eventually just look at the solution and run it, seeing how each element of the code contributed to the final result. Here's my result:

![](/assets/img/Challenge_1.png)

[^Wilkinson]: Wilkinson, L. (2005) The Grammar of Graphics, The Grammar of Graphics. Springer-Verlag. doi: 10.1007/0-387-28695-0.
<!--see slides and link the book-->

## Next class

* Discuss the results of the challenge 
* Intro to Statistics
* Descriptive Statistics
* Summarising Statistics
* Exploring 1 variable: Plotting distribution Histograms and Density plot



## Notes and references

