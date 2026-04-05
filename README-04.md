# Nepal-Earthquake-Damage-Predictor

> **One-liner**: A machine learning classification project predicting building damage severity in Nepal using SQL-integrated pipelines and optimized Decision Tree models.

## Overview

### Problem
The 2015 Gorkha earthquake in Nepal was a catastrophic event. For future disaster resilience, it is vital to identify which structural characteristics make a building "high risk." This project builds a binary classifier to predict **Severe Damage** (Grade > 3) for buildings in the **Kavrepalanchok** district.

### Approach
* **Data Engineering (SQL)**: Synthesized data from three relational tables (`id_map`, `building_structure`, `building_damage`) using SQLite to create a comprehensive feature matrix.
* **Exploratory Data Analysis (EDA)**: 
    * Identified a baseline accuracy of **0.55**, reflecting the majority class distribution.
    * Analyzed structural features like `plinth_area_sq_ft` and `roof_type` to understand physical vulnerabilities.
* **Model Optimization & Tuning**: 
    * Compared **Logistic Regression** and **Decision Tree** classifiers.
    * Performed a grid search for `max_depth` (1-15) to find the optimal model complexity.
* **Overfitting Mitigation**: Used **Validation Curves** to visualize the trade-off between training and validation accuracy.

### Result
The optimized Decision Tree model achieved a **Validation Accuracy of 66.5%**, a significant **11.5% improvement** over the baseline. Analysis of the Validation Curve identified **Max Depth = 10** as the "sweet spot"—beyond this point, the model began to overfit the training data, losing generalization power on unseen test sets.

---

## Tech Stack
`Python` `SQL (SQLite)` `pandas` `scikit-learn` `Seaborn` `Decision Trees`

## Key Metrics

| Metric | Value |
| :--- | :--- |
| **Baseline Accuracy** | 0.55 (55%) |
| **Logistic Regression Acc** | 65.2% |
| **Best Decision Tree Acc** | **66.5%** |
| **Optimal Hyperparameter** | `max_depth = 10` |
| **Model Improvement** | **+11.5%** over baseline |

## Validation Curve Analysis
Through rigorous hyperparameter tuning, I identified the threshold where model complexity leads to overfitting.

* **Underfitting (Depth 1-5)**: Both training and validation scores are low; the model is too simple.
* **Optimal (Depth 10)**: Validation accuracy peaks at 66.5%.
* **Overfitting (Depth 11-15)**: Training accuracy continues to rise, but validation accuracy declines, indicating the model is "memorizing" noise.

---

## Dataset
- **Source**: Nepal Earthquake Open Data Portal (via WorldQuant University)
- **Target Variable**: `severe_damage` (Binary: 1 if Damage Grade > 3, else 0)
- **Features**: Building structure, foundation type, roof type, and land surface condition.

## Key Features
* **End-to-End SQL Pipeline**: Demonstrated ability to extract and join data from relational databases for ML workflows.
* **Hyperparameter Tuning**: Systematic approach to selecting model parameters using cross-validation principles.
* **Bias-Variance Tradeoff**: Visualized and addressed overfitting using validation curves, a critical skill for model reliability.
* **Interpretable Insights**: Ranked structural features by **Gini Importance** to provide actionable data for urban planning.
