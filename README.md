# EXPERIMENT 3: PYTHON DATA ANALYSIS (PANDAS)
Name: Reese Cassandra T. Rapis <br> Section: 2ECE-C

This repository contains my **Programming Assignment 3** for **ECE 2112: Advanced Computer Programming and Algorithms**. The activity focuses on using Pandas for three problems: **Positional and Label-Based Slicing**, **Model Lookup**, and **Multi-Model Subsetting**.

## I. OBJECTIVES
- To load a CSV dataset into a Pandas DataFrame.
- To select rows and columns using positional and label-based indexing.
- To filter records using Boolean conditions on a DataFrame column.
- To extract a well-defined subset of data without changing the source data.

## II. POSITIONAL AND LABEL-BASED SLICING
**Goal:** Load `cars.csv` into a DataFrame named `cars`, extract rows 6 through 10 using positional slicing, then display only the columns `Model`, `mpg`, `cyl`, `hp`, and `gear` from that subset.

**How it works:**
```python
cars = pd.read_csv("cars.csv")

cars_6_to_10 = cars.iloc[5:10]

Display_Columns = cars_6_to_10[['Model', 'mpg', 'cyl', 'hp', 'gear']]
```
- `pd.read_csv("cars.csv")` loads the cars CSV file into a DataFrame.
- `cars.iloc[5:10]` uses positional indexing to select rows 6 through 10, since the first data row is row 1 (index 0) and `iloc` slicing excludes the stop index.
- `cars_6_to_10[['Model', 'mpg', 'cyl', 'hp', 'gear']]` uses label-based column selection to keep only the required columns, in the specified order.

**Checking Values:**
```python
Shape of cars: (32, 12)
Column names: ['Model', 'mpg', 'cyl', 'disp', 'hp', 'drat', 'wt', 'qsec', 'vs', 'am', 'gear', 'carb']
```
- The dataset has 32 vehicle records and 12 attributes each. Rows 6–10 correspond to Valiant, Duster 360, Merc 240D, Merc 230, and Merc 280.

## III. MODEL LOOKUP
**Goal:** Use Boolean indexing on the `Model` column to retrieve the full record for Toyota Corolla, and selected columns (`Model`, `mpg`, `hp`, `wt`) for Pontiac Firebird.

**How it works:**
```python
toyota = cars[cars['Model']=='Toyota Corolla']

pontiac = cars[cars['Model']=='Pontiac Firebird'][['Model', 'mpg', 'hp', 'wt']]
```
- `cars['Model']=='Toyota Corolla'` creates a Boolean mask that is `True` only for the row where the model name matches, and `cars[...]` uses that mask to return the full matching record.
- The same approach is applied for Pontiac Firebird, with an added column selection step to keep only `Model`, `mpg`, `hp`, and `wt`.

**Checking Values:**
```python
toyota: Toyota Corolla — shows full record
pontiac: Pontiac Firebird — shows Model, mpg, hp, wt only
```
- Selecting by model value rather than row position ensures the correct record is retrieved even if the dataset's row order changes.

## IV. MULTI-MODEL SUBSETTING
**Goal:** Create a DataFrame named `selected_cars` containing only the records for Datsun 710, Lotus Europa, and Ferrari Dino, keeping only `Model`, `mpg`, `cyl`, `hp`, and `gear`, selected by model value rather than row number.

**How it works:**
```python
selected_cars = cars.loc[(cars['Model']=='Datsun 710')|(cars['Model']=='Lotus Europa')|(cars['Model']=='Ferrari Dino'), ['Model', 'mpg', 'cyl', 'hp', 'gear']]
```
- Three separate `Model` column are combined with the `|` (OR) operator, producing a single Boolean mask that is `True` for any of the three target models.
- `cars.loc[mask, columns]` applies that mask to select the matching rows and, in the same step, keeps only the required columns.

**Checking Values:**
```python
Shape of selected_cars: (3, 5)
```
- The resulting DataFrame contains exactly the three requested models — Datsun 710, Lotus Europa, and Ferrari Dino — with exactly five columns each, satisfying the required check.

Thank you for reading.
