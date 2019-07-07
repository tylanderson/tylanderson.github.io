+++
# Project title.
title = "Hurricane Risk"

# Date this page was created.
date = 2018-11-20T00:00:00

# Project summary to display on homepage.
summary = "Hurricane Risk Index for Populations in Florida"

# Tags: can be used for filtering projects.
tags = ["Vector"]

share = false

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder.
[image]
  # Caption (optional)
  caption = "Hurricane Risk Index (HRI)"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Center"

  preview_only = true

+++

This project, produced out of an Advanced Vector class, examined how to quantify Hurricane Risk by county for Florida (as well as surrounding counties). Using Historical Hurricane data from NOAA, and Social Vulnerability data from the CDC, we mapped Exposure to hurricanes, Average Intensity of Hurricanes, and Vulnerability. These were aggregated into a final, Hurricane Risk Index, or HRI. This can be used to assess the risk of each county to hurricane impacts. This is based off historical data, and may change in the future.

{{< figure library="1" src="projects/hurricane-risk/HRI_Methods.jpg" >}}
Hurricane Risk Index is created using a multi-criteria evaluation with three parameters, a Social Vulnerability Index, a Hurricane Strike Index, and a Hurricane Wind Speed Index. These factors are based off the theory of disaster risk based off exposure, vulnerability, and intensity. All three varaibles were standardized from 0 - 1, and then combined using the HRI algorithm:
$$ HRI=\frac{(W{a}\*SoVI)+(W{b}\*HurrStrike)+(W{c}\*AvgSpeed)}{W{a}+W{b}+W{c}} $$
Weights were set so that the hurricane data was not over represented: $W{a}=0.5$, $W{b}=0.25$, $W{c}=0.25$.
{{< figure library="1" src="projects/hurricane-risk/HRI_Inputs.jpg" >}}
Individual HRI variables, and Hot Spot analysis for each. Hurricane based variables have a large hot spot in South Florida, while SoVI shows a hot spot of vulnerability just north of Florida.

## HRI Results
{{< figure library="1" src="projects/hurricane-risk/HRI_Map.jpg" >}}
The Hurricane Risk Index product compares total risk of a county. This can account for areas that may have high risk in one category, but low risk in another. This index ranges from 0 to 1, with 0 having no risk in each variable, and 1 having the highest risk in each variable. (Our HRI ranged from near 0 to 0.91).
{{< figure library="1" src="projects/hurricane-risk/HRI_HotSpot_146080_Map.jpg" >}}
Running Hot Spot analysis on the HRI reveals that South Florida has the highest hurricane risk index, as well as a large hot spot of high HRI. This is the area most often struck by hurricanes, so it is important to know the risks in these areas. There is a cold spot just south of Jacksonville, which could indicate those communities are less at risk of hurricane damage. While the SoVI data we used came at county level, it would be very interesting to create a new SoVI index and use to at the town level to see more detail in HRI maps.
