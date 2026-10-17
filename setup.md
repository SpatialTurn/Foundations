---
title: Setup
---

This page is the central setup guide for the whole curriculum. Other modules link here instead of repeating
these steps. Everything is free.

| You need | For | Section |
|---|---|---|
| A Google account | Running notebooks in Google Colab | [Part 1](#part-1-google-colab) |
| QGIS installed on a computer | QGIS episodes (this module, Data Collection, Data Visualization, Case Studies) | [Part 2](#part-2-install-qgis) |
| A Census API key | Notebooks that download Census data (Data Collection, Data Analysis, Case Studies) | [Part 3](#part-3-get-a-census-api-key) |

## Part 1: Google Colab

Colab runs Jupyter notebooks in your web browser, so there is nothing to install.

1. Sign in to a Google account (any Gmail account works).
2. Click a notebook link in any episode's **Notebooks** table. It opens in Colab.
3. Choose **File > Save a copy in Drive** so your changes are kept.
4. Run cells from top to bottom: click a cell and press **Shift + Enter**.
5. If Colab warns that the notebook was not written by Google, click **Run anyway**.

All notebooks read their data straight from the web, so you never need to download data by hand. pandas,
matplotlib and GeoPandas come installed in Colab; when a notebook needs anything else, its first cell
installs it with `!pip install`.

## Part 2: Install QGIS

**QGIS** is a free, open source Geographic Information System for viewing, analyzing and mapping spatial data.

1. Go to <https://qgis.org> and click **Download**.
2. Choose the **Long Term Release (LTR)** version, the most stable one.
   - **Windows:** the standalone installer (`.msi`)
   - **macOS:** the macOS installer (`.dmg`). The first time you open QGIS, you may need to right-click the
     app and choose **Open** to get past the security warning.
   - **Linux:** follow the instructions for your distribution on the QGIS download page
3. Run the installer and keep the default settings.
4. Open **QGIS Desktop** (not "QGIS with GRASS" or other variants, if several are listed).

### The QGIS window

![The main parts of the QGIS window](qgisinterface.png){alt="Screenshot of an empty QGIS project window with yellow labels marking its main parts: the menu bar and toolbars across the top, the Browser panel at upper left listing folders and data sources, the Layers panel at lower left, the large map view on the right, and the status bar along the bottom showing coordinates, scale, magnifier, rotation and the project coordinate system."}

| Part | What it does |
|---|---|
| **Menu bar** | All commands, organized by topic (Project, Layer, Vector, Raster and so on) |
| **Toolbars** | Shortcuts for common tools such as pan, zoom and identify |
| **Browser panel** | Your files, databases and web sources, including **XYZ Tiles** basemaps |
| **Layers panel** | The layers in your project. Layers at the top are drawn on top. |
| **Map view** (canvas) | Where the map is displayed |
| **Status bar** | Coordinates under the cursor, map scale and the project's coordinate system (EPSG code) |

If a panel is missing, turn it back on with **View > Panels**.

### Loading data from a web address

Many episodes load data straight from the web:

1. **Layer > Add Layer > Add Vector Layer**
2. **Source Type**: **Protocol: HTTP(S), cloud, etc.**
3. Paste the address given in the episode into **URI**, then click **Add**

## Part 3: Get a Census API key

The U.S. Census Bureau's data API refuses requests without a key. **Every learner needs their own key.** It
is free and takes a few minutes.

1. Go to <https://api.census.gov/data/key_signup.html>.
2. Enter your organization (for example, Purdue University) and your email address, and agree to the terms.
3. Check your email. The key arrives within a few minutes.
4. **Click the activation link in the email.** The key does not work until you do.
5. Paste the key where a notebook asks for it.

Treat the key like a password: do not post it online or leave it in a notebook you share.

## Optional: Python on your own computer

Colab is the recommended way to follow the curriculum. If you prefer to work offline, install
[Anaconda](https://www.anaconda.com/download) and create an environment with the main libraries:

```bash
conda create -n spatialturn -c conda-forge python=3.11 pandas geopandas matplotlib mapclassify jupyterlab
conda activate spatialturn
jupyter lab
```

Then download a notebook from Colab (**File > Download > Download .ipynb**) and open it in JupyterLab. The data
is still read from the web, so you need an internet connection.

## Troubleshooting

| Problem | Fix |
|---|---|
| A Colab cell gives `NameError` | A cell above it was skipped; use **Runtime > Run before** |
| A Colab cell gives `ModuleNotFoundError` | Run the `!pip install` cell at the top of the notebook first |
| Colab disconnected and forgot everything | Reconnect, then **Runtime > Run all** |
| QGIS will not open on macOS | Right-click the app, choose **Open**, then confirm |
| The Browser or Layers panel is missing | **View > Panels**, then tick the panel |
| A layer loaded from a web address shows nothing | Right-click the layer and choose **Zoom to Layer**; check that the address was pasted completely |
| The basemap is blank | Check your internet connection; XYZ basemaps need to be online |
| The Census API returns "Missing Key" or "Invalid Key" | Check that you clicked the activation link, and that the key was pasted completely |
