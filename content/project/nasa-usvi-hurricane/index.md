+++
# Project title.
title = "USVI Hurricane Water Quality"

# Date this page was created.
date = 2018-11-20T00:00:00

# Project summary to display on homepage.
summary = "Changes in Water Quality in the USVI after the 2017 Hurricane Season"

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

The US Virgin Islands, located just East of Puerto Rico in the Caribbean, consists of three main islands, St. Croix, St. John, and St. Thomas. In 2017, two major hurricanes, Irma and Maria, struck the islands, causing widespread damage. As part of the NASA DEVELOP project, we collaborated with the USVI Coastal Zone Management (CZM) to analyze the image of the hurricanes on water quality around reefs. Tourism is a huge sector in the USVI economy, and reefs are a vital part of that, so knowing the impact of major hurricanes such as Irma and Maria is vital.

{{< figure library="1" src="projects/nasa-usvi-hurricane/USVI_TechImage.png" >}}

Using NASA's Earth Observing Platforms along with ESA's Sentinel-2, we looked at data from Landsat 5, Landsat 8, and Sentinel-2. Landsat 5 was used to look at historical hurricane impacts, while Landsat 8 and Sentinel-2 were used to establish baseline water quality during a non-hurricane year (2016) and post-hurricane water quality. ACOLITE, a standalone program for processing satellite data into ocean color products, was used to batch process the data for all 200+ images analyzed in this study.

{{< figure library="1" src="projects/nasa-usvi-hurricane/USVI_Sats.png" >}}

We analyzed 3 water quality variables, Chlorophyll-a, Suspended Particulate Matter (SPM), and Turbidity. For 2016, we calculated the median value for each pixel, as well the upper quartile. Each 2017 image was per pixel compared to pixel median and upper quartile, in order to create images of areas above 2016 normal. These were used to calculate the percentage of days with data that were calculated as above 2016 normal.

## Results

{{< figure library="1" src="projects/nasa-usvi-hurricane/USVI_Chla.png" >}}
{{< figure library="1" src="projects/nasa-usvi-hurricane/USVI_SPM.png" >}}
{{< figure library="1" src="projects/nasa-usvi-hurricane/USVI_Turb.png" >}}
Residence Time shows the percentage of pixels with data that were flagged as above 2016 normal over time. You can see that over time water quality parameters return to normal, over about 3 months.
{{< figure library="1" src="projects/nasa-usvi-hurricane/ResidenceTime.png" >}}
