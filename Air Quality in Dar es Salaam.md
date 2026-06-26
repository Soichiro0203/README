# Dar-es-Salaam-Air-Quality-Forecasting

> **One-liner**: A time-series forecasting project using MongoDB and Autoregressive (AR) models to predict PM2.5 air pollution levels in Dar es Salaam, Tanzania.

## Overview

### Problem
Particulate matter (PM2.5) pollution is a critical health concern in urban Africa. To provide reliable early warnings, it is essential to transform raw, noisy sensor data into accurate hourly forecasts. This project addresses the challenge of handling large-scale NoSQL data and building a model that accounts for temporal dependencies.

### Approach
I built an end-to-end forecasting pipeline:
* **Data Infrastructure**: Integrated with a **MongoDB** database to extract real-time sensor data from the "air-quality" collection.
* **Wrangling**: Developed a robust preprocessing function to handle timezone localization (`Africa/Dar_es_Salaam`), outlier removal (PM2.5 > 100), and hourly resampling with forward-fill imputation.
* **Hyperparameter Tuning**: Performed a grid search for the optimal lag ($p$) from 1 to 30 hours, evaluating performance using Mean Absolute Error (MAE).
* **Validation**: Implemented **Walk-Forward Validation**, the gold standard for time-series model evaluation, to ensure real-world predictive power.

### Result
The optimized **Autoregressive (AR)** model achieved a **Training MAE of 1.03**, representing a **74.5% improvement** over the baseline MAE of 4.05. Residual analysis confirmed that the model effectively captured the underlying temporal structure, with a lag of **5 hours** identified as the most significant predictor for current air quality.

---

## Tech Stack
`Python` `MongoDB` `pandas` `statsmodels` `Matplotlib` `Plotly Express` `NoSQL`

## Key Metrics

| Metric | Value |
| :--- | :--- |
| **Baseline MAE** | 4.05 |
| **Training MAE (Best)** | **1.03** |
| **Model Improvement** | **74.5% Reduction in Error** |
| **Best Lag (p)** | 5 Hours |
| **Mean PM2.5 Level** | 8.57 µg/m³ |

## Dataset
- **Source**: Dar es Salaam Sensor Network (via WQU Applied Data Science Lab)
- **Database**: MongoDB (NoSQL)
- **Sampling**: Hourly Mean (Resampled)

## Key Features
* **NoSQL Querying**: Demonstrated proficiency in connecting to and wrangling data from MongoDB.
* **Time-Series Diagnostics**: Utilized ACF and PACF plots to determine the appropriate model structure.
* **Optimal Lag Identification**: Discovered that a 5-hour historical window provides the best balance between model complexity and accuracy.
* **Walk-Forward Validation**: Executed a rigorous testing strategy that simulates real-time deployment of the forecasting model.
* **Interactive Visualization**: Developed dynamic plots to visualize the 7-day rolling average and final model predictions against actual test data.
