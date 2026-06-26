# MScFE-Admissions-AB-Testing

> **One-liner**: An end-to-end A/B testing project using MongoDB, statistical power analysis, and chi-square testing to evaluate whether email reminders increase admissions quiz completion rates for WorldQuant University's MScFE program.

## Overview

### Problem
A significant portion of MScFE applicants fail to complete the required admissions quiz, creating a bottleneck in the enrollment funnel. The question is whether sending a targeted email reminder meaningfully improves quiz completion rates — and whether any observed difference is statistically significant rather than due to chance.

### Approach
I designed and analyzed a full A/B experiment:
* **Data Infrastructure**: Connected to a MongoDB database to extract and wrangle applicant records, including nationality data aggregated via an aggregation pipeline.
* **Power Analysis**: Used `statsmodels.stats.power.GofChisquarePower` with effect size 0.5, α = 0.05, and power = 0.8 to determine the minimum required group size (≈ 52 per group).
* **Experiment Duration**: Applied the Central Limit Theorem with a normal distribution model to find the minimum number of experiment days (7 days) needed to achieve ≥ 95% probability of collecting sufficient observations.
* **Group Assignment**: Implemented a `MongoRepository` class with random shuffling and 50/50 group splitting to assign applicants to treatment (email) and control (no email) groups.
* **Statistical Testing**: Built a `Table2x2` contingency table and performed a chi-square test of independence to assess the significance of the difference in completion rates.

### Result
The chi-square test yielded a **p-value of ~0.044** (< 0.05), indicating a **statistically significant difference** between the treatment and control groups. The **odds ratio of ~7.3** suggests that applicants who received the email reminder were approximately 7 times more likely to complete the admissions quiz than those who did not.

---

## Tech Stack
`Python` `MongoDB` `pymongo` `pandas` `statsmodels` `scipy` `Plotly Express` `country_converter`

## Key Metrics

| Metric | Value |
| :--- | :--- |
| **Required Group Size** | 52 per group |
| **Experiment Duration** | 7 days |
| **Probability of Sufficient Data (7 days)** | 0.994 |
| **Chi-Square p-value** | ~0.044 |
| **Odds Ratio** | ~7.3 |

## Dataset
- **Source**: WorldQuant University MScFE Applicant Database (MongoDB)
- **Collection**: `mscfe-applicants`
- **Key Fields**: `countryISO2`, `admissionsQuiz`, `createdAt`, `group`, `inExperiment`

## Key Features
* **MongoDB Aggregation Pipeline**: Used `$group`, `$sort`, and `$dateToString` operators to extract and summarize applicant data by nationality and date.
* **Statistical Power Analysis**: Calculated minimum sample size before running the experiment to ensure adequate statistical power.
* **Normal Distribution Modeling**: Estimated experiment duration using CLT-based probability calculation with `scipy.stats.norm.cdf`.
* **MongoRepository Class**: Encapsulated all database interactions — querying, group assignment, and observation retrieval — in a reusable class.
* **Choropleth Visualization**: Built an interactive world map with Plotly Express to visualize the geographic distribution of MScFE applicants.
* **Contingency Bar Chart**: Created a grouped bar chart comparing quiz completion rates across treatment and control groups.
