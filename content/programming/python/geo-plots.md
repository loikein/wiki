---
weight: 701
title: "Geographical Plots"
---
Refs:

- [The easiest way to plot data from Pandas on a world map | by Udi Yosovzon | Towards Data Science](https://archive.ph/gtWxc) \(GeoPandas \+ Matplotlib\)
- [Geographic Data with Basemap | Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/04.13-geographic-data-with-basemap.html) \(Matplotlib \+ Basemap\)
- [Mapping with Matplotlib, Pandas, Geopandas and Basemap in Python | by Ashwani Dhankhar | Towards Data Science](https://archive.is/gooRj) \(The main example uses Matplotlib. The author uses the `shapefile` package which is now `pyshp`? to read the map file, but `GeoPandas` has similar importer functions.\)
- [Geographical Plots with Python - KDnuggets](https://www.kdnuggets.com/2020/09/geographical-plots-python.html) \(plotly \+ Cufflinks\)
- \(\*\) [How I Created Animated Choropleth Map and Running Bar Plot using Python | by Girish Dev Kumar Chaurasiya | Python in Plain English](https://archive.ph/oYGgf) \(GeoPandas \+ Matplotlib\) \(May need this later\)
- [Python Folium: Create Web Maps From Your Data – Real Python](https://realpython.com/python-folium-web-maps-from-data/) \(Folium\)
- [Easy Steps To Plot Geographic Data on a Map — Python | by Ahmed Qassim | Towards Data Science](https://archive.ph/THz8O) \(Matplotlib, and a mini OpenStreetMap tutorial\)
- [Welcome to Introduction to Python GIS -course 2018! — Intro to Python GIS CSC documentation](https://automating-gis-processes.github.io/CSC/index.html)
    - [Automating-GIS-processes/CSC](https://github.com/Automating-GIS-processes/CSC/tree/master)
- [Mapping and Data Visualization with Python (Full Course Material)](https://courses.spatialthoughts.com/python-dataviz.html) \(Covers many packages\)


## Basic plotting flow

1. Have data \(to plot\) with latitude and longitude columns;
2. Get map data \(vector map/shape file/polygons/tiles/webmap\) of the desired range; \(some packages, like Basemap, seem to come with global and US maps, but not of other countries\)
3. Import both datasets;
4. Plot map data first, then layer the actual data on top of it.

### How to get dataset with latitude/longitude

Datasets with lat/lon:

- [Introduction of geodatasets - geodatasets 2023.3.1.dev6+gfb9ce89](https://geodatasets.readthedocs.io/en/latest/introduction.html)

Convert postcode to lat/long:

- Worldwide by-country lookup TSVs: [GeoNames](https://download.geonames.org/export/zip/?C=N;O=D) \(column names: `["country code", "postal code", "place name", "admin name1", "admin code1", "admin name2", "admin code2", "admin name3", "admin code3", "latitude", "longitude", "accuracy"]`, see `readme.txt`\)
    - Python wrapper: [symerio/pgeocode](https://github.com/symerio/pgeocode) \(does not support the "full" version for CA,NL and UK yet\)
- [geopandas.tools.geocode](https://geopandas.org/en/stable/docs/reference/api/geopandas.tools.geocode.html): [geopy/geopy](https://github.com/geopy/geopy) wrapper. Most decent providers \(like Google\) require API keys.

### How to get maps

- [A full look into providers objects - xyzservices 2023.10.1](https://xyzservices.readthedocs.io/en/stable/introduction.html)
