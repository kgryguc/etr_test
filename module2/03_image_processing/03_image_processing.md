---
title: "E-TRAINEE Image processing workflow"
description: "This is the third theme within the Satellite Multispectral Images Time Series Analysis module."
dateCreated: 2021-04-06
authors:
contributors: 
estimatedTime: 
---

# Image processing workflow

Automating of satellite data processing.


## Objectives

In this theme, you will learn about:
* [Goals of automating processes](#goals-of-automating-processes)<br>
* [Radiometric and geometric calibration](#radiometric-and-geometric-calibration)<br>
* [Different sensors harmonization](#different-sensors-harmonization)<br>
* [Masking processes](#masking-processes)<br>
* [Time composites creation](#time-composites-creation)<br>
* [Overview of R packages dealing with multispectral image processing](#overview-of-R-packages dealing-with-multispectral-image-processing)<br>

After finishing this theme you will be able to complete the process of preparing data for actual use in research. The goal is to present methods and tools that allow fast, reproducible and accurate data processing. 

## Goals of automating processes

* standarization, time saving

## Radiometric and geometric calibration



## Different sensors harmonization

* Landsat TM-OLI, resampling

## Masking processes

* clouds and shadow mask building, spectral index based masks of objects…

## Time composites creation

Results: Concept of time composite ![Concept of time composite](img/composite.png)
Figure X. Concept of creating time composites from three different dates images based on the highest NDVI value.


## Overview of R packages dealing with multispectral image processing


[ASIP: Automated Satellite Image Processing](https://cran.r-project.org/web/packages/ASIP/index.html)
[gdalcubes: Earth Observation Data Cubes from Satellite Image Collections](https://github.com/appelmar/gdalcubes_R)
[geoTS: Methods for Handling and Analyzing Time Series of Satellite Images](https://cran.r-project.org/web/packages/geoTS/index.html)
[landsat: Radiometric and Topographic Correction of Satellite Imagery](https://cran.r-project.org/web/packages/landsat/index.html)
[rsat: Dealing with Multiplatform Satellite Images](https://github.com/ropensci/rsat)
[RGISTools: Handling Multiplatform Satellite Images](https://cran.r-project.org/web/packages/RGISTools/index.html)
[satellite: Handling and Manipulating Remote Sensing Data](https://cran.r-project.org/web/packages/satellite/index.html)


[gapfill:	Fill Missing Values in Satellite Data](https://github.com/florafauna/gapfill)
[dtwSat: Time-Weighted Dynamic Time Warping for Satellite Image Time Series Analysis](https://github.com/vwmaus/dtwSat/)
## Methods

Lorem ipsum...


## Examples 

e.g. from literature 


## Exercise 

Creating analysis ready time-series composition from data downloaded through all presented processing steps using [R](../../software/software_r_language.md) and [QGIS](../../software/software_qgis.md) for visualisation.


### Next unit
Proceed with [Multitemporal classification of vegetation types](../04_multitemporal_classification/04_multitemporal_classification.md)
