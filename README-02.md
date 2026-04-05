# Buenos-Aires-Housing-Predictor

> **One-liner**: A predictive modeling pipeline using Ridge Regression to estimate apartment prices in Buenos Aires, focusing on feature engineering and outlier mitigation.

## Overview

### Problem
Real estate markets in major metropolitan areas like Buenos Aires often contain skewed price distributions and significant "noise" such as outliers, missing data, and multicollinearity. Building an accurate valuation model requires a highly refined data preprocessing strategy to prevent data leakage and handle categorical features effectively.

### Approach
I developed a comprehensive `wrangle` function to clean and unify multiple CSV datasets using `glob` and `pd.concat`. The pipeline involved:
* **Outlier Removal**: Trimming the top and bottom 10% of properties by surface area to ensure model stability.
* **Feature Engineering**: Extracting "boroughs" from location strings and handling high-cardinality categorical data.
* **Data Integrity**: Dropping columns with >50% null values and preventing **Data Leakage** and **Multicollinearity**.
* **Model Pipeline**: Implementing a **Ridge Regression** model within a Scikit-Learn pipeline to handle regularization and categorical encoding.

### Result
The model successfully established a baseline Mean Absolute Error (MAE) and improved predictive performance through systematic feature selection. By analyzing the **10 most influential coefficients**, I quantified the precise impact of features like borough location and surface area ($m^2$) on property value in USD.

---

## Tech Stack
`Python` `pandas` `scikit-learn` `glob` `Matplotlib` `Ridge Regression`

## Key Metrics

| Metric | Value |
| :--- | :--- |
| **Baseline MAE** | $17,239.94 |
| **Mean Apt Price**| $54,246.53 |
| **Model Type** | Ridge Regression |
| **Data Cleaning** | 10% Trimmed Mean (Surface Area) |
| **Top Positive Factor** | Benito Juárez (+$13,778) |
| **Top Negative Factor** | Tláhuac (-$14,166) |

## Dataset
- **Source**: WorldQuant University - Applied Data Science Lab
- **Files**: Multiple CSV files combined (e.g., `mexico-city-real-estate-1.csv` etc.)
- **Target Variable**: `price_aprox_usd` (Apartment Price)

## Key Features
* **Automated Data Wrangling**: A modular function that handles everything from coordinate extraction to categorical pruning.
* **Leakage Prevention**: Strict removal of columns that would artificially inflate model performance during training.
* **Statistical Visualization**: Histograms for price distribution analysis and scatter plots for price-vs-area relationships.
* **Interpretability**: Horizontal bar charts visualizing the top 10 coefficients, providing clear insights into market drivers.
