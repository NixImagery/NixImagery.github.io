---
layout: post
title: "Statistics and Visualisation with R #3"
# date: 2020-06-16 15:08
# description: 
img: sea-black-and-white-beach-89095.jpg
fig-caption: Pirate ships
fig-attrib: Public Domain
published: yes
tags:
- Data
- R
- CPD

# permalink:
# Slack password aThA7b2FSB4sJLP
---
Post number three of my notes from a course on Statistics and (data) Visualisation with R, presented by [Lucia Michielin](https://edinburgh.academia.edu/luciamichielin) of the University of Edinburgh in June and July.

**Third week**

* Do not remove this line (it will not be displayed)
{:toc}

## Programme overview

Class|Date and time|Title
:------|:------|:------
Class 1|01 June 13:00-14:30|Intro to R and R studio 
Class 2|02 June 13:00-14:30|Types of data and Grammar of graphs
Class 3|08 June 13:00-14:30|Intro to statistics and descriptive stats
Class 4|09 June 13:00-14:30|Boxplot and playing with Colours
Class 5|15 June 13:00-14:30|**Data Collection Bias, Probability, and Distribution**
Class 6|16 June 13:00-14:30|**Hypothesis testings and the main tests**
Class 7|22 June 13:00-14:30|Barcharts and cleaning the sample
Class 8|23 June 13:00-14:30|PCA and Cluster analysis
Class 9|29 June 13:00-14:30|Covariance, Regression, Similarity and Difference coefficients
Class 10|30 June 13:00-14:30|Recap and Bring your dataset class 

## Class 5 - Data Collection Bias, Probability, and Distribution

After a quick review of the challenge from last week, an agenda for today was shared which wasn't really followed[^progression].

### Data Collection and bias

> "Data collection is the process of gathering and measuring information on targeted variables in an established system, which then enables one to answer relevant questions and evaluate outcomes. 
The goal for all data collection is to capture quality evidence that allows analysis to lead to the formulation of convincing and credible answers to the questions that have been posed." ([Wikipedia](https://en.wikipedia.org/wiki/Data_collection))

The **sample** is taken from the **population**, but a **bias** is introduced when the sample is taken. One example of this is the **[survivorship bias](https://en.wikipedia.org/wiki/Survivorship_bias)**.

### Probability 
A basic definition was given to the class, with an example from an earlier class that helped us. If we make the statement `if **A** is true then **B** is true` can we infer from this that `if **B** is true then **A** is true`? Clearly not, but we might be able to say `if **B** is true then **A** is more plausible`. Plausibility here relates to how probably something can be.

> "Probability is a numerical description of how likely an event is to occur or how likely it is that a proposition is true." - [Wikipedia](https://en.wikipedia.org/wiki/Probability)

### Distribution

In introducing this topic, we were shown the really neat `rnorm()` function that generates random data sets with specified mean and standard deviation.

In the class, we were given a challenge to go through the steps needed with a new data set to examine it. These steps seem to be just to plot it and have a look. All of the curves looked to be distributed around a central mean, which makes them **normal** distributions. There was a problem with the challenge files which meant that some of us didn't have the correct files and so did a different (trivial) task. The key message is to examine your data as soon as you have it, to look for central values and distribution, so as to understand it and how you expect it to behave in analysis.

Other distributions include uniform, logarithmic, left-, right-skewed and bimodal.

## Playtime discoveries
Between this week's two classes, I had a quick look at the [Comprehensive R Archive Network (CRAN)](https://cran.r-project.org/) and discovered a neat thing. Remember the funky assignment operator `<-` from the first class which had its funky keyboard shortcut `alt -`? Most programming languages I've used have a simple equals sign as the assignment operator and I was a bit baffled as to why super-sexy R should do something so weird as `<-`. Well, it turns out that in most contexts, `=` works in exactly the way you'd expect, so these are equivalent:

```R
> x <- 99> x = 99
```
What's interesting about the R syntax, though, it that it can be reversed and it still works:

```R
> 99 -> x
```
I'm sure that the case for this will become apparent eventually. One more way to do assignments is to call the assignment function:

```R
> assign('x', 99) # notice the weird need for quotes around x in the function call
```

## Next class

* Hypothesis testing
* Null-Hypothesis
* Main types of tests
* Limitations and corrections

## Notes and references
[^progression]: I seem to be not the only one amongst the diminishing cohort (we're down to a dozen today, having started closer to 50) that is finding it hard to follow this course. Yes, it's interesting and cool, the different things you can do with R and geometries, but I am missing clarity, signposting, structure and other basic pedagogical features. 

    Taking time after class to review the presentation slides, it was possible to reconstruct perhaps what the instructor was intending, for example, in the two slides on probability and more generally with this class today. I might have got very little from today's session without spending as long again going over the materials. I am perhaps going to seek out other resources.

