---
title: Uploading Custom Raster Image Collections to Google Earth Engine
author: ~
date: '2019-07-16'
slug: uploading-custom-raster-image-collections-to-google-earth-engine
categories: []
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2019-07-16T17:26:02-04:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

If you are like me, the image collections on Google Earth Engine are not always suitable for the project that you are working on. Luckily there are other people out there like you who have also been interested in the idea of uploading raster image collections that are not in the Google Earth Engine catalog to Earth Engine Image Collection assets. This post aims to show how I did this and why you might want to do this. Things move fast so this post might not be up to date when you use it!

## The Problem

Google Earth Engine is a great utility. It allows for processing of large image collections, which can make for some really cool analysis all from the browser. One of the big draws of Earth Engine is the repository of many different satellite products already ingested by Google. However there are some exceptions. For me, I was working on a project and wanted to create cloud free composites, and products derived from them, from Landsat ARD data and Harmonized Landsat Sentinel-2 data, both of which aren't on the current GEE repository. So what do you do? Well currently, you can upload raster images one at a time to assets in GEE, however this would take a while and doesn't add them to a image collection.

## Enter *geeup*

[geeup](https://github.com/samapriya/geeup) is a python package that I stumbled upon when searching for solutions. This allows you to upload rasters to an image collection from a CLI. Additionally, you can upload metadata along with the files, something we will also utilize

### Setup
  * Make sure you have python installed. I recommend using [anaconda](https://www.anaconda.com/distribution/) to manage everything in a virtual environment.
  * Make sure you have installed and setup the [Google Earth Engine python API](https://developers.google.com/earth-engine/python_install_manual)
  * Make sure geeup is installed and callable from the cli

### Using geeup...

Once everything is installed and working, geeup is pretty easy to use. You can call it from the cli

First let's see all the arguments we need for uploading to image collections
```console
geeup upload --help
```
Which returns the following:
```console
usage: geeup upload [-h] --source SOURCE --dest DEST -m METADATA
                    [--nodata NODATA] [-u USER]

optional arguments:
  -h, --help            show this help message and exit

Required named arguments.:
  --source SOURCE       Path to the directory with images for upload.
  --dest DEST           Destination. Full path for upload to Google Earth
                        Engine, e.g. users/pinkiepie/myponycollection
  -m METADATA, --metadata METADATA
                        Path to CSV with metadata.
  -u USER, --user USER  Google account name (gmail address).

Optional named arguments:
  --nodata NODATA       The value to burn into the raster as NoData (missing
                        data)
```
This lets us know that we must give a path to which the images area stored, a destination name, a csv file, and an user account
We want to upload slected metadata that is embeded into the file, as well as some extra metadata like filename and datetime

geeup upload requires that the first column starts with in_no, a column of filenames without their extensions
Additionally, if you want to take advantage of filtering by date, you need to upload a variable called system:time_start which contains a integer of milliseconds since UNIX epoch.

### Extract Metadata to CSV

I have written some code that iterates through a folder of GeoTIFF images and returns a csv file with the format required to upload to earth engine using geeup upload. This may need some tweaks to get it to work with your data.
~~~python
from osgeo import gdal
import pandas as pd
import os

in_dir = r"E:\Moth\HLS_DATA\HLS_GTiff"
out_csv = r"E:\Moth\HLS_DATA\HLS_metadata.csv"

# List of metadata keys to extract
meta_keys = ['cloud_coverage',
             'SENSOR',
             'spatial_coverage']

# Add other required keys and make pandas data frame
# We will store the metadata in the df
csv_keys = ['id_no', 'system:time_start']
csv_keys.extend(meta_keys)
df = pd.DataFrame(columns=csv_keys)

for root, dirs, files in os.walk(in_dir):
    for file in files:
        if file.endswith(".tif"):
            path = os.path.join(root, file) # make path
            raster = gdal.Open(path, gdal.GA_ReadOnly) # Open Raster in GDAL
            meta = dict.fromkeys(csv_keys) # Make a dict to store key, values

            # Get time from filename
            # Example filename (LC80300062013106C2V01_MTLstack.tif)
            year = file[9:13]
            doy = file[13:16]
            hour = '12'
            timestamp = year + doy + hour
            # convert time stamp to gee format
            gee_timestamp = int(pd.to_datetime(timestamp,
                                               format='%Y%j%H').value // 10**6)

            meta['id_no'] = os.path.splitext(file)[0]
            meta['system:time_start'] = gee_timestamp
            for key in meta_keys:
                meta[key] = raster.GetMetadataItem(key)

            df = df.append(meta, ignore_index=True)
print(df)
df.to_csv(out_csv, index=False)

~~~
***Example Output CSV:***

| id_no                          | system:time_start | cloud_coverage | SENSOR   | spatial_coverage |
|--------------------------------|-------------------|----------------|----------|------------------|
| LC8T19TBG2013106HLS14_MTLstack | 1366126135668     | 22             | OLI_TIRS | 87               |
| LC8T19TBG2013122HLS14_MTLstack | 1367508534542     | 0              | OLI_TIRS | 86               |
| LC8T19TBG2013170HLS14_MTLstack | 1371655742618     | 18             | OLI_TIRS | 86               |
| LC8T19TBG2013177HLS14_MTLstack | 1372260914415     | 73             | OLI_TIRS | 71               |
| LC8T19TBG2013186HLS14_MTLstack | 1373038145976     | 14             | OLI_TIRS | 87               |
| LC8T19TBG2013209HLS14_MTLstack | 1375025717043     | 71             | OLI_TIRS | 72               |
| LC8T19TBG2013218HLS14_MTLstack | 1375802947474     | 0              | OLI_TIRS | 87               |
| LC8T19TBG2013250HLS14_MTLstack | 1378567748156     | 7              | OLI_TIRS | 89               |
| LC8T19TBG2013257HLS14_MTLstack | 1379172916462     | 80             | OLI_TIRS | 71               |

### Putting it all together

Finally, we can upload all of this to Google Earth Engine with that same call from before geeup uploading

~~~console
geeup upload --source somepath/somefolder --dest users/username/imagecollection -u user@gmail.com -m somepath/metadata.csv
~~~
