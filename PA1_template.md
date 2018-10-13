---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---



## Loading and preprocessing the data

```r
library(data.table)
library(lubridate)

#read data, and 
activity <- read.csv("activity.csv", header = TRUE)
activity = na.omit(activity)
activity <- data.table(activity)
activity$date <- ymd(activity$date)
```

## What is mean total number of steps taken per day?


```r
# group by date and sum the steps
agg <- aggregate(steps ~ date, activity, sum)
hist(agg$steps, main = "Total Steps per Day", col = "brown", xlab = "Steps")
```

![](PA1_template_files/figure-html/Histogram-1.png)<!-- -->

# Mean and Median

```r
meanSteps <- mean(agg$steps, na.rm = TRUE)
medSteps <- median(agg$steps, na.rm = TRUE)
```
The mean of the total number of steps is **10766.1886792453**.  
The median of the total number of steps is **10765**.


## What is the average daily activity pattern?

```r
avgSteps <- aggregate(steps ~ interval, activity, mean)
plot(avgSteps$interval, avgSteps$steps, type = "l", xlab = "Interval", ylab = "Average Steps", 
     main = "Average Daily Activity", col = "brown")
```

![](PA1_template_files/figure-html/AvgSteps-1.png)<!-- -->

```r
# max # of avg steps
maxSteps <- max(avgSteps$steps)
maxSteps <- format(round(maxSteps, 2), nsmall = 2)
maxInterval <- subset(avgSteps, steps == max(steps))$interval
```
The interval **835** contains the maximum number of steps **206.17**.

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
