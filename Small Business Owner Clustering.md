# Small-Business-Owner-Clustering

> **One-liner**: An unsupervised learning project using KMeans clustering and PCA to segment small business owners in the United States by financial characteristics from the 2019 Survey of Consumer Finances.

## Overview

### Problem
Understanding the financial profiles of small business owners is critical for targeted policy-making and financial services. With hundreds of variables in the Survey of Consumer Finances (SCF 2019), identifying meaningful segments requires a systematic dimensionality reduction and clustering approach.

### Approach
I built an end-to-end clustering pipeline:
* **Data Wrangling**: Filtered the SCF 2019 dataset to isolate small business owners (`HBUS == 1`) with income under $500,000, resulting in a focused analytical subset.
* **Feature Selection**: Computed trimmed variance across all features and selected the top 10 highest-variance features to reduce noise and focus on financially discriminating variables.
* **Hyperparameter Tuning**: Performed a grid search over cluster counts ($k$ = 2–12), evaluating performance using both inertia (elbow method) and silhouette score.
* **Dimensionality Reduction**: Applied PCA (2 components) to visualize the high-dimensional cluster structure in an interpretable 2D scatter plot.

### Result
The optimal **KMeans** model with **3 clusters** was selected based on the elbow curve and silhouette analysis. The resulting segments revealed distinct financial profiles — separating high-asset, high-income owners from lower-wealth self-employed individuals — providing actionable insight into the diversity of small business ownership in the US.

---

## Tech Stack
`Python` `pandas` `scikit-learn` `Plotly Express` `Matplotlib` `KMeans` `PCA` `StandardScaler`

## Key Metrics

| Metric | Value |
| :--- | :--- |
| **Dataset** | SCF 2019 (SCFP2019.csv.gz) |
| **Observations (filtered)** | Small business owners, income < $500K |
| **Features Used** | Top 10 by trimmed variance |
| **Optimal Clusters (k)** | 3 |
| **Evaluation Methods** | Inertia (Elbow) + Silhouette Score |

## Dataset
- **Source**: Federal Reserve Survey of Consumer Finances 2019
- **Filter**: `HBUS == 1` (business owners) & `INCOME < 500,000`
- **Features**: Financial variables including assets, income, net worth, debt

## Key Features
* **Trimmed Variance Selection**: Used `scipy.stats.mstats.trimmed_var` to robustly identify the most discriminating features while mitigating outlier influence.
* **Elbow & Silhouette Analysis**: Dual evaluation strategy to balance model fit and cluster cohesion across a range of $k$ values.
* **Cluster Profiling**: Computed per-cluster feature means to characterize and label each financial segment.
* **PCA Visualization**: Reduced 10-dimensional cluster assignments to 2D for intuitive visual inspection of separation quality.
* **Interactive Dashboard**: Built a Dash application with real-time controls for toggling trimmed/untrimmed variance and adjusting cluster count via a slider.
