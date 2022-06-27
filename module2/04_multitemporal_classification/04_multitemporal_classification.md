# Prerequisites

-   Basic image classification skills  
-   Basic R knowledge

# Multitemporal classification

Automatic supervised classification based on multitemporal datasets has
the potential to improve mapping performance in comparison to
single-date collected data, especially for vegetation classes.

## Objectives

In this theme, you will learn about:

After finishing this theme you will be able to provide the
classification of multitemporal dataset using reference data and
supervised machine learning methods, assess the obtained accuracy as
well as you will know how to indicate which variables were the most
important for the result.

***(bridge with Module 1 - content to be agreed)***

## Objectives

In this theme, you will learn about: \* [Multitemporal reference data
fitted to study aim and image
datasets](#multitemporal-reference-data-fitted-to-study-aim-and-image-datasets)
\* [Machine learning algorithms](#machine-learning-algorithms) \*
[Variable importance as potential to optimize
classification](#variable-importance-as-potential-to-optimize-classification)
\* [Results validation](#results-validation)

After finishing this theme you will be able to provide the
classification of multitemporal dataset using reference data and
supervised machine learning method, assess the obtained accuracy as well
as you will know how to indicate which variables were the most important
for your result.

## Multitemporal reference data fitted to study aim and image datasets

**(bridge with Module 4 - content to be agreed)**

**Reference data sampling** for the time series data classification is a
challenging task. In the ideal situation the reference data comes from
field campaigns performed near the satellite data acquisition dates.
Such a scenario, however, is rather impossible in the case of time
series composed of regularly collected images. In this case it might be
helpful to use additional Very High Resolution data for the analysed
period if available. In the case of Landsat data classification, for
example the use of daily acquired PlanetScope data can enrich the image
interpretation process needed to develop a reference dataset. However,
it should be noted that we should deeply analyse the areas where the
known objects of interest are located (spectral characteristics and
spatial surroundings) in order to check the consistency between
available data in different terms. If the aim of our study is to use
time series data to perform a classification of images from each term
separately, the situation is more clear than when we would like to
develop a multitemporal dataset as input to one classification. In a
such situation to exclude changes between analysed dates, especially
when using data from several years, it is useful to apply **simple
change detection**. This can be achieved by calculating difference
between spectral index values of the actual and previous years
(e.g. pixels with absolute differences of NDVI ≤0.05 flagged as
‘change’; [Immitzer et al., 2019](https://doi.org/10.3390/rs11222599))
or to apply some disturbance detection related algorithm like
e.g. [LandTrendr](https://geotrendr.ceoas.oregonstate.edu/landtrendr/).
Such information can be important in developing a reference set for
classification that is to point to the same constant objects. When using
a wider time range for classification, a data **time series
visualisation tool** such as
[TimeSync](https://www.fs.usda.gov/pnw/tools/timesync-landsat-time-series-visualization-and-data-collection-tool)
or the one you learned in an exercise in [Theme
2](../02_temporal_information/02_temporal_information.md) may be also
useful.

## Machine learning algorithms

**(bridge with Module 1, 3, 4 - content to be agreed)**

The most frequently used supervised machine learning algorithms in
vegetation classification based on multitemporal satellite data are
Random Forest, Support Vector Machines and Artificial Neural Networks
including Deep Learning.

## Selection of the best terms of data acquisition

**(bridge with Module 4 - content to be agreed)**

Depending on the classified object, the date of data acquisition will be
of key importance in the most accurate identification. For example, for
grasslands in Karkonosze Mountains, that begin to discolour in autumn,
September would be the more appropriate time to distinguish them from
their surroundings than other months like August, when they are
spectrally similar to subalpine tall forbs (**Figure 1**).

<p align="center">
<img src="media/fig1_best_terms.png" title="Visual comparison between grasslands and subalpine tall forbs in Karkonosze Mountains based on Sentinel-2 data from the beginning of August and the middle of September (Wakulińska, Marcinkowska-Ochtyra, 2020)." alt="Figure 1" width="1080"/>
</p>

<div align="center">

<b>Figure 1. Visual comparison between grasslands and subalpine tall
forbs in Karkonosze Mountains based on Sentinel-2 data from the
beginning of August and the middle of September ([Wakulińska,
Marcinkowska-Ochtyra, 2020](https://doi.org/10.3390/rs12172696)).</b>

</div>

Indicating the most optimal spectro-temporal data can be done in three
ways: 1. **classifying each image** for each term separately and
assessing the accuracy of each result (**Figure 2A**), 2.
**classification of multitemporal data**, where particular or all terms
are combined into one dataset to increase the potential of the data by
allowing more temporal variability to be used (**Figure 2B**), 3.
**classification of multitemporal data** and **selection** of the **most
important variables** in the classification and then use of the model
with only them (**Figure 2C**).

<p align="center">
<img src="media/fig2_best_terms.png" title="Time-series datasets used for selection of the best term of data acquisition for classification (A - three single-date datasets, B - multitemporal dataset in each possible terms combination, C - the best variables selected from multitemporal dataset)." alt="Figure 2" width="1080"/>
</p>

<div align="center">

<b>Figure 2. Time-series datasets used for selection of the best term of
data acquisition for classification (A - three single-date datasets, B -
multitemporal dataset in each possible terms combination, C - the best
variables selected from multitemporal dataset).</b>

</div>

The first two do not require the use of additional tools, while the last
one uses **feature selection (FS)** methods (see the [next section]().

-   Feature selection as potential to optimise classification

**(bridge with Module 4 - content to be agreed)**

As there are **many variables** involved in the multitemporal
classification (for example, on five Sentinel-2 scenes with selected 10
spectral bands each, there will be 50 variables). This results in a
longer data processing time and may also lead to the inclusion of
correlated bands (carrying similar information in the classification).
Including **additional information** in the form of e.g. spectral or
textural indices may be useful, but it also increases the dataset
([Henrich et al.,
2009](https://www.researchgate.net/publication/259802556_Development_of_an_online_indices_database_Motivation_concept_and_implementation)
proposed 249 indices possible to calculate based on Sentinel-2 data!).
Hence, selecting the most important ones and including only those
selected in the development of the final product can significantly
improve the accuracy of the obtained result. Apart from obtained
accuracies, the data **storage, processing time**, and classification
models **simplicity** is also important, especially in large scale
analysis, so the reduction of the variables number to the most
influential ones makes this classification process more robust.

The advantage of some algorithms is the ability to identify these
variables thanks to the **variable importance metric** calculation
mechanism, e.g. in Random Forest it is based on an average decrease in
accuracy or an average decrease in the Gini coefficient (the higher the
value of the measure, the greater the usefulness of a given variable).
These methods belong to statistical-based **feature selection** methods
estimating the relevance of variables based on statistical measures. The
best datasets can be also assessed by the analysis of differences
between the classification accuracies (overall accuracy, F1 score) by
using **statistical tests** and then selecting only those for which the
differences are statistically significant. There are also other FS
methods, contrary to statistical - **information theory based**, or
grouped into other categories, in general - **supervised/unsupervised,
filter/wrapper** algorithms ([Cao et al.,
2017](https://doi.org/10.1109/lgrs.2017.2755541), [Li et al.,
2017](https://dl.acm.org/doi/pdf/10.1145/3136625). All of them can be
broadly divided into ranking- or search- based methods, where the first
ones are described as more viable for many applications by producing a
ranking of input features ([Sen et al. 2019]()). In this way to evaluate
the most optimal bands/terms selection, **spectral separability
measures** like e.g. [Jeffries-Matusita
distance](https://stackoverflow.com/questions/24762383/spectral-separability-using-jeffries-matusita-distance-method-in-r)
([Swain, Davis, 1978](https://doi.org/10.1109/tpami.1981.4767177)) can
be used. This measure takes values from 0 (low separability) to
approximately 2 (high separability). By doing this on different datasets
we can rank them based on their discriminative power and choose only the
most influential.

The choice of the final variables is user-dependent. It will affect both
the accuracy of the classification and its duration so the compromise
between high accuracy and time-effectiveness of data acquisition and
processing is needed. [Georganos et
al. (2017)](https://doi.org/10.1080/15481603.2017.1408892) proposed a
metric called **classification optimization score** (COS) that rewards
model simplicity and penalises increasing computational time using a
given number of features in the classification model.

## Results validation

**(bridge with Module 3, 4 - content to be agreed)**

Validation of multitemporal classification results is often not very
straightforward and different strategies can be implemented to validate
it quantitatively. It can be performed as follows: visual images
interpretation the use of existing maps or databases from inventories
whole reference dataset split or the use of cross-validation While the
first two points can be independent of the data used for classification,
the third defines the entire classification and validation procedure
simultaneously. Different strategies can be adopted for the **split of
the whole data set**: equal division (50/50), the greater part intended
for training and the smaller part for validation (e.g. 70/30), or the
greater part intended for validation (e.g. 30/70). In **K-fold
cross-validation** technique the K parameter refers to the different
number of dataset subsets divided randomly and this number is used for
the model training while the rest of the subset is used for validation.
In each training and evaluation step the prediction error is calculated
and after repeating it K-times the overall measure is provided.

-   accuracy assessment

**(bridge with Module 1, 4 - content to be agreed)**

References: Cao, X., Wei, C., Han, J., & Jiao, L. (2017). Hyperspectral
band selection using improved classification map. IEEE geoscience and
remote sensing letters, 14(11), 2147-2151.
<https://doi.org/10.1109/lgrs.2017.2755541>

Georganos, S., Grippa, T., Vanhuysse, S., Lennert, M., Shimoni, M.,
Kalogirou, S., & Wolff, E. (2018). Less is more: Optimizing
classification performance through feature selection in a
very-high-resolution remote sensing object-based urban application.
GIScience & remote sensing, 55(2), 221-242.
<https://doi.org/10.1080/15481603.2017.1408892>

Henrich, V., Götze, E., Jung, A., Sandow, C., Thürkow, D., & Gläßer, C.
(2009, March). Development of an online indices database: Motivation,
concept and implementation. In Proceedings of the 6th EARSeL imaging
spectroscopy sig workshop innovative tool for scientific and commercial
environment applications, Tel Aviv, Israel (pp. 16-18).
[SOURCE](https://www.researchgate.net/publication/259802556_Development_of_an_online_indices_database_Motivation_concept_and_implementation)

Immitzer, M., Neuwirth, M., Böck, S., Brenner, H., Vuolo, F., &
Atzberger, C. (2019). Optimal input features for tree species
classification in Central Europe based on multi-temporal Sentinel-2
data. Remote Sensing, 11(22), 2599. <https://doi.org/10.3390/rs11222599>

Li, J., Tang, J., & Liu, H. (2017, August). Reconstruction-based
Unsupervised Feature Selection: An Embedded Approach. In IJCAI
(pp. 2159-2165). <https://doi.org/10.24963/ijcai.2017/300>

Swain, P. H., & Davis, S. M. (1981). Remote sensing: The quantitative
approach. IEEE Transactions on Pattern Analysis & Machine Intelligence,
3(06), 713-714. <https://doi.org/10.1109/tpami.1981.4767177>

Wakulińska, M., & Marcinkowska-Ochtyra, A. (2020). Multi-temporal
sentinel-2 data in classification of mountain vegetation. Remote
Sensing, 12(17), 2696. <https://doi.org/10.3390/rs12172696>

## Exercise

Multitemporal vegetation classification using Random Forest algorithm
and Sentinel-2 data with \[R\], (../../software/software_r\_language.md)
and [QGIS](../../software/software_qgis.md) for visualisation.

### Next unit

Proceed with [Vegetation monitoring and disturbance
detection](../05_vegetation_monitoring/05_vegetation_monitoring.md)
