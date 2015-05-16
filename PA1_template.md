# Reproducible Research: Peer Assessment 1

Github repo: https://github.com/Begmon/RepData_PeerAssessment1


## Loading and preprocessing the data

```r
file <- './activity.csv'
data <- read.csv(file, header = TRUE)
data_no_na <- data[complete.cases(data), ]
```


## What is mean total number of steps taken per day?

1. Make a histogram of the total number of steps taken each day. Using the data ```data_no_na``` with the NA removed.


```r
library(plyr)
data_sum <- ddply(data_no_na,.(date=as.Date(data_no_na$date)),function(x) c(sumsteps=sum(x$steps))) 
barplot(data_sum$sumsteps, names.arg=data_sum$date, xlab='date', ylab='sum steps')
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 

2. Calculate and report the mean and median total number of steps taken per day

```r
mean(data_sum$sumsteps)
```

```
## [1] 10766.19
```

```r
median(data_sum$sumsteps)
```

```
## [1] 10765
```

## What is the average daily activity pattern?

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


## Imputing missing values

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

2. Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

3. Create a new dataset that is equal to the original dataset but with the missing data filled in.

Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

## Are there differences in activity patterns between weekdays and weekends?
1. Create a new factor variable in the dataset with two levels -- "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.

2. Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). The plot should look something like the following, which was created using simulated data:
