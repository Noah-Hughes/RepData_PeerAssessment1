# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data
Unzip file and load while removing NA

```r
stepdata <- read.csv(unz("activity.zip","activity.csv"))
step2 <-na.omit(stepdata)
```


## What is mean total number of steps taken per day?
Calculate the total number of steps taken per day

```r
sums <- aggregate(step2$steps, list(date = step2$date), FUN = sum)
```


If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day

```r
    hist(sums$x, main = "Total Steps per Day", xlab = "Steps per Day", ylab = "Number of Days", col = "red", breaks = 15)
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 


Calculate and report the mean and median of the total number of steps taken per day

```r
mean(sums$x)
```

```
## [1] 10766.19
```

```r
median(sums$x)
```

```
## [1] 10765
```

## What is the average daily activity pattern?
Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
stepmean <- aggregate(step2$steps, list(interval = step2$interval), FUN = mean)

plot.ts(stepmean$interval/100, stepmean$x, type = "l", main = "Average Steps per Day", xlab = "Hour of Day", ylab = "Average Steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png) 

Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
topnumber <- head(sort(stepmean$x, decreasing = TRUE), 1)
toprow <- subset(stepmean, x == topnumber)
toprow
```

```
##     interval        x
## 104      835 206.1698
```

## Imputing missing values
Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

Create a new dataset that is equal to the original dataset but with the missing data filled in.

Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?


## Are there differences in activity patterns between weekdays and weekends?
