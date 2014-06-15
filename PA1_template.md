#Reproducible Research: Peer Assessment 1
========================================================

This document contains code and outcomes for the first Peer Assessment assignment for the course Reproducible Research. The data used is from an activity monitoring device.

## Loading and preprocessing the data

```r
fullData <- read.csv("activity.csv", stringsAsFactors=F)
install.packages("date")
```

```
## Installing package into 'C:/Users/hhessel/Documents/R/win-library/3.1'
## (as 'lib' is unspecified)
```

```
## Error: trying to use CRAN without setting a mirror
```

```r
library(date)
fullData$date <- as.Date(fullData$date, format = "%Y-%m-%d")
```

## What is mean total number of steps taken per day?

```r
stepsByDate <- by(fullData$steps, fullData$date, sum)
hist(stepsByDate, xlab="Steps", main="Total Steps by Day", xlim=c(0,25000), breaks=8)
```

![plot of chunk meanSteps](figure/meanSteps.png) 

```r
myMean <- mean(stepsByDate, na.rm=TRUE)
myMedian <- median(stepsByDate, na.rm=TRUE)
```
The mean total number of steps per day is 1.0766 &times; 10<sup>4</sup>
The median number of steps per day is 10765

## What is the average daily activity pattern?

```r
stepsByInterval <- aggregate(steps~interval, data=fullData, mean, na.rm=TRUE)
plot(stepsByInterval$steps~stepsByInterval$interval, type="l", ylab="Daily Average Steps", xlab="Interval")
```

![plot of chunk dailyActivity](figure/dailyActivity.png) 

```r
mostSteps <- stepsByInterval$interval[which.max(stepsByInterval$steps)]
```
The interval with the maximum number of steps is 835

## Imputing missing values




