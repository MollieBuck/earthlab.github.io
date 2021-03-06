---
layout: single
title: "Using before / after remote sensing images to better understand the impacts of flooding & erosion - Google Earth and the 2013 Colorado floods"
excerpt: "In this lesson, we will use time series imagery from Google Earth to look at the impacts of the floods in Boulder, Colorado. Specifically we will look at spectral remote sensing data before and after the flood to see what changed in the landscape. This lesson requires doesn't require any programming!"
authors: ['Leah Wasser', 'NEON Data Skills']
category: [course-materials]
class-lesson: ['co-floods-1-intro']
permalink: /course-materials/earth-analytics/week-1/co-floods-1-intro/
nav-title: 'Google Earth Time series'
module-nav-title: 'CO Floods Intro'
dateCreated: 2016-12-06
modified: '2017-06-15'
module-title: 'Understand Disturbance With Data - Flooding and Erosion'
module-description: 'This module introduces the concept of using data to Understand
a natural phenomenon. In this case we will explore flooding and erosion. We use a combination of Google Earth imagery, NOAA precipitation data and
USGS stream flow data to begin to quantify and better understand the drivers and impacts of the 2013 flood as it is seen in Boulder, Colorado.
No programming experience is needed to complete this module.'
module-type: 'class'
class-order: 1
course: "earth-analytics"
week: 1
sidebar:
  nav:
author_profile: false
comments: true
order: 1
topics:
  remote-sensing: ['spectral-remote-sensing']
  earth-science: ['flood-erosion']
  time-series:
---


{% include toc title="In This Lesson" icon="file-text" %}

In this classroom activity we will actively engage with different types of data
that scientifically quantify / document the drivers (causes of) and impacts of
the flood using different methods.

<div class='notice--success' markdown="1">

## <i class="fa fa-graduation-cap" aria-hidden="true"></i> Learning Objectives
At the end of this activity, you will be able to:

* Use the timeline function in Google Earth to view time series imagery data
* Illustrate using a schematic graphic, the causes and impacts of a flood.
* Be able to define a driver and an impact of a disturbance.

## <i class="fa fa-check-square-o fa-2" aria-hidden="true"></i> What you need

You will need to download and install Google Earth on your computer and then
download the `.kml` file below.

<a href="https://www.google.com/earth/download/gep/agree.html" target="_blank" class="btn btn-success btn--x-large">
Get Google Earth</a>

<a href="https://ndownloader.figshare.com/files/7005404" class="btn btn-success btn--x-large">
<i class="fa fa-download" aria-hidden="true"></i> Download .kmz file - Locations of Change</a>

</div>

## About the 2013 CO floods

In early September 2013, a slow moving cold air front moved through Colorado
intersecting with a warm, humid air front. The clash between the cold and warm
fronts yielded heavy rain. This rain, combined with a previous record of drought,
conditions associated with the soils in Colorado and other factors yielded and
devastating flooding across the Front Range in Colorado, USA.

<figure>
 <a href="{{ site.baseurl }}/images/course-materials/earth-analytics/week-1/intro-co-floods/N_St_Vrain_before_after_CreditBoulderCo.jpg">
 <img src="{{ site.baseurl }}/images/course-materials/earth-analytics/week-1/intro-co-floods/N_St_Vrain_before_after_CreditBoulderCo.jpg" alt="North St Vrain before and after 2013 flood."></a>
 <figcaption> The St. Vrain River in Boulder County, CO after (left) and before
 (right) the 2013 flooding event.  Source: Boulder County via <a href="http://krcc.org/post/post-flood-planning-boulder-county" target="_blank"> KRCC</a>.
 </figcaption>
</figure>

<iframe width="560" height="315" src="https://www.youtube.com/embed/bUcWERTM-OA?rel=0&loop=1" frameborder="0" allowfullscreen></iframe>

## Use imagery to detect change
Georeferenced imagery, collected using satellites and airplanes provides a powerful
visual record of landscape changes. Google Earth, has a time series feature that
allows you to look at imagery of the earth, across time. Let's have a look at some
of the visible changes.


### How to view time series imagery in Google Earth

* Open Google Earth
* Double click on the `.kmz` file that you downloaded above. It should open in Google Earth.

<i fa fa-star></i>**Tip:** the `.kmz` file may not be automatically associated with Google Earth. If
double clicking doesn't automatically open Google Earth, then Open Google Earth,
go to File --> Open in Google Earth. Navigate to the
location of your downloaded file (`~Documents/data/co-flood/locations`) and open it.
{: .notice--success}

* Once you have the `.kmz` file open, notice it is listed in the Temporary Places section
of the  `places` window. It should automatically zoom you into to an area in North
Boulder, Colorado. If it doesn't double click on the text `Locations of Significant Damage`.
* Click on the show historical imagery button in google earth

<figure>
 <a href="{{ site.baseurl }}/images/course-materials/earth-analytics/week-1/intro-co-floods/google-earth-time.png">
 <img src="{{ site.baseurl }}/images/course-materials/earth-analytics/week-1/intro-co-floods/google-earth-time.png" alt="google earth time series feature."></a>
 <figcaption> The `show historical imagery` button allows you to turn on and slide
 through imagery from various points in time within Google Earth. It is the button
 outlined in pink in the above imaged.
 </figcaption>
</figure>

* When you click on the show historical imagery, a slider will appear in the upper
LEFT hand corner of your window. Scroll back and forth through time to get used
to the slider
* Finally, double click on one of the thumbtacks from locations of significant
damage file. Scroll to 10/2012 and then to 10/2013. Do you see any differences?
* Check out the other thumbtack. What differences do you see?


<div class="notice--warning" markdown="1">

## <i class="fa fa-pencil-square-o" aria-hidden="true"></i> Activity: What changes do you see?

As a group, discuss the following questions. Record your answers following the
directions of your instructor (Google Doc, word document, etherpad, etc.).

* What differences do you see between 2012 and 2013?
  * For each difference: What do you think caused that difference?
  * For each difference: How can you quantitatively record the difference?
* For each CAUSE listed above, could you somehow quantitatively record the "size" or impact of the cause?
* Was the cause - caused by something else (i.e. did something else DRIVE the cause)?
* Create a diagram that illustrates the causes and effects (or drivers and impacts) of the flood. Is it a linear diagram? Is it quantifiable?
</div>
