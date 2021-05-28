---
layout: post
title: Reading iCal in R
date: 2021-05-26
# description: 
img: R0000956.jpg
fig-caption: Langholm
fig-attrib: Nick Hood
published: yes
tags:
- R
- Data
- Software
- iCal
- Configuration Management
- CPD

# permalink:
---
Being organised is an important habit for anyone in these days of scope creep -- the tendency for more and more to be done as part of the job. We're all trying to maximise our capacity, so eliminating duplication of effort is one way to avoid wasting time doing unnecessary admin. Productivity tools like email and calendars have replaced the memo and diary of pre-Internet days, but there are many brands and infrastructures, often competing with each other. The result can be that we end up keeping several email accounts, and several calendars with the inevitable double booking and confusion.

My policy is wherever possible to keep one master data source: documents are configuration managed and stored safely, checked out and checked in when updated and with a visible, reversible change history. Calendars for each project are aggregated in a suitable viewer from master files in [iCal](https://en.wikipedia.org/wiki/ICalendar) format, allowing them to be easily shared and syndicated.

Planning for next academic year, I wanted to display a simple GANTT chart for students of the overall course structure. This, because I had previously been duplicating weekly details from the master calendar. I wanted a way to automatically generate mini-GANTTs for each week in the Virtual Learning Environment (VLE) from the course calendar. Here's how I did it: the VLE is written and published in [Bookdown](https://bookdown.org/).

Fortunately, there is already a [package](https://cran.r-project.org/package=calendar) for reading and manipulating iCal files. You may need to install this first.

```r
> install.packages("calendar")
```

So, firstly we want to grab data from the iCal feed. This is the path to an `.ics` file or the ical data for the calendar: make sure it's not just a link to a web interface for the calendar.

```r
> mydat <- readLines("https://www.gov.uk/bank-holidays/england-and-wales.ics")
```

It's worth checking that this has returned something useful: the `head()` function returns the first few lines and an iCal file should look something like this:

```r
> head(mydat)
[1] "BEGIN:VCALENDAR"                     
[2] "VERSION:2.0"                         
[3] "METHOD:PUBLISH"                      
[4] "PRODID:-//uk.gov/GOVUK calendars//EN"
[5] "CALSCALE:GREGORIAN"                  
[6] "BEGIN:VEVENT"       
> 
```

We can use `ic_dataframe()` to organise this flat file into something more structured, again peeking in at the first few column header names in the data frame:

```r
> mydf <- ic_dataframe(mydat)
> head(names(mydf))
[1] "DTEND;VALUE=DATE"   "DTSTART;VALUE=DATE" "SUMMARY"           
[4] "UID"                "SEQUENCE"           "DTSTAMP"                          
> 
```
Selecting the information you need from that is a matter of applying filters. A new data frame using the first 3 columns:

```r
> set1 <- data.frame(mydf["DTSTART;VALUE=DATE"],mydf["SUMMARY"])
> head(set1)
  DTSTART.VALUE.DATE                SUMMARY
1         2016-01-01         New Year’s Day
2         2016-03-25            Good Friday
3         2016-03-28          Easter Monday
4         2016-05-02 Early May bank holiday
5         2016-05-30    Spring bank holiday
6         2016-08-29    Summer bank holiday
```
Selecting only Jubilee holidays using the logical form of `grep`:

```r
> set2 <- subset(set1,grepl("Jubilee",set1$SUMMARY))
> head(set2)
   DTSTART.VALUE.DATE                       SUMMARY
54         2022-06-03 Platinum Jubilee bank holiday
```
Adding new headings using `setnames` from the `data.table` library, then removing row numbers and displaying as a table.

```r
library(data.table)
setnames(set1, c("Date","Event name"))
set2 <- subset(set1,grepl("2022",set1$Date))
knitr::kable(set2[order(set2$From),], caption = '2022 Holiday Calendar', row.names = FALSE)

```

Which will yield a table in your book(down):

Table 1: 2022 Holiday Calendar

Date|Holiday
---|----
2022-01-03|New Year’s Day
2022-04-15|Good Friday
2022-04-18|Easter Monday
2022-05-02|Early May bank holiday
2022-06-02|Spring bank holiday
2022-06-03|Platinum Jubilee bank holiday
2022-08-29|Summer bank holiday
2022-12-26|Boxing Day
2022-12-27|Christmas Day

## Conclusion 
I now have a way of automatically updating the calendar in the VLE for my course, my only having to rebuild the site after a change in the master calendar. This is hugely useful within my workflow and reduces the risk of redundancy or error when there is more than one master. Next steps are to make this produce a GANTT chart.

<!--## Footnotes-->
