# PA3_ECE2112_JAMES, KE
---
### EXPERIMENT 3: PYTHON DATA ANALYSIS (PANDAS)
Submitted by: James, Kim Ezekiel G. | 2ECE-A | 09/08/2026

##### The content of this repository contains the **Programming Assignment 3** for ECE2112 Advanced Computer Programming course A.Y. 2026 - 2027 which covers python problems from **Module 3 - PANDAS**.
---

## Table of Contents

- [Overview](#overview)
- [Functions & Techniques Used](#functions--techniques-used)
- [Walkthrough](#walkthrough)
  - [Part A — Positional and Label-Based Slicing](#part-a--positional-and-label-based-slicing)
  - [Part B — Model Lookup](#part-b--model-lookup)
  - [Part C — Multi-Model Subsetting](#part-c--multi-model-subsetting)
- [Files](#files)
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

# (A) Shape and column names
print("Shape:", cars.shape)
print("List of Column Names:", list(cars))

# (B)Rows 6–10 (1-based), pulled positionally
cars_6_to_10 = cars.iloc[5:10]
cars_6_to_10

# (C)Narrow down to specific columns, in this order
cars_6_to_10.loc[:, ['Model', 'mpg', 'cyl', 'hp', 'gear']]
```

(b)
|  | Model | mpg | cyl | disp | hp | drat | wt | qsec | vs | am | gear | carb |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 5 | Valiant | 18.1 | 6 | 225.0 | 105 | 2.76 | 3.46 | 20.22 | 1 | 0 | 3 | 1 |
| 6 | Duster 360 | 14.3 | 8 | 360.0 | 245 | 3.21 | 3.57 | 15.84 | 0 | 0 | 3 | 4 |
| 7 | Merc 240D | 24.4 | 4 | 146.7 | 62 | 3.69 | 3.19 | 20.00 | 1 | 0 | 4 | 2 |
| 8 | Merc 230 | 22.8 | 4 | 140.8 | 95 | 3.92 | 3.15 | 22.90 | 1 | 0 | 4 | 2 |
| 9 | Merc 280 | 19.2 | 6 | 167.6 | 123 | 3.92 | 3.44 | 18.30 | 1 | 0 | 4 | 4 |

(c)
|  | Model | mpg | cyl | hp | gear |
|---|---|---|---|---|---|
| 5 | Valiant | 18.1 | 6 | 105 | 3 |
| 6 | Duster 360 | 14.3 | 8 | 245 | 3 |
| 7 | Merc 240D | 24.4 | 4 | 62 | 4 |
| 8 | Merc 230 | 22.8 | 4 | 95 | 4 |
| 9 | Merc 280 | 19.2 | 6 | 123 | 4 |

### Part B — Model Lookup

Rather than hard-coding a row index, filter on the `Model` column directly to pull a specific car's data.

```python
# (A)Full record for Toyota Corolla
toyota = cars.loc[cars['Model'] == 'Toyota Corolla']
toyota

# (B)Selected fields for Pontiac Firebird
pontiac = cars.loc[(cars['Model'] == 'Pontiac Firebird'), ['Model', 'mpg', 'hp', 'wt']]
pontiac
```
### OUTCOMES:
(a)
| # | Model | mpg | cyl | disp | hp | drat | wt | qsec | vs | am | gear | carb |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 19 | Toyota Corolla | 33.9 | 4 | 71.1 | 65 | 4.22 | 1.835 | 19.9 | 1 | 1 | 4 | 1 |

(b)
| # | Model | mpg | hp | wt |
|---|---|---|---|---|
| 24 | Pontiac Firebird | 19.2 | 175 | 3.845 |

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
### OUTCOMES:
```
Shape: (3, 5)
```
| # | Model | mpg | cyl | hp | gear |
|---|---|---|---|---|---|
| 2 | Datsun 710 | 22.8 | 4 | 93 | 4 |
| 27 | Lotus Europa | 30.4 | 4 | 113 | 5 |
| 29 | Ferrari Dino | 19.7 | 6 | 175 | 5 |

---

## Files

```text
.
├── cars.csv       # dataset used throughout the notebook
├── PA3.ipynb      # the assignment notebook
└── README.md      # this file
```

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
