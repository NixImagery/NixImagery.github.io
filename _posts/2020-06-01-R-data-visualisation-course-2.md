---
layout: post
title: "Statistics and Visualisation with R #2"
date: 2020-06-09 15:08
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
Class 7|22 June 13:00-14:30|Barcharts and cleaning the sample
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

### The results of the challenge 
Last week's challenge was discussed, focusing on the meaning of the plots obtained, and how to add a best fit line using `+geom_smooth()` geometry to the `gg-plot` command. We played a bit with a tool to help us get better at "seeing" the correlation of plotted data: [guessthecorrelation](http://guessthecorrelation.com/).

### Intro to Statistics
This part of the class was further levelling by going over the basics of statistics and how they may be used to **summarise** or **infer** information. **Central tendency** includes arithmetic mean, median and mode values. **Measures of dispersion** like variance and standard deviation were also discussed. These functions were illustrated in the R IDE, including accessing columns within datasets using the dollar sign like this:

```R
mean(iris$Petal.Width)	#using mean formula
```
Similar functions offer median, variance and sd (standard deviation) calculations.

### Visualise the distribution: Histogram and Density plots

There is a nice [cheat sheet for ggplot data visualisation](https://rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf) tips.

Subsets of the data based upon some category can be easily made:

```R
virginica <- subset(iris, Species=="virginica")
```
A table of data around these subsets can be quickly constructed and plotted:

```R
#Values of Virginica
mean(virginica$Petal.Width)
median(virginica$Petal.Width)
var(virginica$Petal.Width)
sd (virginica$Petal.Width)

#... etc for the other two

# Make a new table...
Species <- c("setosa","versicolor", "virginica")

# add columns...
Mean <- c(mean(setosa$Petal.Width), mean(versicolor$Petal.Width), mean(virginica$Petal.Width))
Median <- c(median(setosa$Petal.Width), median(versicolor$Petal.Width), median(virginica$Petal.Width))
Variance <- c(round(var(setosa$Petal.Width), digits = 2), round(var(versicolor$Petal.Width), digits = 2), round(var(virginica$Petal.Width), digits = 2))
SD <- c(round(sd(setosa$Petal.Width), digits = 2), round(sd(versicolor$Petal.Width), digits = 2),round(sd(virginica$Petal.Width), digits = 2))

# Make the data frame for plotting...
FullPlot <- as.data.frame(cbind(Species, Mean, Median, Variance, SD))
```
Notice you can double-click on the FullPlot table in the environment box (equivalent to the command `View(FullPlot)`), it will display the table in a new tab for inspection.

```R
# ... and now plot it in a nice histogram

ggplot(iris, aes(x=Petal.Width, fill=Species))+ 
  geom_histogram(alpha=0.8,color="black", binwidth=0.08)+
  geom_vline(aes(xintercept = mean(Petal.Width)),col='red',size=2)+
  theme_bw()+facet_wrap(~Species, ncol = 1) 
  
```
Here's how that looks:

![](/assets/img/iris-histogram.png)

### The next challenge, number 2
Once again, I got nowhere with the challenge in the 10 minutes we had to do it. I spent most of that time, after loading the dataset, trying to figure out how to make a scatter plot.  When we reviewd the problem at the end of the class, it became apparent that the question was looking for a histogram, not a scatter plot. Getting stuck here meant that I didn't know how to approach the second part of the challenge, and didn't progress to reading the third.

## Class 4 - Boxplot and playing with Colours

* Discuss Challenge 2
* Boxplots
* Playing with colours 
* Exporting graphs

### Discussing Challenge 2 and feeling lost
No time to spend on this before the next class, so I just sat back and tried to follow the discussion[^fml]. 

[^fml]: This shook my confidence a little, which took me back to my school days, the last time that I was so lost in a class that I wasn't even aware when the teacher was asking a question. All you can do in this situation is wait for the next section and try to be invisible. Part of the difficulty I am having is the heavy accent of the instructor, which causes me to miss signposts and words. It made me think of all the EAL kids in Scottish schools.

### Boxplots

![Boxplot](/assets/img/boxplot.png)

* The thick black line is the median.
* The boxes represent 50% of the sample closest to the median
* The whiskers correspond to 95% of the sample closest to the median aka 2SD from the median 
* The dots represent the outliers 

In R, boxplots are another geometry[^gallery]:

[^gallery]: There is a complete catalogue of the graphs available in R at [r-graph-gallery.com](https://www.r-graph-gallery.com/).

```R
ggplot(iris, aes(x=Species, y=Petal.Width, fill=Species)) + geom_boxplot()
```

### Playing with colours
There are a number of colour themes within R to allow you to make beautiful and readable plots and graphs. What is important, as with all open source, is that when using different packages and utilities, you must RTFM[^rtm].

[^rtm]: Read the manual.

These are invoked with colour commands and palettes, like `scale_color_manual` here:

```R
ggplot(iris, aes(x=Species, y=Petal.Width, color=Species)) + 
  geom_boxplot(outlier.alpha = 0)+
  scale_color_manual(values = wes_palette("GrandBudapest2", n=4))

# other color methods:
scale_color_grey(start = 0.6, end = 0.1) # grayscale
scale_color_manual(values=c("#80ec65", "#145200", "#700015")) # manually defined
scale_color_gradientn(colours = rainbow(7)) # gradient
```

### Exporting graphs
Pretty self-explanatory from the IDE: exporting graphs to pdf or png is available from the dropdown in the plots tab.

### Challenge number 3
Well, today I managed to get a result during the time allocated for us to work on the problem, which made up for how I had been feeling earlier. With a little tweaking after class, I settled on this:

```R
ggplot(college, aes(x=region, y=faculty_salary_avg, fill = region)) + 
  geom_boxplot(outlier.alpha = 0.0, alpha = 0.8) +
  geom_jitter(alpha =0.2)+
  theme_bw()+ 
  facet_wrap(~control, ncol = 2)+
  labs(title = "USA University", 
       subtitle = "Faculty salary by region", 
       x = "Region", 
       y = "Average salary")
```
which yielded this:

![Challenge 3 plot](/assets/img/challenge3.png)

## Next class

* Data Collection 
* Datasets biases
* Inferential statistics
* Probability 


## Notes and references

