---
layout: single
title: "Plot histograms of raster values in R"
excerpt: "This lesson introduces the raster geotiff file format - which is often used
to store lidar raster data. We cover the 3 key spatial attributes of a raster dataset
including Coordinate reference system, spatial extent and resolution."
authors: ['Leah Wasser']
modified: '2017-06-15'
category: [course-materials]
class-lesson: ['intro-lidar-raster-r']
permalink: /course-materials/earth-analytics/week-3/plot-raster-histograms-r/
nav-title: 'Plot raster histograms'
week: 3
course: "earth-analytics"
sidebar:
  nav:
author_profile: false
comments: false
order: 2
topics:
  reproducible-science-and-programming:
  remote-sensing: ['lidar']
  earth-science: ['vegetation']
  spatial-data-and-gis: ['raster-data']
---


{% include toc title="In This Lesson" icon="file-text" %}

<div class='notice--success' markdown="1">

## <i class="fa fa-graduation-cap" aria-hidden="true"></i> Learning Objectives

After completing this tutorial, you will be able to:

* Open a lidar raster dataset in `R`.
* Be able to list and define 3 spatial attributes of a raster dataset: extent, crs and resolution.
* Be able to identify the resolution of a raster in `R`.
* Be able to plot a lidar raster dataset in `R`.

## <i class="fa fa-check-square-o fa-2" aria-hidden="true"></i> What You Need

You will need a computer with internet access to complete this lesson.

If you have not already downloaded the week 3 data, please do so now.
[<i class="fa fa-download" aria-hidden="true"></i> Download Week 3 Data (~250 MB)](https://ndownloader.figshare.com/files/7446715){:data-proofer-ignore='' .btn }

</div>

In the last lesson, we discussed 3 key attributes of a raster dataset:

1. Spatial resolution
2. Spatial extent and
3. Coordinate reference systems

In this lesson, we will learn how to use histograms to better understand the
distribution of our data.




## Open Raster Data in R

To work with raster data in `R`, we can use the `raster` and `rgdal` packages.
Remember we can use the `raster()` function to import the raster object into R.


```r
# load libraries
library(raster)
library(rgdal)

# Make sure your working directory is set to  wherever your 'earth-analytics' dir is
# setwd("earth-analytics-dir-path-here")

# open raster data
lidar_dem <- raster(x="data/week3/BLDR_LeeHill/pre-flood/lidar/pre_DTM.tif")

# plot raster data
plot(lidar_dem,
     main="Digital Elevation Model - Pre 2013 Flood")
```

<img src="{{ site.url }}/images/rfigs/course-materials/earth-analytics/week03/lidar-raster-intro/2017-02-01-raster05-plot-raster-histograms-r/load-libraries-1.png" title="digital surface model raster plot" alt="digital surface model raster plot" width="100%" />

## Raster Histograms - distribution of elevation values

The histogram below represents the distribution of pixel elevation values in our
data. This plot is useful to:

1. Identify outlier data values
2. Assess the min and max values in our data
3. Explore the general distribution of elevation values in the data - i.e. is the area generally flat, hilly, is it high elevation or low elevation.

Notice that we are using the `xlab` and `ylab`
arguments  in our plot to label our plot axes.


```r
# plot histogram
hist(lidar_dem,
     main="Distribution of surface elevation values",
     xlab="Elevation (meters)", ylab="Frequency",
     col="springgreen")
```

<img src="{{ site.url }}/images/rfigs/course-materials/earth-analytics/week03/lidar-raster-intro/2017-02-01-raster05-plot-raster-histograms-r/view-hist-1.png" title="histogram of DEM elevation values" alt="histogram of DEM elevation values" width="100%" />

## What does a histogram tell us?

A histogram shows us how the data are distributed. Each bin or bar in the plot
represents the number or frequency of pixels that fall within the range specified
by the bin.

We can use the `breaks=` argument to specify fewer or more breaks in our histogram.
Note that this argument does not result in the exact number of breaks that you may
want in your histogram.


```r
# plot histogram
hist(lidar_dem,
     breaks=3,
     main="Distribution of surface elevation values with breaks",
     xlab="Elevation (meters)", ylab="Frequency",
     col="springgreen")
```

<img src="{{ site.url }}/images/rfigs/course-materials/earth-analytics/week03/lidar-raster-intro/2017-02-01-raster05-plot-raster-histograms-r/view-hist2-1.png" title="histogram of DEM elevation values" alt="histogram of DEM elevation values" width="100%" />

Alternatively, we can specify specific break points that we want `R` to use when it
bins the data.

`breaks=c(1600, 1800, 2000, 2100)`

In this case, `R` will count the number of pixels that occur within each value range
as follows:

bin 1: number of pixels with values between 1600-1800
bin 2: number of pixels with values between 1800-2000
bin 3: number of pixels with values between 2000-2100



```r
# plot histogram
hist(lidar_dem,
     main="Distribution of surface elevation values",
     breaks=c(1600, 1800, 2000, 2100),
     xlab="Elevation (meters)", ylab="Frequency",
     col="wheat3")
```

<img src="{{ site.url }}/images/rfigs/course-materials/earth-analytics/week03/lidar-raster-intro/2017-02-01-raster05-plot-raster-histograms-r/view-hist3-1.png" title="histogram of DEM elevation values" alt="histogram of DEM elevation values" width="100%" />

<div class="notice--warning" markdown="1">

## <i class="fa fa-pencil-square-o" aria-hidden="true"></i> In-class challenge - import DSM

* Import the file: `data/week3/BLDR_LeeHill/pre-flood/lidar/pre_DSM_hill.tif`

Plot the data and a histogram of the data. What do the elevations in the DSM
represent? Are they different from the DTM? Discuss this with your neighbor.

* What is the CRS and spatial resolution for this dataset? What units is the spatial
resolution in?
<!-- Yes - they are the same for both files you can figure this out using
crs() and xres()  / yres() -->

</div>

<img src="{{ site.url }}/images/rfigs/course-materials/earth-analytics/week03/lidar-raster-intro/2017-02-01-raster05-plot-raster-histograms-r/class-challenge-1.png" title="DSM histogram and plot" alt="DSM histogram and plot" width="100%" /><img src="{{ site.url }}/images/rfigs/course-materials/earth-analytics/week03/lidar-raster-intro/2017-02-01-raster05-plot-raster-histograms-r/class-challenge-2.png" title="DSM histogram and plot" alt="DSM histogram and plot" width="100%" />

<div class="notice--info" markdown="1">

## Additional Resources

### About Coordinate Reference Systems

* <a href="http://spatialreference.org/ref/epsg/" target="_blank"> A comprehensive online library of CRS information.</a>
* <a href="http://docs.qgis.org/2.0/en/docs/gentle_gis_introduction/coordinate_reference_systems.html" target="_blank">QGIS Documentation - CRS Overview.</a>
* <a href="https://source.opennews.org/en-US/learning/choosing-right-map-projection/" target="_blank">Choosing the Right Map Projection.</a>
* <a href="https://www.nceas.ucsb.edu/~frazier/RSpatialGuides/OverviewCoordinateReferenceSystems.pdf" target="_blank"> NCEAS Overview of CRS in R.</a>

</div>
