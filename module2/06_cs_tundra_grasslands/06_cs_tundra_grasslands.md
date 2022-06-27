## Introduction

In this case study we will focus on classyfing non-forest tundra
vegetation in higher parts of Karkonosze Mountains, laying on the
Polish-Czech border. The process will consist of extracting refrence
data fro multitemporal imagery and classyfing it with Support Vector
Machine algorithm.

### Other case studies

-   [Seasonal dynamics of vegetation in mountain ecosystems
    (Karkonosze)](../07_cs_vegetation_dynamics/07_cs_vegetation_dynamics.md)
-   [Forest disturbance detection
    (Tatras)](../08_cs_disturbance_detection/08_cs_disturbance_detection.md)

### Module themes

-   [Principles of multispectral
    imaging](../01_multispectral_principles/01_multispectral_principles.md)
-   [Temporal information in satellite
    data](../02_temporal_information/02_temporal_information.md)
-   [Image processing
    workflow](../03_image_processing/03_image_processing.md)
-   [Multitemporal classification of vegetation
    types](../04_multitemporal_classification/04_multitemporal_classification.md)
-   [Vegetation monitoring and disturbance
    detection](../05_vegetation_monitoring/05_vegetation_monitoring.md)

## Getting started

### Installing and loading required libraries

To go further in our excercise we need to download, install and load the
packages we will use further in our study. We will proceed with
attaching packages throughout the exercise whenever we need new
functionality unavailable with previously used libraries.

Let’s proceed with our first package: raster

Run the below line of code in your RStudio console to install remotes
package

``` r
install.packages("raster")
```

We will use raster to read our image into R environment.

Note that some of the dependency packages we will use later are also
installed with others, however we may need to load them in separately.
The raster package and all its dependencies should now be properly
installed.

Now let’s load it them into our project.

``` r
library(raster)
```

Use function brick to load multiband raster.

``` r
image <- brick("data/ABCD_stacked_res.bsq")
```

Brick raster consists of 10 band collected in 2018 from 4 images by
Sentinel-2. The spatial extent of the raster covers Polish side of
Karkonoski National Park.

Next we should load our reference polygons and see their structure. To
do that attach sf package and then load shapefile.

``` r
library(sf)
reference <- st_read("data/poligony_MW_masked.shp")
head(reference)
```

Now we can extract pixel values from brick image. In order to do that we
shall write function which will collect information from pixels for each
polygon with extract function from raster package.

``` r
extract_from_polygons <- function(img, vector, class_field, feature_index){
  
  num_polygons <- length(feature_index)
  extracted_data <- data.frame()
  class_field_index <- which(colnames(vector) == class_field)

  atribbutes_table <- st_drop_geometry(vector)
  
  for (i in feature_index) {
    feature <- vector[i,]
    class <- atribbutes_table[i, class_field_index]
    
    pixel_values <- extract(img, feature, df = TRUE)
    pixel_values <- cbind(pixel_values[ ,2: ncol(pixel_values)], class, i)
    extracted_data <- rbind(extracted_data, pixel_values)
    
  }
  return(extracted_data)
}
```

Now we will use the function above to generate reference polygons.

``` r
reference_pixels <- extract_from_polygons(image, reference, "klasa", seq(1, nrow(reference)))

colnames(reference_pixels) <- c(colnames(reference_pixels)[1:41], "index")
```

With the reference pixel collected we can now process with
classification process.

First we establish some basic parameters, like number of iterations,
percentage of training/test data split and number of bands.

``` r
iterations <- 100
training_percentage <- 0.6
bands <- 40
```

We should establish seed for training/test split. In order for the
results to be reproducible we will generate 100 seed in a 1-100
sequence.

``` r
seeds <- seq(1, 100)
```

Then we can procees with iterative classification process. We will use
the same Support Vector Machine parameters for each iteration (raidal
kernel, cost = 100 and gamma = 0.0333). We will also create some empty
data frames for accuracy results.

``` r
results_svm_f1 <- data.frame()
results_svm_ua <- data.frame()
results_svm_pa <- data.frame()
results_svm_kap <- data.frame()
results_svm_oa <- data.frame()

model_box <- list()

for (i in seq(iterations) ) {
  set.seed(seeds[i])
  training_indices <- createDataPartition(reference$klasa, p = training_percentage, list = FALSE)
  training_data <- reference_pixels[ reference_pixels$i %in% training_indices ,]
  test_data <- reference_pixels[ !(reference_pixels$i %in% training_indices) ,]
  
  
  training_data$klasa <- as.factor(training_data$klasa)
  test_data$klasa <- as.factor(test_data$klasa)
  
  model_svm <- svm(training_data[, 1:bands ], training_data$klasa, kernel = "radial", cost = 100, gamma = 0.0333, type = "C")

  model_box[[i]] <- model_svm
  
  pred_test_svm <- predict(model_svm, test_data[ , 1:bands ])
  
  con_mat_test_svm <- confusionMatrix(pred_test_svm, test_data$klasa, mode = "everything")
  

  results_svm_f1 <- rbind(results_svm_f1, con_mat_test_svm$byClass[ ,7])
  names(results_svm_f1) <- levels(training_data$klasa)
  

  results_svm_ua <- rbind(results_svm_ua, con_mat_test_svm$byClass[ ,5])
  names(results_svm_ua) <- levels(training_data$klasa)
  

  results_svm_pa <- rbind(results_svm_pa, con_mat_test_svm$byClass[ ,6])
  names(results_svm_pa) <- levels(training_data$klasa)
  

  results_svm_kap <- rbind(results_svm_kap, con_mat_test_svm[["overall"]][["Kappa"]])
  names(results_svm_kap) <- "kappa"
  

  results_svm_oa <- rbind(results_svm_oa, con_mat_test_svm[["overall"]][["Accuracy"]])
  names(results_svm_oa) <- "overall_accuracy"
}
```

Now we can find the set with highest achieved Overall Accuracy.

``` r
maximum_oa_model_number <- which.max(results_svm_oa[,1])
best_model <- model_box[[maximum_oa_model_number]]
```

And then use the best model to classify our image.

``` r
classification_image <- raster::predict(image, best_model, progress = "text")
```

Results: classification image ![Classification
image](img/classification_results.png)
