---
layout: single
title: "Work with Precipitation Data in R - 2013 Colorado Floods"
excerpt: "This lesson provides students with an example of a data driven report to emphasize the importance of connecting data, documentation and results."
authors: ['Leah Wasser', 'NEON Data Skills']
modified: '2017-06-15'
category: [course-materials]
class-lesson: ['co-floods-1-intro']
permalink: /course-materials/earth-analytics/week-1/co-floods-data-example-r/
nav-title: 'CO Floods Data Example'
week: 1
sidebar:
  nav:
author_profile: false
comments: true
course: "earth-analytics"
order: 2
topics:
  earth-science: ['flood-erosion']
  time-series:
---


{% include toc title="In This Lesson" icon="file-text" %}

Several factors contributed to extreme flooding that occurred in Boulder,
Colorado in 2013. In this lesson we will check our a report that provides some
information about the event.

<div class='notice--success' markdown='1'>

## <i class="fa fa-graduation-cap" aria-hidden="true"></i> Learning Objectives

After completing this tutorial, you will be able to:

* List some of the components of a project that make it more easily reusable (reproducible) to you when working with other people


## <i class="fa fa-check-square-o fa-2" aria-hidden="true"></i> What you need

You will need a computer with internet access to complete this activity.

</div>

## A data report

Your colleague put together the very informative data report below. The topic of
the report is the 2013 Colorado floods. Examine the report. Then answer the questions
below.


1. What sources of data were used to create the plots?
2. How were the data processed?
3. How did your colleague generate this report? When was it last updated?
4. Who contributed to this report?
5. You'd like to make some changes to the report - can you do that easily? If you
wanted to make changes, what process and tools would you use to make those changes?
6. What units are the precipitation data in?
7. Create a list of the things that would make editing this report easier.


***

## My Report - 2013 Colorado Flood Data

Precipitation Data

A lot of rain impacted Colorado. See below.



<img src="{{ site.url }}/images/rfigs/course-materials/earth-analytics/week01/co-floods-1-intro/2016-12-06-erosion-02-precip-discharge-r-example/daily-summaries-1.png" title="plot 1" alt="plot 1" width="100%" />

## Fall 2013 Precipitation

Let's check out the data for a few months.


<img src="{{ site.url }}/images/rfigs/course-materials/earth-analytics/week01/co-floods-1-intro/2016-12-06-erosion-02-precip-discharge-r-example/subset-data-1.png" title="plot 2 precip" alt="plot 2 precip" width="100%" />


<img src="{{ site.url }}/images/rfigs/course-materials/earth-analytics/week01/co-floods-1-intro/2016-12-06-erosion-02-precip-discharge-r-example/all-boulder-station-data-1.png" title="plot 3 discharge" alt="plot 3 discharge" width="100%" />
