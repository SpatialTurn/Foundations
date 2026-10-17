---
title: 'Reference'
---

## Glossary

Attribute join
:   Combining a table with a layer by matching a shared ID column, such as a FIPS code. In pandas and
    GeoPandas, `merge()`.

Choropleth map
:   A map that shades each area by a value. Use rates or densities rather than raw counts.

Coordinate reference system (CRS)
:   The system that says what coordinates mean, identified by an EPSG code such as EPSG:4326 (latitude and
    longitude, in degrees) or EPSG:26916 (UTM zone 16N, in meters).

CSV
:   Comma-separated values: a plain text table, one row per line, with columns separated by commas.

DataFrame
:   A pandas table with labeled columns, each with one data type.

Dictionary
:   A Python collection of `key: value` pairs, written in curly brackets.

EPSG code
:   A number that identifies a coordinate reference system, from a registry first kept by the European
    Petroleum Survey Group.

f-string
:   A Python string with an `f` before the quote, in which `{ }` is replaced by a value: `f"{name} County"`.

FIPS code
:   A Federal Information Processing Standards code identifying a U.S. state (2 digits) or county (5 digits,
    state plus county). Store it as text.

Function
:   A named, reusable piece of code that takes inputs (parameters) and can return a result.

GeoDataFrame
:   A GeoPandas DataFrame with a `geometry` column holding a shape for each row.

GeoJSON
:   A text format for vector data, common on the web. Usually in EPSG:4326.

Index
:   The position of an item in a list or string. Python counts from 0.

Library
:   A package of ready-made code loaded with `import`, such as pandas or GeoPandas.

List
:   A Python collection of values in order, written in square brackets.

Projected CRS
:   A coordinate reference system on a flat map, with units such as meters. Needed to measure distances and
    areas.

QGIS
:   A free, open source desktop Geographic Information System.

Spatial join
:   Combining two layers by location, for example finding which polygon each point falls inside. In
    GeoPandas, `gpd.sjoin()`.

String
:   Text in Python, written inside quotes.

Variable
:   A name that points to a value, created with `=`.

Vector data
:   Data stored as points, lines or polygons, each with a row of attributes.

## Further reading

- [Python tutorial](https://docs.python.org/3/tutorial/) (the official one, thorough)
- [pandas: 10 minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html)
- [matplotlib tutorials](https://matplotlib.org/stable/tutorials/index.html)
- [GeoPandas: introduction](https://geopandas.org/en/stable/getting_started/introduction.html)
- [QGIS training manual](https://docs.qgis.org/latest/en/docs/training_manual/)
- [Software Carpentry: Plotting and Programming in Python](https://swcarpentry.github.io/python-novice-gapminder/)
