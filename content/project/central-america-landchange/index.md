+++
# Project title.
title = "Mexico Land Change"

# Date this page was created.
date = 2018-11-20T00:00:00

# Project summary to display on homepage.
summary = "Transtion Potential of Land in Mexico in 2030"

# Tags: can be used for filtering projects.
tags = ["Raster"]

share = false

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder.
[image]
  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"
  
  preview_only = true
+++

This project created maps of the lands potential to transtion from Forest, Grassland, and Shrubland to Agriculture or Settlement. We used [ESA CCI Land Cover Data](http://maps.elie.ucl.ac.be/CCI/viewer/), reclassified into 7 catagories, and TerrSett's Land Change Modeler tool. This project used 9 explanatory variables, listed in the workflow below, and change analysis to determine the transition potential of each land cover type using the TerrSett MLP model.
{{< figure library="1" src="projects/central-america-landchange/MX_landcover.jpg" >}}
{{< figure library="1" src="projects/central-america-landchange/MX_Methods.jpg" >}}

Using change analysis, we can see how catagories are lossing area and gaining area. Forests had the highest net loss out of all catagories, while settlement had the highest net gain. Shrubland had both very high loss and very high gain of area. Grassland had very little transition between 2008 and 2015. The gain loss data is additionally run through a markov chain to determine change allocation.
{{< figure library="1" src="projects/central-america-landchange/MX_GainLoss.jpg" >}}


{{< figure library="1" src="projects/central-america-landchange/MX_Skill.jpg" >}}
The Transition Potential Sub-Models, shown above, were built using MLP. We tested each variable for significance in the model, in order to determine which variables to use in MLP modeling for each of the sub-models. The skill and accuracy of each model is shown, as well as the variables that were used to model transitions. Forest to Agriculture was the hardest sub-model to create, mainly due to the fact that it is the largest transition, and therefore the most difficult. While most of the transition from forest to agriculture is in south-east Mexico, it is also widely spread. Grassland to Agriculture was the transition that had the highest skill score, but is the smallest transition. Transition Potentials for each sub-model are shown below. 
{{< figure library="1" src="projects/central-america-landchange/MX_Transitions.jpg" >}}


## Overall Transition Potential and Modeled 2030 Land Cover
{{< figure library="1" src="projects/central-america-landchange/2030_SoftTransition_2.jpg" >}}
The main area with high transition potential is the Yucatan Penisula, which is concerning due to the fact that it is an area with very high biodiversity and holds vast biosphere reserves for this reason. Meanwhile Northern Mexico has very low transition potential. This map can be used to target areas that may be under threat of conversion in order to create conservation areas.
{{< figure library="1" src="projects/central-america-landchange/MX_landcover_2030_2.jpg" >}}