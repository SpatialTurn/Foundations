---
title: 'Instructor Notes'
---

## Overall approach

- This module is for complete beginners. Each Python notebook takes 15 to 25 minutes and covers one idea,
  with an exercise and its solution at the end. In a live session, teach the episode page briefly, then let
  learners work through the notebooks while helpers circulate.
- Suggested timing for a full day: Introduction 30 min; Python Basics (notebooks 2a to 2f) 2.5 hours;
  Working with Data (3a, 3b) 1 hour; Geospatial Python Basics (4a to 4c) 1.5 hours. Getting Started with
  QGIS (about 1.75 hours) works well as a separate session.
- Ask everyone to **Save a copy in Drive** before running anything.
- The examples use Indiana counties and Lafayette food stores throughout, so the same data reappears in
  later modules (Data Collection, Case Studies).
- The Python notebooks were rewritten for beginners from the Workshop 2026 Session B notebook
  (`intro_python.ipynb`), which stays in its own repository unchanged.

## Episode by episode

### Introduction

- The "Which tool?" challenge is a good opener: there is no single right answer for the visual check.

### Python Basics

- Normalize errors early: run the deliberate `SyntaxError` and `NameError` cells in notebook 2a together and
  read the last line aloud.
- The "numbers stored as text" idea (2b) comes back in every Census notebook and in the join notebook (4c).

### Working with Data

- Point out that `describe()` averages the FIPS codes (3a). It is a memorable way to show why identifiers
  should be text.
- The log scale in the scatter plot (3b) is often new; show the same chart without it first.

### Geospatial Python Basics

- The wrong-CRS demonstration in 4b (Indiana ends up near the equator) makes the difference between
  `set_crs()` and `to_crs()` stick.
- In 4c, the failing join is deliberate. Let learners read the error before showing the fix.
- 58 of the 64 food stores lie inside the city limits; all 17 supermarkets do.

### Getting Started with QGIS

- Moved here from the Data Visualization module in October 2026. Data is loaded from this repository's
  `data/` folder by URL.
- The OpenStreetMap basemap needs an internet connection; on a slow network, skip it.
- Loading from a web address (Layer > Add Layer > Add Vector Layer > Protocol: HTTP(S)) avoids file
  downloads and path problems. If a network blocks it, the same GeoJSON files can be downloaded from the
  repository's `data/` folder and loaded as files.
- In QGIS, the OpenStreetMap basemap works normally. (In Colab it does not, which is why the notebooks use
  an Esri basemap.)
- Learners often press **OK** instead of **Apply** while comparing classification modes; encourage
  **Apply** so the dialog stays open.
- Remind learners to rename layers before making a legend.

## Common problems

| Symptom | Likely cause | Fix |
|---|---|---|
| `NameError` | A cell was skipped | **Runtime > Run before** |
| Colab forgot variables | The session disconnected | Reconnect and run all cells from the top |
| `HTTPError` or timeout when reading data | Network hiccup | Rerun the cell |
| A merge fails with "object and int64 columns" | ID types differ | Convert both with `.astype(str).str.zfill(5)` |
| QGIS layer shows nothing | Off screen, or behind the basemap | Right-click > **Zoom to Layer**; drag the layer above the basemap |
