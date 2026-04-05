# Housing in Brazil
One-liner: A data-driven exploration of the Brazilian housing market, identifying regional price disparities and the correlation between property size and valuation.

## Overview

**Problem**

Real estate market transparency is often hindered by fragmented data and inconsistent formatting (e.g., coordinates as strings, mixed currencies). Understanding which regions command higher premiums and how space translates to cost is essential for market entry analysis.

**Approach**

I engineered a data pipeline to unify two distinct datasets ($N=22,844$). This involved advanced string manipulation to extract GPS coordinates and administrative states, handling missing values, and normalizing currencies from BRL to USD (using the 2015-2016 exchange rate of 3.19). I then performed a comparative analysis across five major Brazilian regions using Matplotlib and Plotly.

**Result**

The analysis revealed a clear price hierarchy, with the Southeast region being the most expensive (Avg. $208,997). In the Southern region, I identified a moderate positive correlation (up to $r=0.57$) between home size and price, providing a quantifiable baseline for property valuation in states like Rio Grande do Sul.

##Tech Stack
'Python' 'pandas' 'Matplotlib' 'Plotly' 'NumPy'

##Key Metrics
|Metric|Value|
|Total Observations|22,844 properties|
|Most Expensive Region|Southeast ($208,996 avg)|
|Highest Correlation (South)|0.57 (Rio Grande do Sul)|
|Data Features|7 cleaned attributes|

##Dataset
**Source**

WorldQuant University - Applied Data Science Lab (Real Estate Market Data)

**Size**
Multiple CSV files / 10+ Features (Lat, Lon, Area, Price, etc.)

**Scope**
National coverage with state-level granularity

