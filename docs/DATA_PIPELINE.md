# Data Pipeline

## Pipeline Overview

This project implements an automated data processing pipeline using Python and DVC.

The pipeline consists of four stages:

1. Data Collection
2. Data Preprocessing
3. Feature Engineering
4. Data Validation

## Pipeline Stages

| Stage | Purpose | Input | Output |
|---|---|---|---|
| Collect | Collect the Iris dataset and prepare the raw data | Scikit-learn Iris dataset | `data/raw/iris_raw.csv` |
| Preprocess | Remove duplicates, handle missing values, convert numeric columns, and clean the dataset | `data/raw/iris_raw.csv` | `data/processed/iris_preprocessed.csv` |
| Feature Engineering | Create additional useful features from the processed data | `data/processed/iris_preprocessed.csv` | `data/processed/iris_features.csv` |
| Validate | Check schema, values, ranges, and missing data | `data/processed/iris_features.csv` | Validation result |

## 1. Data Collection

The collection stage loads the Iris dataset from scikit-learn.

The target values are converted into species names:

- `0` → setosa
- `1` → versicolor
- `2` → virginica

A `collected_at` timestamp is also added.

**Output:**

`data/raw/iris_raw.csv`

## 2. Data Preprocessing

The preprocessing stage performs the following operations:

- Removes duplicate rows
- Converts measurement columns to numeric values
- Handles missing numeric values using the median
- Removes rows with missing species values
- Removes the `collected_at` column

**Output:**

`data/processed/iris_preprocessed.csv`

## 3. Feature Engineering

The feature engineering stage creates additional features:

- `sepal_area`
- `petal_area`
- `sepal_to_petal_length_ratio`
- `petal_length_bin`

The `petal_length_bin` feature categorizes petal length into:

- Short
- Medium
- Long

**Output:**

`data/processed/iris_features.csv`

## 4. Data Validation

The validation stage checks whether the processed dataset satisfies the required conditions.

### Validation Rules

- Expected columns must be present.
- No null values are allowed.
- Species must be one of:
  - setosa
  - versicolor
  - virginica
- Sepal measurements must be within valid ranges.
- Petal measurements must be within valid ranges.

If validation fails, a `DataValidationError` is raised and the pipeline exits with a non-zero status.

If all checks pass, the validation stage reports:

`Validation PASSED`

## Pipeline Diagram

```text
Scikit-learn Iris Dataset
          |
          v
   +--------------+
   | Data Collect |
   +--------------+
          |
          v
    iris_raw.csv
          |
          v
   +----------------+
   | Preprocessing  |
   +----------------+
          |
          v
 iris_preprocessed.csv
          |
          v
 +---------------------+
 | Feature Engineering |
 +---------------------+
          |
          v
   iris_features.csv
          |
          v
   +----------------+
   | Data Validation|
   +----------------+
          |
          v
    Validation PASSED
    