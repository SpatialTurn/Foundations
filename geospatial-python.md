---
title: "Geospatial Python Basics"
teaching: 30
exercises: 75
---

:::::::::::::::::::::::::::::::::::::: questions

- How does Python store and map geographic data?
- What is a coordinate reference system, and why does it matter for measuring?
- How do I combine a table with a map layer, or two layers with each other?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Read vector data from the web into a GeoPandas GeoDataFrame and map it
- Check, convert and correctly label a layer's coordinate reference system
- Measure areas and distances in meters
- Combine data with attribute joins and spatial joins

::::::::::::::::::::::::::::::::::::::::::::::::

## Vector data and GeoDataFrames

Most social science maps use **vector** data: **points** (a store, a survey respondent), **lines** (a road,
a river) and **polygons** (a county, a census tract). Each feature has a shape and a row of attributes.

**GeoPandas** stores vector data as a **GeoDataFrame**: a pandas DataFrame with one extra `geometry` column.
Everything from the previous episode (selecting, filtering, sorting, new columns) still works, and maps are
one line away.

```python
import geopandas as gpd

url = "https://raw.githubusercontent.com/SpatialTurn/Foundations/main/data/indiana_counties.geojson"
counties = gpd.read_file(url)
counties.plot(column="unemp_2016", cmap="YlOrRd", legend=True)
```

`gpd.read_file()` reads GeoJSON, shapefiles (also zipped ones) and GeoPackages, from a file or a web address.
Shade areas by **rates** (unemployment, density), not raw counts, or big counties will dominate the map
simply because they are big.

## Coordinate reference systems

Coordinates are only numbers; the **coordinate reference system** (CRS) says what they mean. Web data is
usually in **EPSG:4326**: latitude and longitude, in degrees. Degrees are fine for storing data, but a degree
of longitude shrinks from about 111 km at the equator to about 85 km in Indiana, so areas and distances
calculated in degrees are meaningless.

| Method | What it does | When to use it |
|---|---|---|
| `layer.crs` | Shows the CRS | Always, before combining or measuring layers |
| `layer.to_crs(epsg=26916)` | **Converts** the coordinates to another CRS | Before measuring, or to match another layer |
| `layer.set_crs(epsg=4326)` | **Labels** a layer whose CRS is missing; the numbers do not change | Only when the CRS is missing and you know what it should be |

For Indiana, **EPSG:26916** (UTM zone 16N, in meters) is a good choice for local distances, and **EPSG:5070**
(USA Contiguous Albers Equal Area) for areas across the state or the country. The Data Management module's
[Coordinate Reference Systems](https://spatialturn.github.io/DataManagement/crs.html) episode explains
datums and projections in depth.

## Joining data

| Join | Matches rows by | GeoPandas |
|---|---|---|
| **Attribute join** | A shared ID, such as a FIPS code or GEOID | `layer.merge(table, on="fips")` |
| **Spatial join** | Location: which polygon contains each point | `gpd.sjoin(points, polygons, predicate="within")` |

The most common reason an attribute join fails is that the ID is text in one table and a number in the
other. Convert both to text (and pad with `zfill()` to the right length) before joining, and always compare
the row counts before and after. A spatial join needs both layers in the same CRS.

:::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: set_crs or to_crs?

1. A shapefile arrives with no CRS. Its metadata says the coordinates are latitude and longitude (WGS 84).
2. You need the distance in meters between two stores stored in EPSG:4326.
3. One layer is in EPSG:4326 and another in EPSG:26916, and you want to draw them together.

:::::::::::::::: solution

1. `set_crs(epsg=4326)`: the CRS is missing and you know what it is, so you only add the label.
2. `to_crs(epsg=26916)` first, then measure: the coordinates must be converted to meters.
3. `to_crs()` one layer to match the other, for example `layer2.to_crs(layer1.crs)`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::: challenge

## Challenge 2: Why did the join fail?

You join a table of tract statistics to tract boundaries on `GEOID`, and every row of the result has empty
statistics. What would you check first?

:::::::::::::::: solution

Check the type and format of `GEOID` in both tables. A common cause is that one table stores it as text
(`"18157010400"`) and the other as a number (`18157010400`), or that leading zeros were lost (a California
tract `"06001400100"` read as the number `6001400100`). Convert both to text with
`.astype(str).str.zfill(11)` (11 characters for tracts) and join again. Also check that both tables cover the
same year, because tract boundaries change between censuses.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- A GeoDataFrame is a pandas DataFrame plus a `geometry` column; `gpd.read_file()` reads it from the web
- Check `.crs` first; use `to_crs()` to a projected CRS in meters before measuring, and `set_crs()` only to
  label missing CRS information
- Attribute joins match IDs (make them the same type first); spatial joins match locations (same CRS first)

::::::::::::::::::::::::::::::::::::::::::::::::

## Notebooks

| Notebook | What you will do |
|---|---|
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/04a_Vector_Data_with_GeoPandas.ipynb" target="_blank">4a. Vector Data with GeoPandas</a> | Read Indiana counties and Lafayette food stores, make a choropleth and layer points over polygons |
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/04b_Coordinate_Reference_Systems.ipynb" target="_blank">4b. Coordinate Reference Systems</a> | Compare areas in degrees and meters, measure a distance, and see what a wrong CRS label does |
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/04c_Joining_Tables_and_Layers.ipynb" target="_blank">4c. Joining Tables and Layers</a> | Fix a failing FIPS join, then find which stores lie inside the city limits |
