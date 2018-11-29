+++
# Project title.
title = "Massachusetts Forest Cover"

# Date this page was created.
date = 2018-11-20T00:00:00

# Project summary to display on homepage.
summary = "Forest Cover Change in Massachusetts for 2015"

# Tags: can be used for filtering projects.
tags = ["Raster","Remote Sensing"]

share = false

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder.
[image]
  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"
  
  preview_only = true
+++

For my senior honors thesis, I worked to update a Landsat forest cover map for Massachusetts to 2015. At Clark University forest cover maps for the state have been produced back to the 1970's in ~10 year intervals based on data availability. Landsat 8 data for summer months of 2015 were used, with 15 images (3 per landsat scene) in total. CLASlite was used, a software produced by the Carnegie Institution for Science, which classifies raw imagery into fractional cover (soil, photosyntheic vegatation, and non-photosynthetic vegatation) and forest cover maps. CLASlite is a semi-automated approach, user input is only data and thresholds for classification and masking, and most importantly, it's FREE! 
{{< figure library="1" src="projects/ma-landcover/MA_CLASLITE.jpg" >}}
{{< figure library="1" src="projects/ma-landcover/CLASLITE_Methods.png" >}}
CLASlite has a change detection step included, however we chose to use our own method of doing change detection, as we wanted to use multiple dates of Landsat 8 imagery to classify forest for greater confidence. Each Landsat scene had 3 images, which each were classified into forest cover maps from fractional cover using CLASlite. Confidence of forest was calculated using the equation, $Confidence=\frac{N\_{f}-N\_{n\_f}}{N\_{f}+N\_{n\_f}}$, where $N\_{f}$ is the number of times a pixel was classified as forest and $N\_{n\_f}$ is the number of times a pixel was classified as non-forest. This confidence map was then reclassified to forest cover where values 0 to 0.6 are non-forest, and 0.6 to 1 are forest. 

## Results
### Forest Cover
{{< figure library="1" src="projects/ma-landcover/ForestCover2009_Towns.png" >}}
{{< figure library="1" src="projects/ma-landcover/ForestCover2015_Towns.png" >}}
{{< figure library="1" src="projects/ma-landcover/MA_Validation.png" >}}
Training Points were generated at 968 locations, stratified by EcoRegion. A basemap from MassGIS with WorldView imagery also from 2015 was used to validate that forest cover was accurately classified. Rate of accuracy varied by EcoRegion, with overall accuracy at 87%.
{{< figure library="1" src="projects/ma-landcover/ForestLoss_and_Persistance.png" >}}
Forest and Non-Forest cover persistance, gain, and loss shown. This shows where forest cover has grown and where it has lost area.

### Statistics
{{< figure library="1" src="projects/ma-landcover/ForestCoverRateOfLoss.png" >}}
{{< figure library="1" src="projects/ma-landcover/ForestCoverRateOfLoss_StdDev.png" >}}

