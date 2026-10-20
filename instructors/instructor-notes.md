---
title: 'Instructor Notes'
---

## Overall approach

- This module is for complete beginners. Each Python notebook takes 15 to 25 minutes and covers one idea,
  with an exercise and its solution at the end. In a live session, teach the episode page briefly, then let
  learners work through the notebooks while helpers circulate.
- Suggested timing for a full day: Introduction 30 min; Python Basics (notebooks 2a to 2f) 2.5 hours;
  Working with Data (3a, 3b) 1 hour; Geospatial Python Basics (4a to 4d) 2 hours; Map Your County in
  Python 1 hour. The QGIS episodes (Getting Started 1.75 hours, Tables 1.25 hours, Map Your County 1 hour)
  work well as a separate day.
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
- 4d: the commonest mistake is reading without `masked=True` and reporting -9999 as the lowest elevation.
  Elevation 152.9 to 258.1 m; cultivated crops cover 65% of the county.

### Map Your County (Python and QGIS)

- Both capstones use the same files and should produce the same map; pair a Python learner with a QGIS
  learner and compare at the end.
- Expected: 43 tracts, 0 unmatched; tract 104 (residence halls) has 0 households and a poverty universe of 0,
  so its rates are missing; median income is -666666666 for tracts 104 and 105; 17 tracts have 10% or more
  households without a vehicle. Natural breaks differ slightly between tools: about 4, 9, 15 and 26% in
  Python (mapclassify) and 2.4, 8.6, 15.3 and 25.5% in QGIS. Both are fine; it is a nice point about methods.
- QGIS does not draw features whose Graduated value is NULL. The hint shows a rule-based "no data" class.
- Discuss the poverty map near campus: student populations raise poverty rates. It is a good moment to talk
  about what a Census measure does and does not mean.

### Getting Started with QGIS

- Moved here from the Data Visualization module in October 2026 and rebuilt in Step 8 on Indiana colleges
  (the Alaska airports remain in Workshop Session 1A). Data is loaded from this repository's `data/` folder by
  URL. Each part ends with a **Check** line; ask learners to confirm it before moving on.
- **QGIS 4:** in Add Vector Layer > Protocol, the **Type** list starts with cloud services (Alibaba Cloud OSS is
  preselected). Learners must pick **HTTP/HTTPS/FTP**, or the layer fails to load. QGIS 3 preselects HTTP.
- The OpenStreetMap basemap needs an internet connection; on a slow network, skip it.
- Loading from a web address (Layer > Add Layer > Add Vector Layer > Protocol: HTTP(S)) avoids file
  downloads and path problems. If a network blocks it, the same GeoJSON files can be downloaded from the
  repository's `data/` folder and loaded as files.
- In QGIS, the OpenStreetMap basemap works normally. (In Colab it does not, which is why the notebooks use
  an Esri basemap.)
- Learners often press **OK** instead of **Apply** while comparing classification modes; encourage
  **Apply** so the dialog stays open.
- Remind learners to rename layers before making a legend.

### Tables, Joins and Selections in QGIS

- The ACS CSV loads with correct types because of `tippecanoe_acs_2024.csvt`. Without it, loading from the web
  gives text fields, and Delimited Text guesses `GEOID` as a number.
- Layers read from the web are read-only, so the Field Calculator only offers **virtual fields** (ticked and
  grayed out, with types Decimal (double) and Integer (32 bit)). That is expected.
- Division by zero returns NULL in QGIS expressions (tract 104). Stress that NULL is not 0%.

## Common problems

| Symptom | Likely cause | Fix |
|---|---|---|
| `NameError` | A cell was skipped | **Runtime > Run before** |
| Colab forgot variables | The session disconnected | Reconnect and run all cells from the top |
| `HTTPError` or timeout when reading data | Network hiccup | Rerun the cell |
| A merge fails with "object and int64 columns" | ID types differ | Convert both with `.astype(str).str.zfill(5)` |
| QGIS layer shows nothing | Off screen, or behind the basemap | Right-click > **Zoom to Layer**; drag the layer above the basemap |
