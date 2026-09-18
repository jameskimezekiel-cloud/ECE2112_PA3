# PA3_ECE2112_JAMES, KE
---
### EXPERIMENT 3: PYTHON DATA ANALYSIS (PANDAS)
Submitted by: James, Kim Ezekiel G. | 2ECE-A | 09/08/2026

---

## Table of Contents

- [Overview](#overview)
- [Functions & Techniques Used](#functions--techniques-used)
- [Walkthrough](#walkthrough)
  - [Part A — Positional and Label-Based Slicing](#part-a--positional-and-label-based-slicing)
  - [Part B — Model Lookup](#part-b--model-lookup)
  - [Part C — Multi-Model Subsetting](#part-c--multi-model-subsetting)
- [Files](#files)
- [Setup](#setup)
- [Running the Notebook](#running-the-notebook)
- [Notes](#notes)

---

## Overview

This notebook covers Experiment 3 of the course: exploring and slicing tabular data with `pandas`. Working from the `cars.csv` dataset, it walks through indexing rows and columns two different ways — by position and by label — then uses conditional lookups to pull out specific car models without ever referencing a row number directly.

---

## Functions & Techniques Used

| Technique | Where it's used | What it does |
| :--- | :--- | :--- |
| `.iloc[]` | Part A | Grabs rows by their integer position in the DataFrame. |
| `.loc[]` | Parts A, B, C | Selects rows and/or columns by label, and doubles as the tool for conditional filtering. |
| Boolean masking (`==`, `\|`) | Parts B, C | Builds a True/False filter from a column comparison so rows can be matched by value instead of position. |

---

## Walkthrough

### Part A — Positional and Label-Based Slicing

Load the dataset, check its dimensions, then slice out a specific block of rows and narrow it down to a handful of columns.

```python
import pandas as pd

cars = pd.read_csv('cars.csv')

# Shape and column names
print("Shape:", cars.shape)
print("List of Column Names:", list(cars))

# Rows 6–10 (1-based), pulled positionally
cars_6_to_10 = cars.iloc[5:10]
cars_6_to_10

# Narrow down to specific columns, in this order
cars_6_to_10.loc[:, ['Model', 'mpg', 'cyl', 'hp', 'gear']]
```

`cars.shape` returns `(32, 12)`, and the dataset's 12 columns are `Model`, `mpg`, `cyl`, `disp`, `hp`, `drat`, `wt`, `qsec`, `vs`, `am`, `gear`, and `carb`.

### Part B — Model Lookup

Rather than hard-coding a row index, filter on the `Model` column directly to pull a specific car's data.

```python
# Full record for Toyota Corolla
toyota = cars.loc[cars['Model'] == 'Toyota Corolla']
toyota

# Selected fields for Pontiac Firebird
pontiac = cars.loc[(cars['Model'] == 'Pontiac Firebird'), ['Model', 'mpg', 'hp', 'wt']]
pontiac
```

### Part C — Multi-Model Subsetting

Extend the same filtering idea to match against several model names at once, combined with an OR condition.

```python
selected_cars = cars.loc[
    (cars['Model'] == 'Datsun 710') | (cars['Model'] == 'Lotus Europa') | (cars['Model'] == 'Ferrari Dino'),
    ['Model', 'mpg', 'cyl', 'hp', 'gear']
]

print("Shape:", selected_cars.shape)
selected_cars
```

`selected_cars` comes out to a `(3, 5)` DataFrame — one row per requested model, five columns wide.

---

## Files

```text
.
├── cars.csv       # dataset used throughout the notebook
├── PA3.ipynb      # the assignment notebook
└── README.md      # this file
```

---

## Setup

- Python 3.8 or later
- `pandas` (`pip install pandas`)
- Jupyter Notebook or JupyterLab

---

## Running the Notebook

1. Keep `cars.csv` in the same folder as `PA3.ipynb`.
2. Start Jupyter:
   ```bash
   jupyter notebook
   ```
3. Open `PA3.ipynb` and run all cells from top to bottom.

---

## Notes

- Every model lookup is done through boolean conditions on the `Model` column — no row indices are hard-coded.
- `cars_6_to_10`, `toyota`, `pontiac`, and `selected_cars` are all separate variables, so the original `cars` DataFrame is never overwritten.
- Column order in the final outputs matches what was asked for in each part, not the order columns happen to appear in the source CSV.
