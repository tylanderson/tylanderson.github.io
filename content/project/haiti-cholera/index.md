+++
# Project title.
title = "Haiti Cholera Health Sites"

# Date this page was created.
date = 2018-11-20T00:00:00

# Project summary to display on homepage.
summary = "Accessibility of Health Sites in Artibonite, Haiti"

# Tags: can be used for filtering projects.
tags = ["Vector"]

share = false

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder.
[image]
  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"

  preview_only = true
+++

## Introduction
In 2010, a major earthquake struck Haiti, causing widespread damage. Following the earthquake, a massive cholera outbreak occurred. The first case was in October 2010, and by March 2011 ~4,500 people had already died as a result of cholera. Since 2010, ~9,750 people have died from cholera, and it has infected more than 800,000 people.

The 2010 Haitian Cholera outbreak was the first modern outbreak of cholera. The first cases occurred in Artibonite, Haiti's largest department with an estimated population of 1.7 million people. The outbreak began in the Artibonite river, due to untreated sewage contaminating the river from a UN Peacekeeping Camp, which was set up to provide relief from the 2010 earthquake. As the river is a drinking source for many people, and due to Haiti's poor drinking water and sanitation infrastructure, Cholera spread rapidly. Today Artibonite continues to be the department with the most Cholera cases in Haiti.
{{< figure library="1" src="projects/haiti-cholera/StudyArea.png" >}}

## Data & Methods
Data for this project was retrieved from publicly accessible and open-source sites. Most data came from the Humanitarian Data Exchange (HDX), and Open Street Maps (OSM).

| Data          | Source                                                       | Link                                                                      |
|---------------|--------------------------------------------------------------|---------------------------------------------------------------------------|
| OSM Roads     | Open Street Maps                                             | [URL](https://download.geofabrik.de/central-america/haiti-and-domrep.html)|
| CNIGS Roads   | Centre National de l'Information Géo-Spatiale                | [URL](https://data.humdata.org/dataset/haiti-roads)                       |
| Health Sites  | Global Health Site Mapping Project                           | [URL](https://data.humdata.org/dataset/haiti-healthsites)                 |
| Administrative Boundaries | OCHA Haiti                                        | [URL](https://data.humdata.org/dataset/hti-polbndl-adm1-cnigs-zip)        |
| Population    | WorldPop                                                     | [URL](http://www.worldpop.org.uk/data/summary/?id=172)                    |
| DEM           | STRM                                                         |  [URL](https://www2.jpl.nasa.gov/srtm/)                                   |

**Preprocessing:** The road network, due to being open sourced, had many flaws that need to be fixed. By extending the lines using editor in ArcGIS, and Planarizing the road features, a capable road dataset was built.

  1. Merged OSM and CNIGS road datasets
  2. Extend Lines Tool
  3. Trim Lines Tool
  4. Planarize Lines

**Network Dataset:** After fixes, the road network for analysis was built using simple distance based cost, and service areas were generated for three intervals; 0km - 2km, 2km - 5km, and 5km - 8km. Cholera health sites within 5km was our target, being ~1 hour walking time, with 8km being on the outer fringes of health site accessibility. We chose to use distances as few people in Haiti own their own car, and rural areas have to walk to health sites. Additionally, previous research had looked at health sites within 5km Euclidean distance.

**New Health Site Suitability:** Using suitability variables new health site suitability was calculated for areas outside of current service areas. The weighted overlay tool in ArcGIS was suitable for this. The weights were set as follows:

  * Population: 35%
  * Distance to Roads: 25%
  * Distance from Service Areas: 25%
  * Slope: 15%

## Results
{{< figure library="1" src="projects/haiti-cholera/Network Anlysis.png" >}}

{{< figure library="1" src="projects/haiti-cholera/HealthSiteSuitability.png" >}}

{{< figure library="1" src="projects/haiti-cholera/TownSuitability.png" >}}
