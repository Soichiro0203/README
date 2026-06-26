# Deloitte Data Analytics Job Simulation | Forage

> **One-liner**: A practical data analytics simulation focusing on industrial telemetry analysis (Tableau) and corporate social responsibility (Excel/Gender Pay Equality).

## Project Overview
This project was part of the **Deloitte Data Analytics Virtual Experience**. I acted as a data analyst consultant for "Daikibo Industrials" to solve two critical business challenges: optimizing manufacturing uptime and investigating internal gender pay equity.

## Task 1: Telemetry Data Analysis (Manufacturing Efficiency)
### Problem
Daikibo Industrials collected a month's worth of telemetry data from 4 global factories (Tokyo, Osaka, Berlin, Shenzhen). The client needed to identify which location and which specific machine types were responsible for the most downtime.

### Approach & Skills
* **Tool**: `Tableau`
* **Data Ingestion**: Processed a large-scale JSON dataset containing status messages sent every 10 minutes from 9 types of machines.
* **Calculated Metrics**: Created a custom measure `Unhealthy` to quantify downtime (10 mins per unhealthy status).
* **Interactive Dashboarding**:
    * Built a "Down Time per Factory" bar chart.
    * Built a "Down Time per Device Type" bar chart.
    * Implemented **Dashboard Filtering**: Selecting a factory automatically filters the device-specific downtime, enabling root-cause analysis.

### Insight
Identified the factory with the highest downtime and pinpointed the specific failing machine types to prioritize maintenance scheduling.

---

## Task 2: Gender Pay Equality Analysis (Forensic Analytics)
### Problem
Following internal complaints regarding gender inequality, Daikibo requested an investigation into salary distributions across all global roles.

### Approach & Skills
* **Tool**: `Excel` / `Data Logic`
* **Classification Algorithm**: Implemented a 3-tier classification system for the "Equality Score" (-100 to +100):
    * **Fair**: Score within ±10 (The Ideal range).
    * **Unfair**: Scores between ±10 and ±20.
    * **Highly Discriminative**: Scores exceeding ±20.
* **Forensic Mindset**: Categorized complex compensation data to highlight systemic issues within specific factory-role combinations.

---

## Professional Skills Gained
* **Data Visualization**: Mastery of Tableau for creating executive-level interactive dashboards.
* **Analytical Thinking**: Transforming raw telemetry pings into actionable business metrics (Downtime).
* **Corporate Social Responsibility (CSR)**: Understanding how data analytics can be applied to Forensic HR investigations and social equity.
* **Data Unification**: Handling and unzipping hierarchical JSON structures for BI tools.

## Tech Stack
`Tableau` `Excel` `JSON Data Handling` `Business Intelligence (BI)`
