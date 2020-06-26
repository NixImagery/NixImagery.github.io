---
layout: post
title: Datacamp course - introduction to R
# date: 2020-06-16 15:08
# description: 
img: new-years-day.jpg
fig-caption: New Year's Day
fig-attrib: Nick Hood
published: yes
tags:
- Data
- R
- CPD

# permalink:
---
Having abandoned the data visualisation course run by Edinburgh University, and wanting to gain some further competence in R, I took the [DataCamp "Introduction to R" course](https://learn.datacamp.com/courses/free-introduction-to-r). This course is written by [Jonathan Cornelissen](https://www.jonathancornelissen.com/), one of the founders of DataCamp and a man with seriously good credentials in R.

* table of contents
{:toc}

## Basics
### Assignment and operators
```r
a <- 4		# assignment 3 ways
4 -> a
a = 4

1 + 2		# mathematical operators
4 - 3 
6 * 5
(7 + 9) / 2 
8^2		# exponentiation
10 %% 4		# modulo

x < y		# less than
a > c		# greater than
a <= b 
j >= k 
one == two	# equal to
up != down	# not equal to
```

### Data types
```r
12.5 / 2.5	# numerics
7 + 123		# integers are also numerics
7 = 3		# Boolean (TRUE or FALSE) are logicals
"Hello world"	# characters

class(x)	# what data type is x?
```
## Vectors
A vector is a one-dimensional array (think of a row in a spreadsheet). In research, this is a single *observation*.

```r
# using the combine function to create a vector
a_numeric_vector <- c(1, 2, 3, 4, 5)

# vectors can have column names
names(a_numeric_vector) <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")

# printing the vector outputs the element names:
> a_numeric_vector
   Monday   Tuesday Wednesday  Thursday    Friday 
        1         2         3         4         5
> 

# using a vector to hold the column names
days_of_week <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")
names(week-values) <- days_of_week
```
You can do some quick and easy arithmetic with vectors.

```r
low_nums <- c(1, 2, 3, 4, 5)
hi_nums <- c(6, 7, 8, 9, 10)

total_nums <- low_nums + hi_nums

> total_nums
[1]  7  9 11 13 15

sum(low_nums) 	# adds up the elements in the vector
mean(low_nums)	# average of elements in the vector

low_nums[3]	# print the third low number (note 1-index)
hi_num[c(2:4)] 	# just get the middle values
```

The selection of elements can be conditional using boolean values in another vector.

```r
> c(49, 50, 51) > 50
[1] FALSE FALSE TRUE

> nums <- c(1:99)	# vector of the first 99 integers
> fives <- nums %% 5
> nums[fives == 0]	# all of those divisible by 5 [1]  5 10 15 20 25 30 35 40 45 50 55 60 65 70 75 80 85 90 95
```

In the last example above, ```fives == 0``` is a vector of boolean values. Used as a selector in the `nums` vector, only the `TRUE` elements are selected.

## Matrices
A matrix in R is a collection of elements, all of the same data type, arranged in 2 dimensions of rows and columns.

```r
> # A matrix that contain the numbers 1 up to 9 in 3 rows
> matrix(1:9, byrow = TRUE, nrow = 3)
     [,1] [,2] [,3]
[1,]    1    2    3
[2,]    4    5    6
[3,]    7    8    9
> 
```
The access indicators are shown in the row labels and column headers above. So, element [2,3] of the matrix contains the value 6. The first row of `my_matrix` is the vector `my_matrix[1,]`. Row and column names can be set for matrices, as they can be for vectors. This can be done by calling rownames() and colnames(), or at the time the matrix is set up.

```r
# Construct star_wars_matrix
box_office <- c(460.998, 314.4, 290.475, 247.900, 309.306, 165.8)
star_wars_matrix <- matrix(box_office, nrow = 3, byrow = TRUE,
                           dimnames = list(c("A New Hope", "The Empire Strikes Back", "Return of the Jedi"), 
                                           c("US", "non-US")))
```

The function `cbind()` binds columns to an existing matrix. `rbind()` does the same thing for adding row vectors to a matrix. `rowSums()` and `colSums()` do what they sound like - making new vectors ready to be bound into the source matrix if required.

Arithmetic operators work element-wise on matrices.

## Factors

## Data Frames

## Lists

## Notes and references
