---
layout: post
title: Datacamp course - intermediate R
date: 2020-07-10
# description: 
img: DSF7259.jpg
fig-caption: Achmelvich Beach
fig-attrib: Nick Hood
published: yes
tags:
- Data
- R
- CPD

# permalink:
---
Continuing my journey into `R`, the next course in the R programming track at DataCamp is [Intermediate R](https://campus.datacamp.com/courses/intermediate-r). This course is presented by [Filip Schouwenaars](https://www.datacamp.com/instructors/filipsch). It teaches language syntax and programming conventions, building on [the last course](/introduction-to-R-datacamp).

* table of contents
{:toc}

## Conditionals and Control Flow
### Relational operators
This section begins with a talk-through the main relational operators in R, with simple examples, followed by exercises in the virtual lab.

```r
> TRUE == TRUE			# Equality
[1] TRUE
> 'oranges' != 'apples'	# Inequality
[1] TRUE
> 'oranges' > 'apples'	# Strings compare alphabetically
[1] TRUE
> 'oranges' < 'apples'
[1] FALSE
> vec <- c('apples', 'bananas', 'dragon fruit', 'tomato')
> vec > 'oranges'		# Works on vectors (and matrices)
[1] FALSE FALSE FALSE  TRUE
```
`TRUE` coerces to the value 1, `FALSE`, 0. So truth is greater!

### Logical operators
Syntax for these familiar operators is `&`, `|` and `!`, for logical `AND`, `OR` and `NOT`, respectively.

## Evaluation and next steps
There is a greater teacher presence in this course than the previous, through the use of video presentations to support the hands-on interactive labs.