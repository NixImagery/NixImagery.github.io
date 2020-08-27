---
layout: post
title: Merge join data files on 2 columns with python
date: 2020-08-27
# description: 
img: R0000677.jpg
fig-caption: Rolling Stones
fig-attrib: Nick Hood
published: yes
tags:
- Python
- Data
- OSX

# permalink:
---
This was posted on a forum:

> I have two enormous data sets - 2 million rows in each one. I have them in ASCII format. Each set has three columns. The first two columns are identical for both sets - essentially, coordinates. The third row in each set gives the temperature at that location for two different substances.

> I am trying to find a way to create a single table with 4 columns, the first two being the coordinates and the third and fourth being the different temperatures.

> Excel gives up after 1,000,000 rows.

> Can anyone suggest a (free) tool that can do this - and then preferably allow for some analysis - plotting temp 1 against temp 2, for instance.

I thought about this on and off during one of those challenging COVID days, and finally sat down in the evening and knocked up a quick solution to the first part of the problem, using `python`.

file 1.csv, 2.csv contain data:

```sh
$ cat 1.csv 
"x","y","t1"
42,35,122
39,44,242
12,43,188

$ cat 2.csv 
"x","y","t2"
53,22,192
39,44,122
22,56,238
```

Launching `python 3`[^why]

```sh
$ python3
Python 3.6.2 (v3.6.2:5fd33b5926, Jul 16 2017, 20:11:06) 
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
```
```python
>>> import pandas as pd
>>> csv1 = pd.read_csv("1.csv")
>>> csv2 = pd.read_csv("2.csv”)
```
(check it looks ok)

```python
>>> csv1.head()
    x   y   t1
0  42  35  122
1  39  44  242
2  12  43  188
>>> csv2.head()
    x   y   t2
0  53  22  192
1  39  44  122
2  22  56  238
```
Make an outer join of these two tables on the two coordinate columns:

```python
>>> merged_data = csv1.merge(csv2,on=["x","y"],how='outer’)

>>> merged_data.head()
    x   y     t1     t2
0  42  35  122.0    NaN
1  39  44  242.0  122.0
2  12  43  188.0    NaN
3  53  22    NaN  192.0
4  22  56    NaN  238.0
```

“NaN” is not your Nan, it’s just "not a number", or “no data here”.

```python
>>> merged_data.to_csv("out.csv",index=False)
```

... and back in the shell, we can see the result...

```sh
$ cat out.csv 
x,y,t1,t2
42,35,122.0,
39,44,242.0,122.0
12,43,188.0,
53,22,,192.0
22,56,,238.0
```
… your merged file, sir.

[^why]: I am using python3 because OSX has a legacy version 2 nobody dares touch. On other systems you might want to use just “python” and “pip” in the above examples. You might have to install pandas first, using `$ pip3 install pandas`.

It ought to work with a few million rows. I didn't answer the final part of the OP's question but it ought to easy enough with this example - a million or more rows, might be a different problem.

## Footnotes
