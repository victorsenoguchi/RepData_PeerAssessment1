---
title: "Reproducible Research: Peer Assessment 1"
author: "Victor Borges"
date: "25/01/2021"
output: 
  html_document:
    keep_md: true
---



## Loading and preprocessing the data


```r
data <- read.csv("activity.csv")
complete_data <- data[complete.cases(data),]
stepsPerDay <- aggregate(steps ~ date, complete_data, sum)
```

## What is mean total number of steps taken per day?

stepsPerDay <- aggregate(steps ~ date, complete_data, sum)
hist(stepsPerDay$steps,
     main = "Steps per day",
     xlab = "Steps",
     col = "blue",
     breaks = 8)
meanStepsPerDay <- mean(stepsPerDay$steps)
medianStepsPerDay <- median(stepsPerDay$steps)


## What is the average daily activity pattern?

stepsInterval <- aggregate(steps ~ interval, complete_data, mean)
plot(stepsInterval$interval,
     stepsInterval$steps, 
     type="l", xlab = "5 min - interval", 
     ylab = "Average steps", 
     main = "Average Daily Activity Pattern", 
     col = "blue")
stepsInterval$interval[which.max(stepsInterval$steps)]

## Imputing missing values

nrow(data[is.na(data$steps),])


## Are there differences in activity patterns between weekdays and weekends?


