---
title: "Map Your County in QGIS"
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
- Export a print layout with a title, legend, scale bar, north arrow and source line

::::::::::::::::::::::::::::::::::::::::::::::::

## The capstone

This episode is a small project that uses everything in the QGIS part of Foundations: loading data from the web
and making a layout ([Getting Started with QGIS](qgisintro.md)), and joins, the Field Calculator and selections
([Tables, Joins and Selections](qgis-tables.md)). The instructions are shorter than before: each step says what
to do and which earlier part shows how. Try first, and open the hints only when you are stuck.

**The brief.** A local food bank wants a one-page map of where households without a car live in Tippecanoe
County, Indiana, to plan a delivery service. You will deliver it as a PNG image that a reader with no GIS
experience can understand.

The data is the same as in the [Python version](map-your-county-python.md) of this capstone, so you can compare
your result with a colleague who uses Python:

| Dataset | Web address |
|---|---|
| Census tracts | `https://raw.githubusercontent.com/SpatialTurn/Foundations/main/data/tippecanoe_tracts.geojson` |
| ACS 2024 table | `https://raw.githubusercontent.com/SpatialTurn/Foundations/main/data/tippecanoe_acs_2024.csv` |

## What a finished map needs

A map leaves your hands and is read without you there to explain it. It needs to answer four questions on its
own:

| Question | Map element |
|---|---|
| What is shown, and in what units? | A **title** (ideally stating the finding) and a **legend** with units |
| Where is it, and how big? | Recognizable shapes, a **scale bar**, a **north arrow** |
| Where does the data come from, and when? | A **source line** with the dataset and year |
| What is missing? | A visible **no data** class, never a misleading zero |

---

## Steps

### 1. Start a project

Create a folder for the capstone, start a new QGIS project and save it there. Set the project CRS to
**EPSG:26916** (UTM zone 16N), so the map is not stretched and the scale bar is true.

::::::::::::::::::::::::::::::::::::: spoiler

### Hint

Click the CRS button at the bottom right of the QGIS window, search for `26916` and click **OK**.

:::::::::::::::::::::::::::::::::::::::::::::

### 2. Load and join

Load both web addresses, join the table to the tracts on `GEOID`, and check that no tract is left without a
match.

::::::::::::::::::::::::::::::::::::: spoiler

### Hint

[Tables, Joins and Selections](qgis-tables.md), Parts 1 to 3: **Properties > Joins**, then select
`"acs_total_pop" IS NULL` in the attribute table. 0 selected means every tract matched.

:::::::::::::::::::::::::::::::::::::::::::::

### 3. Calculate the rate

Create a virtual field `pct_no_vehicle`: households without a vehicle as a percentage of all households. Check
what happens in Census Tract 104.

::::::::::::::::::::::::::::::::::::: spoiler

### Hint

Field Calculator, virtual field (ticked automatically for this read-only layer), **Decimal (double)**:
`"acs_hh_no_vehicle" / "acs_households" * 100`. Tract 104 (Purdue residence halls) has 0 households, so the
result is NULL there, which is correct.

:::::::::::::::::::::::::::::::::::::::::::::

### 4. Style the choropleth

Use **Graduated** symbology on `pct_no_vehicle` with 5 classes and a sequential color ramp. Look at the
histogram first and choose a classification mode that suits a skewed distribution. Then make sure the tract with
no value is shown as **no data**, not left out or colored like a low value.

::::::::::::::::::::::::::::::::::::: spoiler

### Hint

- In the Graduated panel, the **Histogram** tab (click **Load Values**) shows most tracts below 10% and a few
  far higher. **Natural Breaks (Jenks)** suits this.
- QGIS leaves features with NULL values undrawn in a Graduated style. To show them, open
  **Layer Styling** or **Properties > Symbology**, switch to **Rule-based**, and add a rule with the filter
  `"pct_no_vehicle" IS NULL`, a light gray symbol and the label "No households (dorms)". A quicker alternative:
  load the tracts a second time below the styled layer with a light gray hatch fill, and name it "No data".
- Use a pale outline (white or light gray, 0.2 mm) so small tracts in the city stay readable.

:::::::::::::::::::::::::::::::::::::::::::::

### 5. Compose the layout

Create a print layout with the map, a title that states the finding, a legend with units and without extra
layers, a scale bar in kilometers or miles, a north arrow and a source line. Add an inset or zoom on the cities
if the small urban tracts are hard to see (optional).

::::::::::::::::::::::::::::::::::::: spoiler

### Hint

[Getting Started with QGIS](qgisintro.md), Part 6. A good source line: "Data: U.S. Census Bureau, American
Community Survey 2020-2024 5-year estimates, census tracts. Map by (your name), 2026." For a zoom, add a second
map item, set its extent to the cities, and tick **Overviews** on the main map to show where the zoom is.

:::::::::::::::::::::::::::::::::::::::::::::

### 6. Export and check

Export the layout as a PNG at 200 dpi or more. Then read it as a stranger would, using the table above.

---

:::::::::::::::::::::::::::::::::::: challenge

## Challenge: A second map

Make a second finished map, of the **poverty rate** (`below_poverty` as a share of `poverty_universe`). Many of
the highest-poverty tracts are near Purdue. Add one sentence to the map that explains why.

:::::::::::::::: solution

Virtual field `poverty_rate` = `"acs_below_poverty" / "acs_poverty_universe" * 100` (NULL for tract 104, where
the poverty universe is 0). The highest rates, around 70 to 80%, are in tracts near campus with many students,
who often report low incomes while supported by family or loans. A note such as "Tracts near Purdue have many
students, who often report low incomes" keeps readers from misreading the map.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

## Your own county

To map another county, download its state's tract boundaries from the Census Bureau's
[cartographic boundary files](https://www.census.gov/geographies/mapping-files/time-series/geo/cartographic-boundary.html)
(a zipped shapefile can be added to QGIS without unzipping), filter it to your county with **Filter...** and
`"COUNTYFP" = '157'` (your county's code), and request the ACS table with your own Census API key as shown in
the Data Collection module's [Census episode](https://spatialturn.github.io/DataCollection/census.html). The
Python version of this capstone has a ready-made cell for the table.

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Join, then check for unmatched features
- Clean special codes and zero denominators before computing rates
- Pick classes that suit the distribution, and show missing data as its own class
- A finished map has a title, legend with units, scale bar, north arrow and source line

::::::::::::::::::::::::::::::::::::::::::::::::
