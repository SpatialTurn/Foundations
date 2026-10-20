---
title: "Map Your County in Python"
teaching: 10
exercises: 50
---

:::::::::::::::::::::::::::::::::::::: questions

- Can I take a Census table and boundaries all the way to a finished, shareable map on my own?
- What makes a map "finished"?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Join a Census table to tract boundaries and check the join
- Clean Census "no estimate" codes and zero denominators before calculating rates
- Choose a classification for a skewed rate and show missing data honestly
- Export a map with a title, legend, scale bar, north arrow and source line

::::::::::::::::::::::::::::::::::::::::::::::::

## The capstone

This episode is a small project that uses everything in the Python part of Foundations: reading data from the
web (notebooks 3a and 4a), coordinate systems (4b), joins (4c) and plotting (3b). The instructions are shorter
than before. Each step says what to do and offers a hint and a hidden solution, so try first and peek only when
you are stuck.

**The brief.** A local food bank wants a one-page map of where households without a car live in Tippecanoe
County, Indiana, to plan a delivery service. You will deliver it as a PNG image that a reader with no GIS
experience can understand.

The data is the same as in the QGIS version of this capstone, so you can compare your result with a
colleague who uses QGIS:

| File | Contents |
|---|---|
| `tippecanoe_tracts.geojson` | 43 census tract boundaries with `GEOID` |
| `tippecanoe_acs_2024.csv` | ACS 2024 5-year estimates per tract, downloaded once from the Census API for this lesson |

An optional last section shows how to make the same map for **your own county**, using your own Census API key.

## What a finished map needs

A map leaves your hands and is read without you there to explain it. It needs to answer four questions on its
own:

| Question | Map element |
|---|---|
| What is shown, and in what units? | A **title** (ideally stating the finding) and a **legend** with units |
| Where is it, and how big? | Recognizable shapes, a **scale bar**, a **north arrow** |
| Where does the data come from, and when? | A **source line** with the dataset and year |
| What is missing? | A visible **no data** class, never a misleading zero |

## Three traps in real Census tables

You will meet all three in this capstone:

1. **IDs as numbers.** Read `GEOID` as text, or leading zeros vanish and joins fail in states with codes that
   start with 0.
2. **Special codes.** The Census Bureau writes **-666666666** where it cannot estimate a value (median income in
   two Purdue tracts here). Replace codes with missing values before any calculation.
3. **Zero denominators.** A tract made of residence halls has people but **no households**, so a rate per
   household does not exist there. It must be missing, not 0%.

:::::::::::::::::::::::::::::::::::: challenge

## Challenge: Which classification?

The share of households without a vehicle ranges from under 1% to about 41%, and most tracts are below 10%.
Which classification would you use for a five-class choropleth: equal interval, quantile, or natural breaks?

:::::::::::::::: solution

With a **skewed** distribution, equal interval puts most tracts in the lowest one or two classes and wastes the
rest. **Natural breaks** follows the gaps in the data and shows both the many low tracts and the few very high
ones; **quantile** (equal counts) gives every class the same number of tracts, which is good for rankings but
can split similar values. The notebook uses natural breaks. Whatever you choose, say so in the legend or a note.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Join, then check: row counts and unmatched rows
- Clean special codes and zero denominators before computing rates
- Project to meters, pick classes that suit the distribution, and show missing data clearly
- A finished map has a title, legend with units, scale bar, north arrow and source line

::::::::::::::::::::::::::::::::::::::::::::::::

## Notebook

| Notebook | What you will do |
|---|---|
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/05a_Map_Your_County.ipynb" target="_blank">5a. Map Your County</a> | Join, clean, classify and finish a map of households without a car, then a poverty map; optionally repeat it for your own county |
