---
title: "E-TRAINEE Temporal information in satellite data"
description: "This is the second theme within the Satellite Multispectral Images Time Series Analysis module."
dateCreated: 2021-04-06
authors:
contributors: 
estimatedTime: "1"
---

## Prerequisites
For working on this theme, you need:
- basic R skills
- R packages -TODO: Module 2 R environment/project setup tutorial-


# Temporal information in satellite data

As you know from the previous theme, no other level of data acquisition allows for analysis at regular intervals from the beginning of work of the instrument than the satellite level. This results in a collection of **huge amounts of data**, e.g. Landsat has collected more than 8 million scenes of Earth since the start of the mission. So here we would like to present the potential of the multitemporal aspect of a large volume of such data in Earth observation analysis.

## Objectives

After reading through theoretical contents this theme you will learn how to:<br>
- [indicate satellite sensors with high or low temporal resolution](#resolution)<br>
- [recognize the types of multitemporal analysis](#temporal-analysis)<br>
- [list key aspects of satellite time series data analysis](#aspects)<br>
- [divide satellite data into categories depending on temporal resolution](#monitoring)<br>
- [define different types of changes on satellite data](#changes)<br>
- [address uncertainty in the results](#uncertainty)<br>
- [differentiate several change detection algorithms](#methods)<br>


After performing the [exercise](#exercise) in this theme you will be able to:
- identify date of change based on visual image interpretation and spectral indices values
- recognise change agents based on spectral indices values
- recreate presented steps to prepare your own reference dataset


## Temporal resolution of selected sensors {#resolution}

The temporal resolution of satellite data from different sensors depends on the type of orbit on which the satellite is placed. Geostationary satellite systems continuously acquire images of the same part of the globe, so multiple data acquisitions can occur even on the same day or even within a few minutes. Examples of such systems are meteorological satellites such as Meteosat and NOAA. Another class of satellites includes systems orbiting in polar orbits, like Landsat or SPOT missions. In their case, time resolution is defined as the time the satellite revisits the same part of a given area. Typically, it takes between one day and half a month for a satellite in polar orbit to make another acquisition. This time can be reduced by placing several satellites with twin sensor parameters in the same polar orbit, like in case of Sentinel-2.

Overview of temporal resolution of selected satellite sensors is presented in Figure 1 below.





## Satellite data archives

* EarthExplorer, ESA etc.

## Types of temporal analysis

* intra-annual, year-to-year, multi-year

Depending on temporal resolution of satellite data and its time range multitemporal analysis can be divided in following categories:
- intra-annual - analysed data are acquired within the same year (e.g. analysis of phenological changes in one season),
- inter-annual (year-to-year) - analysed data are acquired in two different years with any interval  (e.g. analysis of the hurricane or flood effects),
- inter-annual (multi-year) - analysed data are acquired in more than two different years with any interval  (e.g. analysis of the pest infestation or climate change effects).


## Types of changes on satellite data

* definitions of abrupt, gradual changes

Temporal-scale changes in satellite time series data can be abrupt and gradual, where the first one refers to short-term, large magnitude, and the second one refers to long-term, small magnitude date-to-date changes (Zhu 2017). Abrupt changes can be caused by disturbance agents such as fires, floods or deforestation. Gradual changes can be caused by climate changes or land management.

There are also seasonal changes related to plant phenology. 

## Monitoring of change types and difference in spectral trajectory in time series

## Uncertainty of change analysis


## Methods

Lorem ipsum...


## Examples 

e.g. from literature 

Zhu, Z., 2017, Change detection using landsat time series: A review of frequencies, preprocessing, algorithms, and applications. ISPRS Journal of Photogrammetry and Remote Sensing, 130, 370-384.




## Exercise 

Assigning change agent to the spectral trajectory in [QGIS](../../software/software_qgis.md).


### Next unit
Proceed with [Image processing workflow](../03_image_processing/03_image_processing.md)
