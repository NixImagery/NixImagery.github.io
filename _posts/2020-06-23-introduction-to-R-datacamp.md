---
layout: post
title: Datacamp course - introduction to R
date: 2020-07-08
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
Having abandoned the data visualisation course run by Edinburgh University, and wanting to gain some further competence in R, I took the [DataCamp "Introduction to R" course](https://datacamp.com/courses/free-introduction-to-r). This course is written by [Jonathan Cornelissen](https://www.jonathancornelissen.com/), one of the founders of DataCamp and a man with seriously good credentials in R.

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
> nums[fives == 0]	# all of those divisible by 5
 [1]  5 10 15 20 25 30 35 40 45 50 55 60 65 70 75 80 85 90 95
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
A **factor** is a data type used to store categorical variables. These are discrete variable which can only take a finite number of values (cf. continuous variables which can have any of an infinite set of values, like real numbers). `R` can make a vector of the categories from a vector of categorical values:

```r
> birthdates <- c(12,4,13,23,31,16,1,9,12,4,8,24,27,25,24,25)
> birthdates
 [1] 12  4 13 23 31 16  1  9 12  4  8 24 27 25 24 25
> bd_factors <- factor(birthdates)
> bd_factors
 [1] 12 4  13 23 31 16 1  9  12 4  8  24 27 25 24 25
Levels: 1 4 8 9 12 13 16 23 24 25 27 31
> 
```
Such variables are **nominal** or **ordinal** according to whether they are just names, or if they can be ranked in some meaningful way. Ordinal factors are created with additional parameters, e.g., `order = TRUE` and `levels = c("low", "high")` and can be compared easily.

## Data Frames
A **data frame** has the variables of a data set as columns and the observations as rows. A quick peek at the structure of a data frame is provided by `head()` and `tail()` functions, e.g.:

```r
> head(mtcars)
                   mpg cyl disp  hp drat    wt  qsec vs am gear carb
Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
>
```

`mtcars` is one of the many data sets built into R. A list of them is obtained by calling `data()`. `str()` provides a look at the structure of a data set:

```r
> str(mtcars)
'data.frame':	32 obs. of  11 variables:
 $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
 $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
 $ disp: num  160 160 108 258 360 ...
 $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
 $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
 $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
 $ qsec: num  16.5 17 18.6 19.4 17 ...
 $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
 $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
 $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
 $ carb: num  4 4 1 1 2 1 4 2 2 4 ...
> 
```
Columns of a data frame are added one column vector at a time as a list of parameters in the function call `data.frame()`. Selecting a data point from row 32, column 2 is a matter of calling `df_bears[32,2]`. Note the order - *observation* (row) first, then *variable* (column). A whole observation (e.g. the tenth) is obtained by `df_bears[10,]`. The first 4 data points from the *paw_size* column are `df_bears[1:4,"paw_size"]`. The whole column vector is `df_bears$paw_size` (notice the dollar sign notation). **Subsets** can be made calling `subset(df_bears, paw_size < 4)`. Sorting can be achieved by making a vector of the data frame order, based upon the columns you are interested in:

```r
> a <- order(df_bears$claw_size)
> df_bears[a,]
> 
> mtcars[order(mtcars$disp),]
>                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb
Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
...
```

## Lists
**Lists** can contain arbitrary data and **data types**. They are constructed by calling `list()` with optional names for each component, e.g. `list(top_dogs = df_dogs[1:10,], top_cats = df_cats[1:10,])`.

## Evaluation and next steps
I've found this introduction differently paced to the earlier introduction course run by the university. Because there is no instructor, attention has been paid to very small details: every aspect of the course works because it is programmatic. Learners have to take the right (small) steps to complete the exercises successfully. Errors are picked up and RTFQ-type prompts are given. This was less challenging than the earlier, demonstrator-led course but I completed this one, instead of bailing out feeling frustrated and weak. I also learned considerably more that is useful and earned a more secure foundation for further study.

I am working with RStudio on a daily basis now as I am producing documentation and course materials with Bookdown. My intention is to further develop competence with R and R-markdown.
