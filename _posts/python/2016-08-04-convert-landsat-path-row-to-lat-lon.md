---
layout: single
title: 'Convert Landsat 8 path/row to lat/lon coordinates in Python'
date: 2016-08-04
authors: [Zach Schira]
category: [tutorials]
excerpt: 'This tutorial demonstrates how to convert Landsat 8 path/row coordinates to latitude and longitude in Python.'
sidebar:
  nav:
author_profile: false
comments: true
lang: [python]
lib: [ogr, shapely, urllib, zipfile]
---

The Landsat 8 satellite uses the [WRS-2](http://landsat.gsfc.nasa.gov/the-worldwide-reference-system/) reference system to catalog data. This referece system uses paths and rows, which are derived from the satellites orbit. You may find it useful to be able to convert between the WRS-2 paths and rows to latitude and longitude coordinates. This tutorial will demonstrate how to programmatically perform the conversion in python.

## Objectives

- Import WRS-2 shapefiles
- Define point with given latitude and longitude coordinates
- Find corresponding path/row

## Dependencies

- ogr
- shapely.wkt
- shapely.geometry
- urllib
- zipfile


```python
import ogr
import shapely.wkt
import shapely.geometry
import urllib
import zipfile
```

First we need to download and unzip the WRS-2 shapefiles which can be found on the USGS Landsat website.


```python
url = "https://landsat.usgs.gov/sites/default/files/documents/wrs2_asc_desc.zip"
filehandle, _ = urllib.urlretrieve(url)
zip_file_object = zipfile.ZipFile(filehandle, 'r')
zip_file_object.extractall(".")
zip_file_object.close()
```

Then we can read the shapefile that we just downloaded.


```python
shapefile = 'wrs2_asc_desc/wrs2_asc_desc.shp'
wrs = ogr.Open(shapefile)
layer = wrs.GetLayer(0)
```

Define latitude and longitude coordinates for your desired location. For this example we will use the coordinates of Boulder, Colorado. With these coordinates, we can create a point using shapely. You also must define the mode as ascending or descending ('A', 'D'). Ascending corresponds to nightime images, and descending to daytime images.


```python
lon = -105.2705
lat = 40.0150
point = shapely.geometry.Point(lon, lat)
mode = 'D'
```

Now we will define a helper function called `checkPoint`. This function will take the geometry from a feature, which corresponds to a specific path and row, and check to see if the point we are looking for is contained in the feature, and if it is the correct mode. We will then loop through each feature, until we find one with our point. After this is done, we will print the path and row corresponding to the desired point.


```python
def checkPoint(feature, point, mode):
    geom = feature.GetGeometryRef() #Get geometry from feature
    shape = shapely.wkt.loads(geom.ExportToWkt()) #Import geometry into shapely to easily work with our point
    if point.within(shape) and feature['MODE']==mode:
        return True
    else:
        return False

i=0
while not checkPoint(layer.GetFeature(i), point, mode):
    i += 1
feature = layer.GetFeature(i)
path = feature['PATH']
row = feature['ROW']
print('Path: ', path, 'Row: ', row)
```

    ('Path: ', 34, 'Row: ', 32)

