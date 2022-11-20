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
Continuing my journey into `R`, the next course in the R programming track at DataCamp is Intermediate R. This course is presented by Filip Schouwenaars. It teaches language syntax and programming conventions, building on [the last course](/introduction-to-R-datacamp).

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
Syntax for these familiar operators is `&`, `|` and `!`, for logical `AND`, `OR` and `NOT`, respectively. They have high precedence and therefore do not need brackets around expressions:

```r
> 4 > 3 & 8 <= 9
[1] TRUE
```
Logical operators may be used on matrices and vectors:

```r
> !c(TRUE, FALSE, 1 > 0)
[1] FALSE  TRUE FALSE
```

Note that double-signed operators like `&&` work only on the first element of a vector.

### Conditional statements
Again, familiar syntax here, with the conditional test in brackets; code blocks in curly braces; and two statement words, `if` and `else`:

```r
x <- 0
if (x < 0) { 
    print ('x is negative')
} else if (x == 0) { 
  print ('x is zero') 
} else { 
    print ('x is positive') 
}
```
Notice that the `else` and `else if` statements come on the same line as the closign curly brace of the associated `if` statement. Once a conditional test evaluates `TRUE`, the corresponding code block is executed and the remaining code within the `if` control structure is ignored. Conditional statements may be nested.

## Evaluation and next steps
There is a greater teacher presence in this course than the previous, through the use of video presentations to support the hands-on interactive labs.

Thus far into the `R` Programming Track with Datacamp, I have stopped because I have hit an unexpected paywall. Continuing requires a commitment of at least $25 per month, which is good value if I were continuing with courses several hours per day but not appropriate for my current ad-hoc engagement. The day job takes priority, which means *all* of the available time mostly. I'll be switching to other resources from now, probably starting with *R for Data Science*[^Grolemund2016], or at least the [online version](https://r4ds.had.co.nz/).

## References
[^Grolemund2016]: Grolemund, G. and Wickham, H. (2016) R for Data Science, O’Reilly Media.