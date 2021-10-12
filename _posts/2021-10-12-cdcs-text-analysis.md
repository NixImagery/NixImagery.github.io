---
layout: post
title: Introduction to Text Analysis 
date: 2021-10-12 15:30
# description: 
img: Kodak-Portra-800-20211010_12192098.jpg
fig-caption: Quinag
fig-attrib: Nick Hood
published: yes
tags:
- PhD
- CPD
- Text Analysis
- CDCS

# permalink:
---

I booked on to the [CDCS Introduction to Text Analysis](https://www.cdcs.ed.ac.uk/events/introduction-text-analysis) 2-hour course and installed [nltk](http://www.nltk.org/install.html) in preparation. This 2-hour "silent disco" online event is an intermediate Python course on using the NLTK package.

### Introduction to Text Analysis

The workshop uses Notable but I ran the [notebook](https://digital-exploits.edina.ac.uk/intro-ta/files/intro_text_analysis-2021.ipynb) in Visual Studio (because it's a good IDE). The notebook is written in markdown text with code blocks interspersed in "cells" throughout the document.

The workshop begins with some exercises in the IDE to get used to running python code within the cells to do something with text strings, using variables, e.g.

```python
first_name = "ada"
last_name = "lovelace"

full_name = first_name + ' ' + last_name # combine strings with a space inbetween

print (full_name)
```

### File handling

Basic file actions are rehearsed including opening and reading a file, and using text manipulation functions:

```python3
file = open("origin-intro.txt")

txt = file.read()
txt = txt.lower()
```

### NLTK

The Python package NLTK provides a set of natural languages algorithms e.g. tokenizing, part-of-speech tagging, stemming, sentiment analysis, topic segmentation, and named entity recognition. We played with some of these using the text extracts we had been given.

#### Tokenization
Text analysis begins with breaking down a block of text into smaller chunks such as words or sentences. This is called *Tokenization*.

```python
import nltk
from nltk.tokenize import sent_tokenize # or word_tokenize for words

f = open("origin-intro.txt") # open file

txt = f.read()          # add file contents to variable

tokenized_text=sent_tokenize(txt)

print(tokenized_text)
```

#### Cleaning text

The initial part of this process in preparing for analysis is:

* Open the file and assign it to a variable
* Convert to lower case
* Split into tokens
* remove stopwords

"Stop" words are sometimes called filler words: they are the common words that don't add much meaning to a sentence.

```python
import re
from nltk.tokenize import word_tokenize

f = open("origin-intro.txt") # open file
contents = f.read()          # add file contents to variable
contents = contents.lower()  # lower case text
contents = re.sub(r'[^\w\s]','',contents)  #remove punctuation (note use of regex)
tokenized_word=word_tokenize(contents)

filtered_word=[]

for w in tokenized_word:
    if w not in stop_words:
        filtered_word.append(w)
print("Filterd Words:",filtered_word)
```

### Further functions and libraries

Working through the notebook, running code and downloading libraries as required, I was able to easily clean blocks of text; tokenize and count words; plot frequency distributions; tag parts of speech; identify common bigrams and n-grams (word pairs and n-word groups).

### Fun with Trump

A delightful bit of fun was had analysing President Trump's Tweets using this code to fetch the text:

```python
import csv
import urllib.request

url = 'https://learn.edina.ac.uk/intro-ta/files/trump-tweet-archive.csv' # download the file
csv = urllib.request.urlopen(url).read() # assign the contents of the file to a variable (csv)
with open('tweets.csv', 'wb') as file: # create a new file and save the contents of 'csv' to this file
    file.write(csv)
    
    print('CSV file created')
```

What do you think was the top 4-gram in all of this data?

> make america great again! 390

Of course it was. 

### Conclusion

This was a very nice way to run through a tutorial notebook and learn a few tricks in python for text analysis, with support running in the background if I needed it. The format is powerful; it focuses you on the task within the time window allocated and helps you avoid distractions. Although it's self-study (and as such relies on good quality materials in the first place), it's OK to play a bit too, because there's help at hand if you come unstuck. Well done, [CDCS](https://www.cdcs.ed.ac.uk/training).