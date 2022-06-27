## Introduction

In this case study we will focus on forest disturbance detection in
Tatras, which is the highest mountain range in the Carpathian Mountains.
We will go through the whole process from searching and downloading the
data to producing disturbance maps.

### Other case studies

-   [Monitoring tundra grasslands
    (Karkonosze)](../06_cs_tundra_grasslands/06_cs_tundra_grasslands.md)
-   [Seasonal dynamics of vegetation in mountain ecosystems
    (Karkonosze)](../07_cs_vegetation_dynamics/07_cs_vegetation_dynamics.md)

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

Let’s proceed with our first package: remotes

``` r
#   Run the below line of code in your RStudio console to install remotes package
#   install.packages("remotes")
```

Remotes package is required to install getSpatialData package from
GitHub.

``` r
#   Run the below line of code in your RStudio console to install getSpatialData package
#   remotes::install_github("16EAGLE/getSpatialData")
```

Note that some of the dependency packages we will use later, like sf,
are also installed with getSpatialData, however we may need to load them
in separately. The getSpatialData package and all its dependencies
should now be properly installed.

Now let’s load it them into our project, along with the sf package.

``` r
library(getSpatialData)
library(sf)
```

In our first step we want to establish our Area of Interest. Now let’s
load a vector file with general area of Tatras using sf package.

``` r
tatras <- st_read("data/tatras.gpkg")
```

To preview the Area of Interest run the below chunk of code wit
uncommented line.

``` r
set_aoi(st_geometry(tatras))
# view_aoi()
```

Now let’s set archive directory. This directory will store all the data
we will download in the further steps.

``` r
set_archive(paste0(getwd(), "/data"))
```

To access the satellite data we need to access appropriate data portal.
In this case study we will use Landsat data archive from United States
Geological Survey’s [EarthExplorer](https://earthexplorer.usgs.gov/). If
you don’t have an account yet, proceed to the [registration
page](https://ers.cr.usgs.gov/register). If you have an account, the
following line will prompt you to input your username and password in
order to access the data on EarthExplorer.

``` r
login_USGS()
```

After the successful login you may now query the database. For our
purpose we would like to access Landsat 8 Collection 2 Level 2 data
acquired in the summer months (June-September) in 2015-2020 years.

``` r
landsat_scenes <- getLandsat_records(
  time_range = c("2015-06-01", "2020-09-30"),
  products = "landsat_ot_c2_l2"
)
```

We now have a data frame of over 3000 records. To find our records of
interest we should filter out the records with specific conditions. To
to that we will need functions provided with lubridate and dplyr
packages.

Load lubridate and dplyr.

``` r
library(lubridate)
library(dplyr)
```

Filter records with set parameters: - add a column indicating month of
acquisition; - add a summary column (used later) - filter the records to
only include L1_T1 products of path/row 188/26 from months
June-Septemper.

``` r
landsat_scenes_filtered <- landsat_scenes %>%
  mutate(month = month(date_acquisition),
         summary = paste0("ID: ", record_id, " Acquisition Date: ", date_acquisition,
                          " Path: ", tile_number_horizontal , " Row: ", tile_number_vertical)) %>%
  filter(level == "l1" & collection_category == "T1" & tile_number_horizontal == 188 & tile_number_vertical == 26 & (month == 6 | month == 7 | month == 8 | month == 9))
```

Download filtered records.

``` r
getLandsat_data(landsat_scenes_filtered)
```

Put the files to separate year directories. It should look like this.

``` r
list.files("data/landsat", pattern = "*.tar", recursive = TRUE)
```

Now prepare mask extent. To do produce a vector extent of AOI, extended
by 300 meters and pull the extent from it, using extent function from
raster package.

``` r
tatras_transform <- st_transform(tatras, 32634)
tatras_transform_buffer <- st_buffer(tatras_transform, 300)

library(raster)
ex <- extent(tatras_transform_buffer)
```

Prepare functions for time series analysis. Function to find image with
highest NDVI value for each pixel.

``` r
ls_max_ndvi <- function(tar_list, ex) {
  
  list_ndvi <- list()
  i <- 1
  
  for (ls_img_tar in tar_list) {
    
    randomstring <- paste(sample(c(0:9, letters, LETTERS), 6, replace = TRUE), collapse = "")
    tempdir <- file.path(dirname(ls_img_tar), randomstring) 
    dir.create(tempdir, recursive = TRUE, showWarnings = FALSE)
    untar(ls_img_tar, exdir = tempdir, tar = "internal")
    files <- list.files(tempdir, full.names = TRUE)
    date <- as.numeric(substr(basename(ls_img_tar), 18, 25))
    
    sr_bands <- sort(grep("SR_B", files, value = TRUE))
    qa_path <- sort(grep("QA_PIXEL.TIF", files, value = TRUE))
    
    qa_mask <- raster(qa_path)

    
    crop_qa <- crop(qa_mask, ex, snap = "in")
    crop_qa[crop_qa == 21824] <- 1
    crop_qa[crop_qa > 1] <- 0
    
    cloud_mask_all_na <- crop_qa
    cloud_mask_all_na[cloud_mask_all_na == 0] <- NA
    
    band_4_crop <- raster(sr_bands[4]) * cloud_mask_all_na 
    band_4_crop <- band_4_crop * 0.0000275 + -0.2
    
    band_5_crop <- raster(sr_bands[5]) * cloud_mask_all_na 
    band_5_crop <- band_5_crop * 0.0000275 + -0.2
    
    ndvi <- (band_5_crop - band_4_crop) / (band_5_crop + band_4_crop)
    list_ndvi[[i]] <- ndvi 
    
    unlink(tempdir, recursive = TRUE, force = TRUE)
    i <- i + 1 
  }
    
  
  brick_ndvi <- brick(list_ndvi)
  max_ndvi <- raster::which.max(brick_ndvi)
  
  return(max_ndvi)
  
}
```

Function to prepare bands based on the highest NDVI indication.

``` r
ls_prepare_bands <- function(tar_list, max_ndvi, ex) {
  
  i <- 1
  
  list_b <- list()
  list_g <- list()
  list_r <- list()
  list_nir <- list()
  list_swir1 <- list()
  list_swir2 <- list()
  list_date <- list()
  
  for (ls_img_tar in tar_list) {
    
    mask_ndvi <- max_ndvi
    
    mask_ndvi[mask_ndvi == i] <- -1
    mask_ndvi[mask_ndvi > 0] <- 0
    mask_ndvi[mask_ndvi == -1] <- 1
    
    randomstring <- paste(sample(c(0:9, letters, LETTERS), 6, replace = TRUE), collapse = "")
    tempdir <- file.path(dirname(ls_img_tar), randomstring) 
    dir.create(tempdir, recursive = TRUE, showWarnings = FALSE)
    untar(ls_img_tar, exdir = tempdir, tar = "internal")
    files <- list.files(tempdir, full.names = TRUE)
    date <- as.numeric(substr(basename(ls_img_tar), 23, 25))
    
    sr_bands <- sort(grep("SR_B", files, value = TRUE))
    qa_path <- sort(grep("QA_PIXEL.TIF", files, value = TRUE))
    
    qa_mask <- raster(qa_path)
    img_date <- qa_mask
    values(img_date) <- 1
    img_date <- crop(img_date, ex, snap = "in")
    
    crop_qa <- crop(qa_mask, ex, snap = "in")
    crop_qa[crop_qa == 21824] <- 1
    crop_qa[crop_qa > 1] <- 0
    
    cloud_mask_all_na <- crop_qa
    cloud_mask_all_na[cloud_mask_all_na == 0] <- NA
    
    band_2_crop <- raster(sr_bands[2]) * cloud_mask_all_na 
    band_2_crop <- band_2_crop * 0.0000275 + -0.2
    
    band_3_crop <- raster(sr_bands[3]) * cloud_mask_all_na 
    band_3_crop <- band_3_crop * 0.0000275 + -0.2
    
    band_4_crop <- raster(sr_bands[4]) * cloud_mask_all_na 
    band_4_crop <- band_4_crop * 0.0000275 + -0.2
    
    band_5_crop <- raster(sr_bands[5]) * cloud_mask_all_na 
    band_5_crop <- band_5_crop * 0.0000275 + -0.2
    
    band_6_crop <- raster(sr_bands[6]) * cloud_mask_all_na 
    band_6_crop <- band_6_crop * 0.0000275 + -0.2
    
    band_7_crop <- raster(sr_bands[7]) * cloud_mask_all_na 
    band_7_crop <- band_7_crop * 0.0000275 + -0.2
    
    
    raster_date <- img_date
    raster_date[raster_date == 1] <- date
    raster_date <- raster_date * cloud_mask_all_na
    
    b_max <- band_2_crop *  mask_ndvi
    g_max <- band_3_crop *  mask_ndvi
    r_max <- band_4_crop *  mask_ndvi
    nir_max <- band_5_crop *  mask_ndvi
    swir1_max <- band_6_crop *  mask_ndvi
    swir2_max <- band_7_crop *  mask_ndvi
    raster_date_max <- raster_date * mask_ndvi
    
    list_b[[i]] <- b_max
    list_g[[i]] <- g_max
    list_r[[i]] <- r_max
    list_nir[[i]] <- nir_max
    list_swir1[[i]] <- swir1_max
    list_swir2[[i]] <- swir2_max
    list_date[[i]] <- raster_date_max
    
    i <- i + 1
    unlink(tempdir, recursive = TRUE, force = TRUE)

  }
  
  list_b$fun <- max
  list_g$fun <- max
  list_r$fun <- max
  list_nir$fun <- max
  list_swir1$fun <- max
  list_swir2$fun <- max
  list_date$fun <- max
  
  mos_b <- do.call(mosaic, list_b)
  mos_g <- do.call(mosaic, list_g)
  mos_r <- do.call(mosaic, list_r)
  mos_nir <- do.call(mosaic, list_nir)
  mos_swir1 <- do.call(mosaic, list_swir1)
  mos_swir2 <- do.call(mosaic, list_swir2)
  mos_date <- do.call(mosaic, list_date)
  
  composition <- brick(mos_b, mos_g, mos_r, mos_nir, mos_swir1, mos_swir2, mos_date)
  names(composition) <- c("B", "G", "R", "NIR", "SWIR1", "SWIR2", "DATE")
  
  return(composition)
}
```

Function to calculate spectral indices.

``` r
ls_calculate_indices <- function(bands) {
  
  names(bands) <- c("b", "g", "r", "nir", "swir1", "swir2", "date")
  
  bcoef <- c(0.3029, 0.2786, 0.4733, 0.5599, 0.508, 0.1872)
  gcoef <- c(-0.2941, -0.243, -0.5424, 0.7276, 0.0713, -0.1608)
  wcoef <- c(0.1511, 0.1973, 0.3283, 0.3407, -0.7117, -0.4559)
  t4coef <- c(-0.8239, 0.0849, 0.4396, -0.058, 0.2013, -0.2773)
  t5coef <- c(-0.3294, 0.0557, 0.1056, 0.1855, -0.4349, 0.8085)
  t6coef <- c(0.1079, -0.9023, 0.4119, 0.0575, -0.0259, 0.0252)
  
  b <- bands$b
  g <- bands$g
  r <- bands$r
  nir <- bands$nir
  swir1 <- bands$swir1
  swir2 <- bands$swir2
  date <- bands$date
  
  ndvi <- (nir - r) / (nir + r)
  ndmi <- (nir - swir1) / (nir + swir1)
  msi <- swir1 / nir
  nmdi <- (nir - (swir1 - swir2)) / (nir + (swir1 - swir2))
  sr <- nir / r
  evi <- 2.5 * ((nir - r) / (1 + nir + 6 * r - 7.5 * b + 1))
  gndvi <- (nir - g) / (nir + g)
  psri <- (r - b) / nir
  npci <- (r - b) / (r + b)
  savi <- (1.5 *(nir - r)) / (nir + r + 0.5)
  osavi <- (nir - r) / (nir + r + 0.16)
  msavi <- (2 * nir + 1 - sqrt((2 * nir + 1)^2 - 8 * (nir - r))) / 2
  nbr <- (nir - swir2) / (nir + swir2)
  nbr2 <- (swir1 - swir2) / (swir1 + swir2)
  wdrvi <- (0.2 * nir - r) / (0.2 * nir + r)
  
  bright <- (b*bcoef[1])+(g*bcoef[2])+(r*bcoef[3])+(nir*bcoef[4])+(swir1*bcoef[5])+(swir2*bcoef[6])
  green <- (b*gcoef[1])+(g*gcoef[2])+(r*gcoef[3])+(nir*gcoef[4])+(swir1*gcoef[5])+(swir2*gcoef[6])
  wet <- (b*wcoef[1])+(g*wcoef[2])+(r*wcoef[3])+(nir*wcoef[4])+(swir1*wcoef[5])+(swir2*wcoef[6]) 
  t4 <- (b*t4coef[1])+(g*t4coef[2])+(r*t4coef[3])+(nir*t4coef[4])+(swir1*t4coef[5])+(swir2*t4coef[6]) 
  t5 <- (b*t5coef[1])+(g*t5coef[2])+(r*t5coef[3])+(nir*t5coef[4])+(swir1*t5coef[5])+(swir2*t5coef[6])
  t6 <- (b*t6coef[1])+(g*t6coef[2])+(r*t6coef[3])+(nir*t6coef[4])+(swir1*t6coef[5])+(swir2*t6coef[6]) 
  
  br <- brick(ndvi, ndmi, msi, nmdi, sr, evi, gndvi, psri, npci, savi, osavi, msavi, nbr, nbr2, wdrvi, bright, green, wet, t4, t5, t6, date)
  
  names(br) <- c("NDVI", "NDMI", "MSI", "NMDI", "SR", "EVI", "GNDVI", "PSRI", "NPCI", "SAVI", "OSAVI", "MSAVI", "NBR", "NBR2", "WDRVI", "TCB", "TCG", "TCW", "TCT4", "TCT5", "TCT6", "Data")
  
  return(br)
  
}
```

Use all 3 functions for each year to produce Max NDVI spectral indices
time series.

``` r
years <- list.files("data/landsat", full.names=T)

for (year in years) {
  
  imgs <- list.files(year, full.names = T, pattern = ".tar*")
  dir_name <- dirname(imgs)[1]
  y <- substr(year, start = nchar(year) - 3, stop = nchar(year))
  print(paste0("Year: ", y, ". No. of images: ", length(imgs)))
  
  max_ndvi <- ls_max_ndvi(imgs, img_mask)

  bands <- ls_prepare_bands(imgs, max_ndvi, img_mask)
  output <- paste0(dir_name, "/", y, "_bands.tif")
  writeRaster(bands, output)
  
  ind <- ls_calculate_indices(bands)
  output <- paste0(year, "/", y, "_indices.tif")
  writeRaster(ind, output)
}
```

Result (NDVI for 2015) ![Result (NDVI for 2015)](img/ndvi_int.png)

``` r
# ind_2015 <- brick("data/landsat/2015/2015_indices.tif")
# names(ind_2015) <- c("NDVI", "NDMI", "MSI", "NMDI", "SR", "EVI", "GNDVI", "PSRI", "NPCI", "SAVI", "OSAVI", "MSAVI", "NBR", "NBR2", "WDRVI", "TCB", "TCG", "TCW", "TCT4", "TCT5", "TCT6", "Date")
# 
# ndvi_2015 <- ind_2015$NDVI
# 
# library(leaflet)
# library(RColorBrewer)
# pal <- colorNumeric(c("red", "orange", "yellow", "green", "darkgreen"), values(ndvi_2015),
#  na.color = "transparent")
# leaflet() %>% addTiles() %>%
#  addRasterImage(ndvi_2015, colors = pal, opacity = 0.8) %>%
#  addLegend(pal = pal, values = values(ndvi_2015),
#    title = "NDVI from Landsat 8 - 2015")
```

Now prepare time series indices from stacks of yearly indices. Example
for NDVI.

``` r
ndvi <- list()

i <- 1
for (year in years) {

  y <- substr(year, start = nchar(year) - 3, stop = nchar(year))
  ind_path <- paste0("data/landsat/", year, "/", y, "_indices.tif")
  ind <- brick(ind_path)
  ndvi[[i]] <- ind[[1]]
  i <- i + 1

}

bndvi <- brick(ndvi)

writeRaster(bndvi, "ndvi_series.tif")
```

Results: 2015 NDVI ![2015 NDVI](img/2015_ndvi.png)
<!-- 2016 NDVI ![2016 -->
<!-- NDVI](img/2016_ndvi.png) 2017 NDVI ![2017 NDVI](img/2017_ndvi.png) 2018 -->
<!-- NDVI ![2018 NDVI](img/2018_ndvi.png) 2019 NDVI ![2019 -->
<!-- NDVI](img/2019_ndvi.png) 2020 NDVI ![2020 NDVI](img/2020_ndvi.png) -->
