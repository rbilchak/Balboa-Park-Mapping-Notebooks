# We can put links to notebooks here and post any code or questions 

Later we can take the good info and add it to the ReadMe for the project: 

## Viewshed Analysis 

Relevance: 
This method of analysis identifies all possible viewpoints from a specific location within a project area. The viewshed analysis will allow us to compile multiple layers (vegetation, commercial buildings, residential, etc.) to better current viewpoits/vistas and reduce any negative impacts of future construction. Below is the link to the ArcGIS Interactive Viewshed demonstration map and various tools with how to apply to the Balboa Park Project. The Interactive Viewshed model components include a color scheme (visibility patterns), parameters (angles, range, tilt), and an observer (observer placement). 

[ArcGIS Interactive Viewshed Directions/Application](https://doc.arcgis.com/en/arcgis-earth/use/interactive-analysis.htm#:~:text=Viewshed%20analysis%20indicates%20the%20visibility%20%28visible%20or%20obstructed%29,in%20the%20scene%20to%20specify%20the%20observer%20position.)

[Python Elevation](https://github.com/Esri/elevation-gp-python)

[The JavaScript library used to create a map and perform viewshed analysis](https://github.com/mmurillo4410/viewshed)

1. Download [QGIS](https://www.qgis.org/en/site/) Open Source Geographic Information System 
    QGIS: Used for multiple purposes including: 
        - line of sight 
        - develop estimates of viewpoints 
2. Install Visibility Analysis to QGIS
3. Go to [USGS](https://www.usgs.gov/programs/national-geospatial-program/national-map) to search region of interest and obtain the dataset
4. On USGS National Map Website, search Balboa Park. This will locate the data sets that cover the Digital Elevation Model (DEM) and produce an image to overlay into QGIS. 
5. Figure out your radius and number of viewpoints 
6. Figure out local viewsheds that are visible from the park, by using the default, basic model. This basic model views buildings and does not include vegetation. To include vegetation, the LIDAR program is needed, which is a limitation we have due to time and access. 
7. Save your project on your desktop
8. Add layers (the USGS map or dataset) 
9. Create layers for viewpoints.
10. Create viewshed Analysis with a scale (white to dark). White being higher elevation and Dark being lower elevation
11. Create polygon of the project boundary.
12. Find Cumulative vieeshed. This takes into consideration of all viewpoints selected and how many of those points can be seen from a viewpoint selected. 

## 2. Economic Analysis 

Relevance: This method will take the 1989 Master Plan and overlay it with the most up-to-date map we have in order to assess the economic standing of the neighborhood and how the creation of the park has effected the surrounding community. 

## 3. Isochrone Analysis

Relevance: This method will examine the park's accessibility through public transportation. In order to increase the utilization of the park by local communities it needs to be accessible. If the new plan intends on removing parking spaces, park utilization will decline of accessibilty is low. 

1. Install the necessary libraries: To use isochrone data, you will need to install the following libraries:

osmnx: to download OpenStreetMap data for San Diego

networkx: to analyze the network

pandas: to manipulate data

geopandas: to work with spatial data

pyproj: to convert between coordinate systems

folium: to create interactive maps

You can install these libraries using !pip install.


2. Download OpenStreetMap data for San Diego: You can use the osmnx library to download the OpenStreetMap data for San Diego. The following code will download the data for San Diego and extract the street network

3. Generate isochrone data: You can use the osmnx library to generate isochrone data. The following code will generate isochrones for Balboa Park for travel times of 5, 10, 15, 20, and 25 minutes using public transportation

4. Prepare the data for mapping: You can use geopandas to merge the isochrone data with the street network data and prepare the data for mapping. The following code will merge the isochrone data with the street network data and convert the data to the appropriate coordinate system

5. Create an interactive map: You can use folium to create an interactive map of the isochrone data. The following code will create an interactive map of the isochrone data for Balboa Park:

## 4. Slope Analysis 

Relevance: Specifically requested by SAGE, this method will help determine the future development of the park. In coordination with the viewshed analysis, slope analysis will allow developers to discover what areas are accessible through walking, biking, or cars. Thus slope analysis can give insight on what time of development can occur throughout the park. 

1. Acquire the elevation data for Balboa Park: The first step is to acquire the elevation data for Balboa Park. You can obtain this data from various sources such as USGS National Map or OpenTopography. You can also use Python libraries such as rasterio or GDAL to download the data programmatically.

2. Preprocessing the data: Once you have acquired the data, you will need to preprocess it before performing the slope analysis. This includes converting the data to a suitable format (e.g., GeoTIFF) and projecting it to a standard coordinate reference system (CRS) such as WGS 84.

3. Calculating slope: Next, you will need to calculate the slope of the terrain. You can do this by using the gdaldem command line tool or by using Python libraries such as rasterio or GDAL. The slope is typically calculated in degrees or percent rise.

4. Comparing previous and new slope: Once you have calculated the slope for Balboa Park, you can compare the previous and new slope by calculating the difference between the two. You can do this by subtracting the previous slope from the new slope and plotting the difference on a map.

# code: 

import rasterio
import numpy as np
import matplotlib.pyplot as plt

# Load the elevation data
with rasterio.open('balboa_park.tif') as src:
    elev_data = src.read(1)

# Calculate slope using rasterio
res = src.res[0]
slope = np.arctan(np.sqrt(np.square(src.dtypes[0](np.gradient(elev_data, res)[0])) + np.square(src.dtypes[0](np.gradient(elev_data, res)[1]))))
slope = np.degrees(slope)

# Calculate previous slope (assuming you have the data)
prev_slope = ...

# Calculate difference between slopes
slope_diff = slope - prev_slope

# Plot difference map
plt.imshow(slope_diff, cmap='coolwarm')
plt.colorbar()
plt.title('Difference in Slope')
plt.show()
