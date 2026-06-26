# Volatility-Forecasting-South-Africa

> **One-liner**: A full-stack financial forecasting project using GARCH(1,1) modeling and FastAPI to predict stock return volatility for MTN Group, South Africa's largest telecommunications company.

## Overview

### Problem
Stock volatility forecasting is fundamental to risk management and options pricing. MTN Group (MTNOY), listed on the OTC market, exhibits classic volatility clustering — periods of calm followed by turbulence — making it an ideal candidate for GARCH modeling. The challenge is to build not just an accurate model, but a deployable API that serves real-time predictions.

### Approach
I built an end-to-end volatility forecasting system:
* **Data Pipeline**: Fetched historical daily OHLCV data from the AlphaVantage API and stored it in a SQLite database via a custom `SQLRepository` class, enabling reproducible retrieval.
* **Feature Engineering**: Computed percentage returns from closing prices and selected the 2,500 most recent observations for training.
* **Model Diagnostics**: Used ACF and PACF plots on squared returns to confirm the presence of volatility clustering (ARCH effects) and validate the GARCH model choice.
* **Model Training**: Fitted a `GARCH(1,1)` model using the `arch` library, with AIC and BIC recorded for model selection.
* **Walk-Forward Validation**: Split data into 80% training / 20% testing to evaluate out-of-sample forecasting performance.
* **API Deployment**: Deployed the trained model as a RESTful API using **FastAPI** with `/fit` and `/predict` endpoints, enabling on-demand 5-day volatility forecasts.

### Result
The **GARCH(1,1)** model successfully captured volatility clustering in MTNOY returns. The standardized residuals showed no remaining autocorrelation in squared values (confirmed via ACF), indicating a well-specified model. The deployed API returns a **5-day forward volatility forecast** in real time via a POST request, demonstrating a complete machine learning deployment pipeline.

---

## Tech Stack
`Python` `FastAPI` `arch` `pandas` `SQLite` `AlphaVantage API` `statsmodels` `Matplotlib` `joblib` `pydantic`

## Key Metrics

| Metric | Value |
| :--- | :--- |
| **Ticker** | MTNOY (MTN Group) |
| **Training Observations** | 2,500 daily returns |
| **Model** | GARCH(1,1) |
| **Train/Test Split** | 80% / 20% |
| **Forecast Horizon** | 5 business days |
| **API Framework** | FastAPI (uvicorn) |

## Dataset
- **Source**: AlphaVantage API (`TIME_SERIES_DAILY`, full output)
- **Storage**: SQLite database via `SQLRepository` class
- **Frequency**: Daily (business days)
- **Features**: Open, High, Low, Close, Volume → returns derived from Close

## Key Features
* **Custom Data Layer**: `AlphaVantageAPI` and `SQLRepository` classes cleanly separate data acquisition from modeling, following software engineering best practices.
* **ARCH Effects Validation**: ACF/PACF plots of squared returns confirmed heteroskedasticity prior to fitting the GARCH model.
* **GarchModel Class**: Encapsulated the full ML lifecycle — `wrangle_data`, `fit`, `predict_volatility`, `dump`, and `load` — in a single reusable class with model persistence via `joblib`.
* **AIC/BIC Tracking**: Automatically recorded information criteria on each training run for systematic model comparison.
* **RESTful API**: FastAPI endpoints `/fit` and `/predict` accept JSON requests and return structured responses, enabling integration with downstream applications.
* **Pydantic Validation**: `FitIn`, `FitOut`, `PredictIn`, and `PredictOut` schemas enforce strict input/output contracts for the API.
