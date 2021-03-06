---
layout: single
title: "Visualizing hourly traffic crime data for Denver, Colorado using R, dplyr, and ggplot"
date: 2016-12-06
authors: [Max Joseph]
category: [tutorials]
excerpt: 'This tutorial demonstrates how to access and visualize crime data for Denver, Colorado.'
sidebar:
nav:
author_profile: false
comments: true
lang: [r]
lib: [dplyr, ggplot2, lubridate, viridis, RCurl]
---

The city of Denver publicly hosts crime data from the past five years in their open data catalog. In this tutorial, we will use R to access and visualize these data, which are essentially spatiotemporally referenced points with features for type of crime, neighborhood, etc.

First, we will load some packages that we'll use later.

``` r
library(dplyr)
library(ggplot2)
library(lubridate)
library(viridis)
library(RCurl)
```

Then, we need to download a comma separated values file that contains the raw data.

``` r
data_url <- "http://data.denvergov.org/download/gis/crime/csv/crime.csv"
data <- getURL(data_url, ssl.verifypeer = 0L, followlocation = 1L)
d <- read.csv(text = data)
```

Let's lowercase the column names, and look at the structure of the data with the `str()` function.

``` r
names(d) <- tolower(names(d))
str(d)
```

    ## 'data.frame':    450928 obs. of  19 variables:
    ##  $ incident_id           : num  2.01e+09 2.01e+09 2.01e+09 2.01e+09 2.01e+09 ...
    ##  $ offense_id            : num  2.01e+15 2.01e+15 2.01e+15 2.01e+15 2.01e+15 ...
    ##  $ offense_code          : int  5420 5499 5312 5313 1315 5016 5420 1313 2999 5707 ...
    ##  $ offense_code_extension: int  0 2 0 0 0 0 0 2 1 0 ...
    ##  $ offense_type_id       : chr  "traffic-accident-dui-duid" "vehicular-eluding-no-chase" "disturbing-the-peace" "curfew" ...
    ##  $ offense_category_id   : chr  "traffic-accident" "all-other-crimes" "public-disorder" "public-disorder" ...
    ##  $ first_occurrence_date : chr  "2014-06-29 01:19:59" "2014-06-29 01:50:59" "2014-06-29 02:00:00" "2014-06-29 02:03:59" ...
    ##  $ last_occurrence_date  : chr  "" "" "" "" ...
    ##  $ reported_date         : chr  "2014-06-29 02:00:59" "2014-06-29 01:54:00" "2014-06-29 02:00:00" "2014-06-29 02:17:59" ...
    ##  $ incident_address      : chr  "" "N YOSEMITE ST / E 14TH AVE" "545 S CLAY ST" "" ...
    ##  $ geo_x                 : num  3140557 3173049 3134848 3140115 3135509 ...
    ##  $ geo_y                 : num  1696907 1694538 1682641 1705557 1672647 ...
    ##  $ geo_lon               : num  -105 -105 -105 -105 -105 ...
    ##  $ geo_lat               : num  39.7 39.7 39.7 39.8 39.7 ...
    ##  $ district_id           : int  1 2 4 1 4 6 1 6 1 2 ...
    ##  $ precinct_id           : int  123 223 412 112 422 622 122 611 112 213 ...
    ##  $ neighborhood_id       : chr  "cbd" "east-colfax" "athmar-park" "sunnyside" ...
    ##  $ is_crime              : int  0 1 1 1 1 1 0 1 1 1 ...
    ##  $ is_traffic            : int  1 0 0 0 0 0 1 0 0 0 ...

The code below uses the `dplyr` package to subset the data to only include traffic accident crimes (`filter(...)`), and parses the date/time column so that we can extract quantities like hour-minutes (to evaluate patterns over the course of one day), the day of week (e.g., 1 = Sunday, 2 = Monday, ...), and year day (what day of the year is it?), creating new columns for these variables with the `mutate()` function.

``` r
accidents <- d %>%
  filter(offense_category_id == "traffic-accident") %>%
  mutate(datetime = ymd_hms(first_occurrence_date, tz = "MST"),
         hm = as.POSIXct(paste(hour(datetime), minute(datetime), sep = ":"),
                         format = "%H:%M"),
         dow = wday(datetime),
         yday = yday(datetime))
```

Last, we will group our data by hour-minute and day of the week, and for each combination of these two quantities, compute the number of traffic accident crimes. Then we'll create a new variable `day`, which is the character representation (Sunday, Monday, ...) of the numeric `dow` column (1, 2, ...). We'll also create a new variable `offense_type`, which is a more human-readable version of the `offense-type-id` column. Using ggplot, we'll create a density plot with a color for each day of week. This workflow uses `dplyr` to munge our data, then pipes the result to `ggplot2`, so that we only create one object in our global environment `p`, which is our plot.

``` r
p <- accidents %>%
  group_by(hm, dow, yday, offense_type_id) %>%
  summarize(n = n()) %>%
  # the call to mutate() makes new variables with better names
  mutate(day = factor(c("Sunday", "Monday", "Tuesday",
                 "Wednesday", "Thursday", "Friday",
                 "Saturday")[dow],
                 levels = c("Monday", "Tuesday",
                            "Wednesday", "Thursday", "Friday",
                            "Saturday", "Sunday")),
         offense_type = ifelse(
           offense_type_id == "traffic-accident-hit-and-run",
           "Hit and run",
           ifelse(
             offense_type_id == "traffic-accident-dui-duid",
             "Driving under the influence", "Traffic accident"))) %>%
  ggplot(aes(x = hm,
             fill = day,
             color = day)) +
  geom_freqpoly(binwidth = 60 * 30) + # 60 sec/min * 30 min
  scale_color_viridis(discrete = TRUE, "", direction = -1) +
  scale_fill_viridis(discrete = TRUE, "", direction = -1) +
  xlab("Time of day") +
  ylab("Frequency") +
  ggtitle("Traffic crimes in Denver, Colorado") +
  scale_x_datetime(date_breaks = "4 hours", date_labels = "%H:%M")
p
```

![Traffic accident data for each hour in Denver, CO](/images/visualize-denver-colorado-traffic-crime_files/plot-hourly-1.png)

This dplyr to ggplot approach is extremely modular. If we wanted to see this plot for each type of traffic accident crime, we could do so simply by adding one statement.

``` r
p + facet_wrap(~ offense_type, ncol = 1, scales = "free_y")
```

![Traffic crime data by type](/images/visualize-denver-colorado-traffic-crime_files/facet-by-group-1.png)
