---
title: "PA1_templateYB"
author: "Yoram Barak"
date: "2024-03-15"
output: html_document
editor_options: 
  markdown: 
    wrap: 72
    keep md
---

# **Reproducible Research Project 1**

# **Introduction**

It is now possible to collect a large amount of data about personal movement using activity monitoring devices such as a Fitbit , Nike Fuelband , or Jawbone Up . These type of devices are part of the “quantified self” movement – a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. But these data remain under-utilized both because the raw data are hard to obtain and there is a lack of statistical methods and software for processing and interpreting the data.

This assignment makes use of data from a personal activity monitoring device. This device collects data at 5 minute intervals through out the day. The data consists of two months of data from an anonymous individual collected during the months of October and November, 2012 and include the number of steps taken in 5 minute intervals each day.

The data for this assignment can be downloaded from the course web site:

Dataset: Activity monitoring data [52K]

The variables included in this dataset are:

steps: Number of steps taking in a 5-minute interval (missing values are coded as NA NA)

date: The date on which the measurement was taken in YYYY-MM-DD format

interval: Identifier for the 5-minute interval in which measurement was taken

The dataset is stored in a comma-separated-value (CSV) file and there are a total of 17,568 observations in this dataset.

## ***Assignment***

This assignment will be described in multiple parts. You will need to write a report that answers the questions detailed below. Ultimately, you will need to complete the entire assignment in a single R markdown document that can be processed by knitr and be transformed into an HTML file.

Throughout your report make sure you always include the code that you used to generate the output you present. When writing code chunks in the R markdown document, always use echo = TRUE echo = TRUE so that someone else will be able to read the code. This assignment will be evaluated via peer assessment so it is essential that your peer evaluators be able to review the code for your analysis.

For the plotting aspects of this assignment, feel free to use any plotting system in R (i.e., base, lattice, ggplot2)

Fork/clone the GitHub repository created for this assignment . You will submit this assignment by pushing your completed files into your forked repository on GitHub. The assignment submission will consist of the URL to your GitHub repository and the SHA-1 commit ID for your repository state.

NOTE: The GitHub repository also contains the dataset for the assignment so you do not have to download the data separately.

Loading and preprocessing the data Show any code that is needed to

Load the data (i.e. read.csv() read.csv())

Process/transform the data (if necessary) into a format suitable for your analysis

-   What is mean total number of steps taken per day? For this part of the assignment, you can ignore the missing values in the dataset.

-   Calculate the total number of steps taken per day

-   If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day

-   Calculate and report the mean and median of the total number of steps taken per day

-   What is the average daily activity pattern? Make a time series plot (i.e. type = “l” type = “l”) of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

-   Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

-   Imputing missing values Note that there are a number of days/intervals where there are missing values (coded as NA NA). The presence of missing days may introduce bias into some calculations or summaries of the data.

-   Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NA NAs)

-   Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

-   Create a new dataset that is equal to the original dataset but with the missing data filled in.

-   Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

-   Are there differences in activity patterns between weekdays and weekends? For this part the weekdays() weekdays() function may be of some help here. Use the dataset with the filled-in missing values for this part.

    -   Create a new factor variable in the dataset with two levels – “weekday” and “weekend” indicating whether a given date is a weekday or weekend day.

    -   Make a panel plot containing a time series plot (i.e. type = “l” type = “l”) of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.

# Assignment answers: Loading and preprocessing the data

### Load the data

`activity_data <- read.csv("activity.csv")`

### Check the structure of the data for integrity

`str(activity_data)`

### Check for missing values

`sum(is.na(activity_data$steps))`

### Calculate the total number of steps taken per day (ignoring missing values)

`total_steps_per_day <- tapply(activity_data$steps, activity_data$date, sum, na.rm = TRUE)`

### Calculate the mean and median of the total number of steps taken per day

`mean_steps_per_day <- mean(total_steps_per_day)`

`median_steps_per_day <- median(total_steps_per_day)`

####Anaswer -

mean_total_steps

[1] 10766.19

median_steps_per_day

[1] 10765

### Make a histogram of the total number of steps taken each day

`hist(total_steps_per_day, main = "Histogram of Total Steps per Day", xlab = "Total Steps per Day", ylab = "Frequency", col = "lightblue")`

![](images/clipboard-3021353525.png)

### Calculate the average daily activity pattern

`average_steps_by_interval <- tapply(activity_data$steps, activity_data$interval, mean, na.rm = TRUE)`

### Plot the average daily activity pattern

`plot(names(average_steps_by_interval), average_steps_by_interval, type = "l", xlab = "5-minute Interval", ylab = "Average Number of Steps", main = "Average Daily Activity Pattern")`

![](images/clipboard-2665184310.png)

### Find the 5-minute interval with the maximum average number of steps

`max_interval <- which.max(average_steps_by_interval) max_steps <- max(average_steps_by_interval)`

#### The maximum average number of steps for 5-minute interval:

```         
> max_interval 835  104 
```

### Impute missing values

`activity_data_imputed <- activity_data activity_data_imputed$steps[is.na(activity_data_imputed$steps)] <- mean(activity_data_imputed$steps, na.rm = TRUE)`

### Calculate the total number of missing values in the dataset

`total_missing_values <- sum(is.na(activity_data$steps))`

### Make a histogram of the total number of steps taken each day with imputed missing values

`total_steps_per_day_imputed <- tapply(activity_data_imputed$steps, activity_data_imputed$date, sum) hist(total_steps_per_day_imputed, main = "Histogram of Total Steps per Day (Imputed)", xlab = "Total Steps per Day", ylab = "Frequency", col = "lightblue")`

![](images/clipboard-3944004247.png)

### Calculate the mean and median total number of steps taken per day with imputed missing values

`mean_steps_per_day_imputed <- mean(total_steps_per_day_imputed) median_steps_per_day_imputed <- median(total_steps_per_day_imputed)`

|     |
|-----|
|     |

### Are there are differences in activity patterns between weekdays and weekends

`activity_data_imputed$date <- as.Date(activity_data_imputed$date) activity_data_imputed$day <- weekdays(activity_data_imputed$date) activity_data_imputed$day_type <- ifelse(activity_data_imputed$day %in% c("Saturday", "Sunday"), "weekend", "weekday")`

### Calculate the average number of steps per interval for weekdays and weekends

`average_steps_by_interval_weekday <- tapply(activity_data_imputed$steps[activity_data_imputed$day_type == "weekday"], activity_data_imputed$interval[activity_data_imputed$day_type == "weekday"], mean) average_steps_by_interval_weekend <- tapply(activity_data_imputed$steps[activity_data_imputed$day_type == "weekend"], activity_data_imputed$interval[activity_data_imputed$day_type == "weekend"], mean)`

### Create a panel plot for weekdays and weekends

`par(mfrow = c(2, 1), mar = c(4, 4, 2, 1)) # Set bottom, left, top, right margins`

### Plot for weekdays

`plot(names(average_steps_by_interval_weekday), average_steps_by_interval_weekday, type = "l", xlab = "5-minute Interval", ylab = "Average Number of Steps", col = "blue", main = "Average Number of Steps - Weekdays")`

### Add legend for weekdays

`legend("topright", legend = "Weekdays", col = "blue", lty = 1, cex = 0.8, xpd = TRUE)`

### Plot for weekends

`plot(names(average_steps_by_interval_weekend), average_steps_by_interval_weekend, type = "l", xlab = "5-minute Interval", ylab = "Average Number of Steps", col = "red", main = "Average Number of Steps - Weekends")`

### Add legend for weekends

`legend("topright", legend = "Weekends", col = "red", lty = 1, cex = 0.8, xpd = TRUE)`

![](images/clipboard-1664501808.png)

### Reset the plotting layout

`par(mfrow = c(1, 1))`
