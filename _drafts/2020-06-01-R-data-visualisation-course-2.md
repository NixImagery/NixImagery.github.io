---
layout: post
title: Statistics and Visualisation with R, week 2
date: 2020-06-04 20:50
# date: 2020-06-09 20:32
# description: 
img: pirate_ships.jpg
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
This is the second in a series of posts containing my notes from a course on Statistics and (data) Visualisation with R, presented by [Lucia Michielin](https://edinburgh.academia.edu/luciamichielin) of the University of Edinburgh. The course is running two days a week in June and July.

**Second week**

* Do not remove this line (it will not be displayed)
{:toc}

## Programme overview

Class|Date and time|Title
:------|:------|:------
Class 1|01 June 13:00-14:30|Intro to R and R studio 
Class 2|02 June 13:00-14:30|Types of data and Grammar of graphs
Class 3|08 June 13:00-14:30|**Intro to statistics and descriptive stats**
Class 4|09 June 13:00-14:30|**Boxplot and playing with Colours**
Class 5|15 June 13:00-14:30|Data Collection Bias, Probability, and Distribution 
Class 6|18 June 13:00-14:30|Hypothesis testings and the main tests 
Class 7|22 June 13:00-14:30|Barcharts and cleaning  the sample
Class 8|23 June 13:00-14:30|PCA and Cluster analysis
Class 9|29 June 13:00-14:30|Covariance, Regression, Similarity and Difference coefficients
Class 10|30 June 13:00-14:30|Recap and Bring your dataset class 

## A bit of homework

### Errors
I had the chance to play with the IDE and learn a few things by invoking errors.

```R
> ggplot(college, aes(x=sat_avg, y=admission_rate)) + geom_point()
Error in ggplot(college, aes(x = sat_avg, y = admission_rate)) : 
  could not find function "ggplot"
```
The above occurs if you just run that line of code without first loading the library in which `ggplot` lives, i.e. by calling `library("tidyverse")` first. 

```R
> ggplot(college, aes(x=sat_avg, y=admission_rate)) + geom_point()
Error in ggplot(college, aes(x = sat_avg, y = admission_rate)) : 
  object 'college' not found
```
This error is thrown because the data object 'college' has not been created. Do this by loading the data first, i.e. call `college <- read_csv('http://672258.youcanlearnit.net/college.csv')`.

### Mutate and as.factor
Last week's class included the creation of the dataset using this call:

```R
college <- college %>%
  mutate(state=as.factor(state), region=as.factor(region),
         highest_degree=as.factor(highest_degree),
         control=as.factor(control), gender=as.factor(gender),
         loan_default_rate=as.numeric(loan_default_rate))
```

The `mutate()` function adds new variable columns to the dataset or replaces existing ones if the same name is used. You can see that `state` is replaced by a different version of itself: the `as.factor()` function takes data and turns it into a factor if it isn't already. "Factor" is a term that indicates that the data is a category or enumerated type, rather than just a set of strings. To see this, consider this:

```R
> var=letters[1:5]
> var
[1] "a" "b" "c" "d" "e"
> var=as.factor(var)
> var
[1] a b c d e
Levels: a b c d e
```
`var` is created as a vector, then converted to a factor or column in the `as.factor` call.

## Class 3 - Intro to statistics and descriptive stats
* Discuss the results of the challenge 
* Intro to Statistics
* Descriptive Statistics
* Summarising Statistics
* Exploring 1 variable: Plotting distribution Histograms and Density plot

## Next class




## Notes and references

