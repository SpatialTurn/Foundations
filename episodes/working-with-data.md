---
title: "Working with Data"
teaching: 25
exercises: 45
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I load a table of data into Python?
- How do I select, filter, sort and summarize rows and columns?
- How do I turn a table into a clear chart?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Read a CSV file from the web into a pandas DataFrame
- Inspect a DataFrame's size, columns and data types
- Select columns, filter rows, sort, add calculated columns and summarize groups
- Make bar charts, histograms and scatter plots with matplotlib, with clear labels

::::::::::::::::::::::::::::::::::::::::::::::::

## Libraries

Python's strength for data work comes from **libraries**: packages of ready-made code that you load with
`import`. Two of them do most of the work in this curriculum:

| Library | Usual nickname | What it does |
|---|---|---|
| pandas | `pd` | Tables (DataFrames): reading, cleaning, filtering, summarizing, joining |
| matplotlib | `plt` | Charts of every kind |

```python
import pandas as pd
import matplotlib.pyplot as plt
```

The nicknames are a convention: you will see them in almost every tutorial and answer online.

## DataFrames

A **DataFrame** is a table with labeled columns. Each column has one data type, and each row is one record,
such as one county. `pd.read_csv()` reads a file straight from its web address.

```python
url = "https://raw.githubusercontent.com/SpatialTurn/Foundations/main/data/indiana_county_stats.csv"
counties = pd.read_csv(url)
counties.head()          # first five rows
counties.dtypes          # the type pandas guessed for each column
```

pandas **guesses** each column's type from its values. Identifiers such as FIPS codes often come out as
numbers. That looks harmless, but it drops leading zeros and breaks joins later, so convert them to text.

## The core operations

| Task | Code |
|---|---|
| One column | `counties["pop_2012"]` |
| Several columns | `counties[["name", "pop_2012"]]` |
| Filter rows | `counties[counties["unemp_2016"] >= 5.5]` |
| Two conditions | `counties[(counties["pop_2012"] < 30000) & (counties["unemp_2016"] >= 5)]` |
| Sort | `counties.sort_values("pop_2012", ascending=False)` |
| New column | `counties["density"] = counties["pop_2012"] / counties["land_sq_mi"]` |
| Summary statistics | `counties.describe()` |
| Summarize by group | `counties.groupby("density_class")["unemp_2016"].mean()` |

Calculations on a column apply to every row at once, so you rarely need a loop.

## Charts

matplotlib has one function per chart type. Choose the chart from the question:

| Question | Chart | Function |
|---|---|---|
| How do a few categories compare? | Bar chart | `plt.bar()`, `plt.barh()` |
| How are the values of one variable spread out? | Histogram | `plt.hist()` |
| Are two variables related? | Scatter plot | `plt.scatter()` |
| How does something change over time? | Line chart | `plt.plot()` |

```python
plt.hist(counties["unemp_2016"], bins=12)
plt.title("Unemployment across Indiana's 92 counties, 2016")
plt.xlabel("Unemployment rate (%)")
plt.ylabel("Number of counties")
plt.show()
```

Every chart needs a title and axis labels with units. For very skewed values, such as population density,
a logarithmic axis (`plt.xscale("log")`) makes the pattern visible. The Data Visualization module goes much
further into chart and map design.

:::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Read the code

What does this code produce?

```python
counties[counties["unemp_2016"] > 6].sort_values("pop_2012")[["name", "pop_2012"]]
```

:::::::::::::::: solution

A small table with the name and 2012 population of the counties whose 2016 unemployment rate was above 6%,
sorted from the smallest population to the largest. Reading from the inside out: filter the rows, sort
them, then keep two columns.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::: challenge

## Challenge 2: Pick a chart

Which chart would you use for each question?

1. Are counties with more people per square mile also counties with higher unemployment?
2. Which five counties have the most people?
3. Are most counties' unemployment rates close to the average, or spread out?

:::::::::::::::: solution

1. A **scatter plot** of density against unemployment (with a log scale for density)
2. A **bar chart**, sorted from largest to smallest
3. A **histogram** of unemployment rates

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- pandas reads tables from the web into DataFrames with `pd.read_csv(url)`
- Check data types first; keep identifiers such as FIPS codes as text
- Select, filter, sort, calculate and group with a few lines of code, no loops needed
- Pick the chart that answers the question, and always label it

::::::::::::::::::::::::::::::::::::::::::::::::

## Notebooks

| Notebook | What you will do |
|---|---|
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/03a_Working_with_Tables_in_pandas.ipynb" target="_blank">3a. Working with Tables in pandas</a> | Read Indiana county data, filter, sort, add a density column and summarize by class |
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/03b_Plotting_with_matplotlib.ipynb" target="_blank">3b. Plotting with matplotlib</a> | Make bar charts, histograms and scatter plots, combine panels and save a figure |
