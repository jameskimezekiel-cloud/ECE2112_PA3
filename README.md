# ADPROG_PA3 — Python Data Analysis (Pandas)

**Experiment 3: Python Data Analysis (Pandas)**
Submitted by: James, Kim Ezekiel G. | 2ECE-A | 09/09/2026

## Overview

This notebook works with the `cars.csv` dataset (the classic `mtcars`-style
dataset) using **pandas** to practice positional slicing, label-based
selection, and Boolean indexing.

## Requirements

- Python 3
- pandas
- `cars.csv` in the same directory as the notebook (the notebook loads it
  with `pd.read_csv('cars.csv')`)

Install pandas if needed:
```bash
pip install pandas
```

## How to Run

1. Place `cars.csv` in the same folder as `ADPROG_PA3.ipynb`.
2. Open the notebook with Jupyter:
   ```bash
   jupyter notebook ADPROG_PA3.ipynb
   ```
3. Run all cells in order (Cell → Run All).

## Contents

### A. Positional and Label-Based Slicing

Load the dataset:
```python
import pandas as pd

cars = pd.read_csv('cars.csv')
cars
```

**a. Shape and column names**
```python
print("Shape of cars:")
print(cars.shape)

print("\nColumn names:")
print(cars.columns.tolist())
```

**b. Rows 6–10 via positional slicing (`.iloc`)**
```python
cars_6_to_10 = cars.iloc[5:10]
cars_6_to_10
```

**c. Keep only `Model`, `mpg`, `cyl`, `hp`, `gear` (label-based)**
```python
cars_6_to_10 = cars_6_to_10[['Model', 'mpg', 'cyl', 'hp', 'gear']]
cars_6_to_10
```

### B. Model Lookup

**a. Full row for Toyota Corolla**
```python
toyota = cars[cars["Model"] == "Toyota Corolla"]
toyota
```

**b. Selected columns for Pontiac Firebird**
```python
pontiac = cars.loc[cars["Model"] == "Pontiac Firebird",
    ["Model", "mpg", "hp", "wt"]]
pontiac
```

### C. Multi-Model Subsetting

**Select Datsun 710, Lotus Europa, and Ferrari Dino by name**
```python
models = ["Datsun 710", "Lotus Europa", "Ferrari Dino"]

selected_cars = cars.loc[cars["Model"].isin(models),
    ["Model", "mpg", "cyl", "hp", "gear"]]

print("Shape of selected_cars:")
print(selected_cars.shape)

selected_cars
```

## Key Variables

| Variable         | Description                                              |
|------------------|-----------------------------------------------------------|
| `cars`           | Full dataset loaded from `cars.csv`                       |
| `cars_6_to_10`   | Rows 6–10, later reduced to 5 selected columns             |
| `toyota`         | Full row for Toyota Corolla                                |
| `pontiac`        | Selected columns for Pontiac Firebird                      |
| `selected_cars`  | 3 selected models with 5 selected columns (3×5 DataFrame)  |
