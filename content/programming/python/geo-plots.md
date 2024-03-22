---
weight: 701
title: "Geographical Plots"
---
## \(Maybe\) Useful resources

Courses:

- [Welcome to Introduction to Python GIS -course 2018! — Intro to Python GIS CSC documentation](https://automating-gis-processes.github.io/CSC/index.html)
    - Repo: [Automating-GIS-processes/CSC](https://github.com/Automating-GIS-processes/CSC/tree/master)
- [Mapping and Data Visualization with Python (Full Course Material)](https://courses.spatialthoughts.com/python-dataviz.html) \(Covers many packages\)
- [Welcome to Pangeo at AOES — Pangeo-at-AOES 0.1.1 documentation](https://kpegion.github.io/Pangeo-at-AOES/index.html)
- [Pythia Foundations — Pythia Foundations](https://foundations.projectpythia.org/landing-page.html)
- [Home — Geographic Data Science with Python](https://geographicdata.science/book/intro.html)
    - Repo: [gdsbook/book](https://github.com/gdsbook/book/tree/master)

{{< details "Things to check out later:" >}}
- [Geographic Data with Basemap | Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/04.13-geographic-data-with-basemap.html) \(Matplotlib \+ Basemap\)
- [Mapping with Matplotlib, Pandas, Geopandas and Basemap in Python | by Ashwani Dhankhar | Towards Data Science](https://archive.is/gooRj) \(The main example uses Matplotlib. The author uses the `shapefile` package which is now `pyshp`? to read the map file, but `GeoPandas` has similar importer functions.\)
- [Using python and geoPandas to map public green spaces in Manchester | by Camila Varó | Medium](https://archive.is/JMyS8) \(GeoPandas \+ Matplotlib \+ contextily\)
- [How I Created Animated Choropleth Map and Running Bar Plot using Python | by Girish Dev Kumar Chaurasiya | Python in Plain English](https://archive.is/oYGgf) \(GeoPandas \+ Matplotlib, Pillow for output as GIF, plotly\)
- [Easy Steps To Plot Geographic Data on a Map — Python | by Ahmed Qassim | Towards Data Science](https://archive.is/THz8O) \(Matplotlib, and a mini OpenStreetMap tutorial\)
- [PacktPublishing/Applied-Geospatial-Data-Science-with-Python: Applied Geospatial Data Science with Python, published by Packt](https://github.com/PacktPublishing/Applied-Geospatial-Data-Science-with-Python)
- [PacktPublishing/Learning-Geospatial-Analysis-with-Python-Fourth-Edition: Learning Geospatial Analysis with Python - Fourth Edition, published by Packt](https://github.com/PacktPublishing/Learning-Geospatial-Analysis-with-Python-Fourth-Edition)
{{< /details >}}

{{< details "Things to not check out later:" >}}
- [Python Folium: Create Web Maps From Your Data – Real Python](https://realpython.com/python-folium-web-maps-from-data/) \(Folium\)
- [Geographical Plots with Python - KDnuggets](https://www.kdnuggets.com/2020/09/geographical-plots-python.html) \(plotly \+ Cufflinks\)
- [Geography with Cartopy](https://tutorial.xarray.dev/fundamentals/04.3_geographic_plotting.html) \(Xarray \+ Matplotlib \+ cartopy\)
{{< /details >}}


## Basic plotting flow

1. Have <u>data</u> \(to plot\) with latitude and longitude columns;
2. Get <u>map</u> \(vector map/shape file/polygons/tiles/webmap\) of the desired range; \(some packages, like Basemap, seem to come with global and US maps, but not of other countries\)
3. Import both datasets;
4. Plot map data first, then layer the actual data on top of it.

### Main usage of some packages

<!-- : If you only have points, and do not plan to bring your own map, there is really no need for it. -->

I will be mainly using `matplotlib` and `seaborn` to plot with `cartopy`. If I got extra time, I will try out `geoplot` as well.

`geopandas`
: Pandas DataFrame equivalence for data or map that are geographical polygons. Also plots the polygons and points.
: [Introduction to GeoPandas — GeoPandas 0+untagged.50.g5558c35.dirty documentation](https://geopandas.org/en/stable/getting_started/introduction.html)

`contextily`
: Auto-add webmap to data plot as background image.
: [Introduction guide to contextily — contextily 1.1.0 documentation](https://contextily.readthedocs.io/en/latest/intro_guide.html)

`xyzservices`
: API interfaces that contextily uses. Sometimes debugging contextily unavoidably leads to it, for example, looking for the now gone `Stamen` provider.
: [Gallery - xyzservices 2023.10.1](https://xyzservices.readthedocs.io/en/stable/gallery.html)

`cartopy`
: Handle map projection of plots \(Matplotlib axes\) and data to be plotted on those axes.
: [Gallery — cartopy 0.22.0 documentation](https://scitools.org.uk/cartopy/docs/latest/gallery/index.html)

`matplotlib`/`seaborn`
: My go-to Python plotting packages. See [Matplotlib/Seaborn](/programming/python/matplotlib-seaborn/).

`geoplot`
: Claims to be a geospatial version of `seaborn`. May try later.
: [Gallery — geoplot 0.5.0 documentation](https://residentmario.github.io/geoplot/gallery/index.html)

Others
: I was told that `folium`, `plotly`, `bokeh`, `geoviews` and many other plotting packages could plot geospatial figures as well. But since I am already familiar with `matplotlib` and `seaborn`, I decided against trying other packages. I remember trying `bokeh` a few years ago, but did not stick with it for some reason.

### How to get dataset with latitude/longitude

Datasets with lat/lon:

- [Introduction of geodatasets - geodatasets 2023.3.1.dev6+gfb9ce89](https://geodatasets.readthedocs.io/en/latest/introduction.html)

Convert postcode to lat/long:

- Worldwide by-country lookup TSVs: [GeoNames](https://download.geonames.org/export/zip/?C=N;O=D) \(column names: `["country code", "postal code", "place name", "admin name1", "admin code1", "admin name2", "admin code2", "admin name3", "admin code3", "latitude", "longitude", "accuracy"]`, see `readme.txt`\)
    - Python wrapper: [symerio/pgeocode](https://github.com/symerio/pgeocode) \(does not support the "full" version for CA,NL and UK yet\)
- [geopandas.tools.geocode](https://geopandas.org/en/stable/docs/reference/api/geopandas.tools.geocode.html): [geopy/geopy](https://github.com/geopy/geopy) wrapper. Most decent providers \(like Google\) require API keys.

### How to get map

Two methods, bring your own map \(as polygons or image\) and plot them manually, or use some packages to download and plot automatically.

I am a lazy person. So far, I've found two different automatic approach, using `cartopy` and `contextily`, respectively.

#### Adding map with `cartopy`

It is not maps _per se_, but I will be abusing the "feature" function in `cartopy` as makeshift maps.

Refs:

- [Maps with Cartopy - Research Computing in Earth Sciences](https://rabernat.github.io/research_computing_2018/maps-with-cartopy.html)
- [matplotlib - Borders and coastlines interfering in Python Cartopy - Stack Overflow](https://stackoverflow.com/a/62312238)
- [cartopy.mpl.geoaxes.GeoAxes — cartopy 0.22.0 documentation](https://scitools.org.uk/cartopy/docs/latest/reference/generated/cartopy.mpl.geoaxes.GeoAxes.html#cartopy.mpl.geoaxes.GeoAxes.add_image)
- [List of named colors — Matplotlib 3.8.3 documentation](https://matplotlib.org/stable/gallery/color/named_colors.html#css-colors)

Toy example with no projection:

```python {hl_lines="4"}
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import cartopy.feature as cfeature

# define extra features
states_provinces = cfeature.NaturalEarthFeature(
    category='cultural',
    name='admin_1_states_provinces_lines',
    scale='50m',
)
urban_areas = cfeature.NaturalEarthFeature(
    category='cultural',
    name='urban_areas',
    scale='50m',
)

# begin plotting
plt.clf()
fig,ax = plt.subplots()
sns.scatterplot(ax=ax, data=df, x="longitude", y="latitude", hue="Rating")

# start cartopy settings
ax.set_global()

ax.add_feature(cfeature.LAND, facecolor="silver")
# ax.add_feature(cfeature.OCEAN)
# ax.add_feature(cfeature.COASTLINE, edgecolor="silver")
ax.add_feature(cfeature.BORDERS, edgecolor="white")
# ax.add_feature(states_provinces, linestyle=':', edgecolor="white", facecolor="none")
# ax.add_feature(cfeature.LAKES)
# ax.add_feature(cfeature.RIVERS, edgecolor="white")
# ax.add_feature(urban_areas, facecolor="silver, alpha=0.5)

ax.gridlines(draw_labels=True, alpha=0.3)

# matplotlib settings
ax.legend(frameon=True)
plt.show()
```

{{< details "`ax.add_image`" >}}
`cartopy` has its own `ax.add_image` and `cartopy.io.img_tiles` methods, but the documentation is very ambiguous and the method not easy to use.

Docs:

- [cartopy.mpl.geoaxes.GeoAxes — cartopy 0.22.0 documentation](https://scitools.org.uk/cartopy/docs/latest/reference/generated/cartopy.mpl.geoaxes.GeoAxes.html#cartopy.mpl.geoaxes.GeoAxes.add_image)
- [Input/output capabilities — cartopy 0.22.0 documentation](https://scitools.org.uk/cartopy/docs/latest/reference/io.html#module-cartopy.io.img_tiles)
- [Map tile acquisition — cartopy 0.22.0 documentation](https://scitools.org.uk/cartopy/docs/latest/gallery/scalar_data/eyja_volcano.html)

Toy example with no projection: \(remember `Stamen` is no longer available\)

```python {hl_lines="4"}
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import cartopy.io.img_tiles as cimgt

# begin plotting
plt.clf()
fig,ax = plt.subplots()
sns.scatterplot(ax=ax, data=df, x="longitude", y="latitude", hue="Rating")

# cartopy settings
ax.set_global()
ax.add_image(cimgt.OSM(), 5) # the larger zoom level, the smaller the label fonts
ax.gridlines(draw_labels=True, alpha=0.3)

# matplotlib settings
ax.legend(frameon=True)
plt.show()
```
{{< /details >}}

#### Adding map with `contextily`

The maps are beautiful out of the box, but handling projection becomes a problem if you are not using `geopandas`.

Ref: [Creating a Map with XYZ Tiles using Geopandas, Matplotlib, Contextily, and XYZServices | Tutorials/Post - Remote Sensing, GIS, Earth System, Geo-AI/ML](https://thegeoint.com/article/2023/12/7/14.html)

Toy example with `cartopy` and `seaborn` with no projection, which translates to equirectangular projection on plot axes, aka `PlateCarree`:

```python {linenos="table", hl_lines="2 16"}
import pandas as pd
import contextily as ctx
import matplotlib.pyplot as plt
import seaborn as sns

# begin plotting
plt.clf()
fig,ax = plt.subplots()
sns.scatterplot(ax=ax, data=df, x="longitude", y="latitude", hue="Rating")

# add map to background
ctx.add_basemap(
    ax,
    source=ctx.providers.CartoDB.Positron,
    zoom="auto",
    crs="EPSG:4326",
)

# matplotlib settings
ax.legend()
ax.set_xlabel('Longitude')
ax.set_ylabel('Latitude')
plt.show()
```

A more involved way of using the `add_basemap` function that I have yet to try: [Adding a background map to plots — GeoPandas 0+untagged.50.g5558c35.dirty documentation](https://geopandas.org/en/stable/gallery/plotting_basemap_background.html#Adding-labels-as-an-overlay)

<!-- 
```python
ax = df_wm.plot(figsize=(10, 10), alpha=0.5, edgecolor="k")
cx.add_basemap(ax, source=cx.providers.CartoDB.PositronNoLabels, zoom=12)
cx.add_basemap(ax, source=cx.providers.CartoDB.PositronOnlyLabels, zoom=10)
```
 -->

## Arbitrary map projection with `cartopy` and `seaborn`

Most examples online read as if only FacetGrid could use custom projections, which is not true. I think any plot could use any projection with a proper amount of `matplotlib` setup.

Refs:

- [Matplotlib interface (cartopy.mpl) — cartopy 0.22.0 documentation](https://scitools.org.uk/cartopy/docs/latest/reference/matplotlib.html) \(most important info: `class cartopy.mpl.geoaxes.GeoAxes` is a subclass of `matplotlib.axes.Axes`\)
- [Faceted maps with Seaborn and Cartopy.ipynb](https://gist.github.com/shoyer/16db9cd187886a3effd8)

### `projection` vs `transform`

Refs:

- [Understanding the transform and projection keywords — cartopy 0.22.0 documentation](https://stackoverflow.com/a/57086213)
- [Cartography and Mapping in Python](https://uoftcoders.github.io/studyGroup/lessons/python/cartography/lesson/)
- [Cartopy projection list — cartopy 0.22.0 documentation](https://scitools.org.uk/cartopy/docs/latest/reference/projections.html)
- [cartopy.crs.epsg — cartopy 0.22.0 documentation](https://scitools.org.uk/cartopy/docs/latest/reference/generated/cartopy.crs.epsg.html)
- [python - Use ccrs.epsg() to plot zipcode perimeter shapefile with EPSG 4326 coordinate system - Stack Overflow](https://stackoverflow.com/questions/57030906/use-ccrs-epsg-to-plot-zipcode-perimeter-shapefile-with-epsg-4326-coordinate-sy)

### Example with `cartopy` features

TBA

<!-- 

### Example with `contextily` map

> Refs for using `geopandas` CRS methods: \(haven't tried\)
> 
> - [Plotting Maps With Geopandas and Contextily | by Gauti Sigthorsson | Geek Culture | Medium](https://archive.is/x2LsX)
> - [Creating a basemap in python using contextily | Andrew Wheeler](https://andrewpwheeler.com/2020/06/25/creating-a-basemap-in-python-using-contextily/)
{.book-hint .info}

Sometimes you need to manually get the CRS \(short for Coordinate Reference System\) data. It is weird to me that the projected axes from `cartopy` do not talk with `contextily`, but I can do nothing about it.

On [EPSG.io](https://epsg.io/), find the CRS that you use for `projection`. For example, [ETRS89-extended / LAEA Europe - EPSG:3035](https://epsg.io/3035). Find and copy the `PROJ.4` text from the Export section.

This is not the projection I used, but I imagine it would work:

```python {hl_lines="5 8-10 15 20 28"}
import pandas as pd
import contextily as ctx
import matplotlib.pyplot as plt
import seaborn as sns
import cartopy.crs as ccrs

# define projection systems
projection = ccrs.epsg(3035)        # use this when creating axes
transform = ccrs.PlateCarree()      # use this when plotting
crs = ccrs.CRS("+proj=laea +lat_0=52 +lon_0=10 +x_0=4321000 +y_0=3210000 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs +type=crs")  # use this with contextily

# begin plotting
plt.clf()
fig = plt.figure(figsize=(10, 10))
ax = fig.add_subplot(1, 1, 1, projection=projection)
sns.scatterplot(
    ax=ax,
    data=df,
    x='longitude', y='latitude', hue="Rating",
    transform=transform,
)

# add map to background
ctx.add_basemap(
    ax,
    source=ctx.providers.CartoDB.Positron,
    zoom="auto",
    crs=crs,
)

# matplotlib settings
ax.legend()
ax.set_xlabel('Longitude')
ax.set_ylabel('Latitude')
plt.show()
```

 -->


## Calculations

### Distance

Example from: [python - Getting distance between two points based on latitude/longitude - Stack Overflow](https://stackoverflow.com/questions/19412462/getting-distance-between-two-points-based-on-latitude-longitude), [my answer](https://stackoverflow.com/a/78207442/10668706)

```python
import cartopy.geodesic as cgeo

coords_1 = (52.2296756, 21.0122287)
coords_2 = (52.406374, 16.9251681)
coords_3 = (52.406374, 10)

# Note: cartopy only accepts lon-lat pairs!!
globe = cgeo.Geodesic()

inv = globe.inverse(coords_1[::-1], coords_2[::-1])
print(inv.T[0]/1000)
# [279.3529016]

inv_2 = globe.inverse(coords_1[::-1], [coords_2[::-1], coords_3[::-1]])
print(inv_2.T[0]/1000)
# [279.3529016  750.45799898]
```

Wrapper function for easier usage with DataFrame:

```python
import cartopy.geodesic as cgeo

def distance(longitudes, latitudes):
    assert(1 < len(longitudes))
    assert(1 < len(latitudes))
    assert(len(longitudes) == len(latitudes))

    places = list(zip(longitudes, latitudes))
    globe = cgeo.Geodesic()
    inv = globe.inverse(places[0], places[1:])
    return (inv.T[0]/1000)
```


## Entertainment

[xkcd: Map Projections](https://xkcd.com/977/)  
[977: Map Projections - explain xkcd](https://www.explainxkcd.com/wiki/index.php/977:_Map_Projections)  
[xkcd's "Map Projections", animated - YouTube](https://www.youtube-nocookie.com/embed/7O2CBgWshiM) gives an idea how much the lands are distorted when you spin the globe with each projection.
