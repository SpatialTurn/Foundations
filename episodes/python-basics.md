---
title: "Python Basics"
teaching: 30
exercises: 120
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I write and run Python code?
- How does Python store numbers, text and collections of values?
- How do I make decisions, repeat work and reuse code?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Run code in a notebook and read error messages
- Use variables, numbers, strings, lists and dictionaries
- Write `if` statements and `for` loops
- Write and call your own functions

::::::::::::::::::::::::::::::::::::::::::::::::

## How this episode works

This page gives a short overview of each idea. The real learning happens in the six notebooks at the end:
each takes 15 to 20 minutes, covers one idea, and ends with an exercise and its solution. Work through them
in order. The examples use Indiana counties, so by the end you will already be thinking about the kind of
data the other modules use.

## Running code and reading errors

A notebook has **text cells** and **code cells**. Run a code cell with **Shift + Enter** and its output
appears below it. `print()` shows a value; `#` starts a comment that Python ignores.

```python
print("Hello, World!")   # text goes in quotes
print(6 * 7)             # numbers do not
```

Errors are normal. Read the **last line** of the message first: it names the problem, such as a
`SyntaxError` (Python could not read the line, often a missing quote or bracket) or a `NameError` (a name
Python does not know, often a typo or a skipped cell).

## Variables and types

`=` stores a value under a name. Every value has a type:

| Type | Examples | Used for |
|---|---|---|
| `int` | `177513` | Whole numbers, such as counts |
| `float` | `499.8` | Decimal numbers, such as areas and rates |
| `str` | `"Tippecanoe"`, `"18157"` | Text, including identifiers like FIPS codes |
| `bool` | `True`, `False` | Yes or no |

```python
population = 177513
land_sq_mi = 499.8
density = population / land_sq_mi      # 355.2 people per square mile
```

Numbers stored as text (`"177513"`) cannot be used in math until you convert them with `int()` or
`float()`. Real data often arrives this way: the Census API, for example, returns every value as text.

## Text (strings)

**f-strings** build text from values, and string **methods** clean it:

```python
name = "  tippecanoe county "
clean = name.strip().title()                      # "Tippecanoe County"
print(f"{clean} had {population:,} people")       # "Tippecanoe County had 177,513 people"
```

## Lists and dictionaries

A **list** holds values in order; positions start at **0**. A **dictionary** holds `key: value` pairs, so
you look values up by name.

```python
counties = ["Marion", "Lake", "Allen"]
print(counties[0], counties[-1])                  # first and last

allen = {"name": "Allen", "fips": "18003", "unemployment": 4.3}
print(allen["unemployment"])
```

A dictionary of lists (one list per column) and a list of dictionaries (one dictionary per row) are both
ways of describing a table. pandas, in the next episode, turns either one into a DataFrame.

## Decisions and loops

`if`, `elif` and `else` choose what runs. A `for` loop repeats a block for every item in a list. The
indented lines belong to the block.

```python
for d in [101.4, 548.3, 21.7]:
    if d >= 300:
        print(d, "urban")
    else:
        print(d, "rural or small town")
```

## Functions

A function packages a piece of work under a name so you can reuse it. `return` sends a result back.

```python
def density(population, area):
    """Return people per unit of area."""
    return population / area

density(177513, 499.8)
```

:::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Predict the output

What does each line print? Decide first, then run them in a notebook to check.

```python
print(7 / 2)
print(7 // 2)
print("7" + "2")
print([10, 20, 30][1])
```

:::::::::::::::: solution

- `3.5`: `/` always gives a decimal number
- `3`: `//` divides and rounds down
- `72`: joining two strings, not adding numbers
- `20`: positions start at 0, so `[1]` is the second item

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::: challenge

## Challenge 2: Fix the bug

This code should print the total population of three counties, but it stops with an error. What is wrong?

```python
populations = ["34365", "360412", "79129"]
total = 0
for p in populations:
    total = total + p
print(total)
```

:::::::::::::::: solution

The populations are stored as **text** (inside quotes), and Python cannot add text to a number, so it
raises a `TypeError`. Convert each value inside the loop with `total = total + int(p)`, or store the
numbers without quotes in the first place.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Run cells with Shift + Enter, in order, and read the last line of any error first
- Values have types (`int`, `float`, `str`, `bool`); convert numbers stored as text before doing math
- Lists keep values in order (from position 0); dictionaries look values up by key
- `if` / `elif` / `else` make decisions; `for` loops repeat work; functions package work for reuse

::::::::::::::::::::::::::::::::::::::::::::::::

## Notebooks

Work through these in order. Each one opens in Google Colab.

| Notebook | What you will do |
|---|---|
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/02a_Notebooks_Cells_and_Printing.ipynb" target="_blank">2a. Notebooks, Cells and Printing</a> | Run cells, print, write comments, read error messages and edit text cells |
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/02b_Variables_Types_and_Math.ipynb" target="_blank">2b. Variables, Types and Math</a> | Store values, check types, calculate a population density and convert text to numbers |
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/02c_Strings.ipynb" target="_blank">2c. Strings: Working with Text</a> | Build text with f-strings, clean messy names and split coordinates |
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/02d_Lists_and_Dictionaries.ipynb" target="_blank">2d. Lists and Dictionaries</a> | Pick items from lists, store county records in dictionaries, and see how both become tables |
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/02e_Conditions_and_Loops.ipynb" target="_blank">2e. Conditions and Loops</a> | Classify counties with `if` and loop over lists to build results |
| <a href="https://colab.research.google.com/github/SpatialTurn/Foundations/blob/main/notebooks/02f_Functions.ipynb" target="_blank">2f. Functions</a> | Write reusable functions with parameters, defaults and return values |
