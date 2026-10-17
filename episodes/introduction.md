---
title: "Introduction to Foundations"
teaching: 20
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- What do I need to know before starting the other modules?
- Which tools does this curriculum use, and what is each one for?
- How do Google Colab notebooks work?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Describe what Python, Jupyter notebooks, Google Colab and QGIS are used for
- Open a notebook in Colab, save your own copy and run its cells
- Choose the right tool for a simple geospatial task
- Find your way through the modules of the curriculum

::::::::::::::::::::::::::::::::::::::::::::::::

## Why a foundations module?

The other modules in this curriculum assume a little background: how to run a Python notebook, what a
table and a map layer are, and how to load data into QGIS. This module teaches exactly that, from zero.
If you have never written code or opened a GIS, start here. If you already know some Python or QGIS, skim
the episodes and use the notebooks as a refresher.

## The tools

| Tool | What it is | What we use it for |
|---|---|---|
| **Python** | A free, general-purpose programming language with excellent libraries for data and maps | Reading, cleaning, analyzing and mapping data in a repeatable way |
| **Jupyter notebook** | A document that mixes text, code and results | Every Python lesson in the curriculum |
| **Google Colab** | A free service that runs Jupyter notebooks in your web browser | Running the notebooks without installing anything |
| **QGIS** | A free, open source desktop GIS | Looking at data, styling layers and making finished maps |

Python and QGIS are not rivals. Many projects use both: Python to download and prepare data, and QGIS to
check it visually and design the final map. Both read the same file formats (GeoJSON, GeoPackage,
shapefile, GeoTIFF).

## Working in Google Colab

Every notebook link in this curriculum opens in Colab. The first time:

1. Make sure you are signed in to a Google account.
2. Click the notebook link. It opens read-only, straight from GitHub.
3. Choose **File > Save a copy in Drive**. Your copy keeps your changes; the original stays clean.
4. Run cells from top to bottom: click a cell and press **Shift + Enter**.
5. If Colab warns that the notebook was not written by Google, click **Run anyway**.

A few things to know:

- **Order matters.** Later cells use variables made in earlier cells. If you skip a cell, you will see a
  `NameError`. Use **Runtime > Run before** to catch up.
- **Sessions end.** After a while without activity, Colab disconnects and forgets everything in memory.
  Reconnect and rerun the cells from the top.
- **Files are temporary.** Files you create appear in the **Files** panel on the left and disappear when the
  session ends. Download anything you want to keep.
- **Data comes from the web.** All notebooks read their data straight from a web address, so you never need
  to download data by hand.

::::::::::::::::::::::::::::::::::::: callout

### Do I need to install Python?

No. Colab runs Python on Google's computers and already includes the libraries used in this curriculum
(pandas, matplotlib, GeoPandas). If you prefer to work on your own computer, the [Setup](../learners/setup.md)
page explains how to install Python with Anaconda.

::::::::::::::::::::::::::::::::::::::::::::::::

## What this module covers

| Episode | You will learn | Notebooks |
|---|---|---|
| Python Basics | Running cells, variables, text, lists, dictionaries, decisions, loops and functions | 2a to 2f |
| Working with Data | Tables with pandas and charts with matplotlib | 3a and 3b |
| Geospatial Python Basics | Map layers with GeoPandas, coordinate reference systems, and joining data | 4a to 4c |
| Getting Started with QGIS | Loading data from the web, styling layers and making a finished map layout | none (QGIS) |

## Where to go next

After this module, the curriculum follows the life of a research dataset:

1. [Data Management](https://spatialturn.github.io/DataManagement/): data models, formats, coordinate
   systems and planning
2. [Data Collection](https://spatialturn.github.io/DataCollection/): repositories, census data,
   geocoding, imagery and field data
3. [Data Analysis](https://spatialturn.github.io/DataAnalysis/): network analysis, spatial
   autocorrelation, clustering and NDVI
4. [Data Visualization](https://spatialturn.github.io/DataVisualization/): charts, map design and
   accessibility
5. [Data Curation](https://spatialturn.github.io/DataCuration/): metadata, documentation, preservation
   and sharing
6. [Case Studies](https://spatialturn.github.io/CaseStudies/): food deserts and grocery access, from
   start to finish

:::::::::::::::::::::::::::::::::::: challenge

## Which tool?

Would you reach for Python (in Colab), QGIS, or both?

1. Download median income for every county in the United States and calculate a new column
2. Design a printed poster map of a city's parks with a legend and scale bar
3. Check whether a layer someone sent you lines up with the roads
4. Repeat the same analysis every month when new data is published

:::::::::::::::: solution

1. **Python.** Downloading thousands of rows and calculating columns is quick to code and easy to repeat.
2. **QGIS.** Its print layout is made for finished maps.
3. **QGIS**, for a quick visual check over a basemap (Python could check it too).
4. **Python.** A notebook can be rerun each month with the new data, giving the same steps every time.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Python (in Jupyter notebooks on Google Colab) is for repeatable data work; QGIS is for looking at data and
  making maps
- Save your own copy of each notebook, and run cells in order with Shift + Enter
- Colab sessions and files are temporary; data is always read from the web
- This module prepares you for every other module in the curriculum

::::::::::::::::::::::::::::::::::::::::::::::::
