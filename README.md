# PA3_ECE2112_JAMES, KE
---
### EXPERIMENT 3: PYTHON DATA ANALYSIS (PANDAS)
Submitted by: James, Kim Ezekiel G. | 2ECE-A | 09/08/2026

This notebook works with the `cars.csv` dataset (the classic `mtcars`-style
dataset) using **pandas** to practice positional slicing, label-based
selection, and Boolean indexing.

## Objectives
---
##### At the end of this laboratory activity, the student should be able to:
1. load a CSV dataset into a Pandas DataFrame;
2. select rows and columns using positional and label-based indexing;
3. filter records using conditions on a DataFrame column; and
4. extract a well-defined subset of data without changing the source data.

## A. Positional and Label-Based Slicing
---
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

## B. Model Lookup
---
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

## C. Multi-Model Subsetting
---
**Select Datsun 710, Lotus Europa, and Ferrari Dino by name**
```python
models = ["Datsun 710", "Lotus Europa", "Ferrari Dino"]

selected_cars = cars.loc[cars["Model"].isin(models),
    ["Model", "mpg", "cyl", "hp", "gear"]]

print("Shape of selected_cars:")
print(selected_cars.shape)

selected_cars
```

To view the program for PA3: download [ECE2112_PA3](https://github.com/jameskimezekiel-cloud/ECE2112_PA3/blob/main/ADPROG_PA3.ipynb), open on Jupyter Notebook, and run all cells.

## README file Version History
- September 08, 2026 - Uploaded the .ipynb file
- September 08, 2026 - Uploaded the README file
