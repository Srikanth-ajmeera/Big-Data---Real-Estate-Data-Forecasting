# Zillow U.S. Real Estate Analysis & Forecasting  
*Time span: Jan 2000 – Apr 2025 • Source: Zillow Transaction & Assessment Data (ZTRAX)*  

---

## 1  Introduction  
This repository contains an end–to–end analysis of historical Zillow home-price data for U.S. cities, followed by forecasting with traditional statistical models and modern machine-learning approaches. The goal is to understand long-term pricing trends, seasonal effects, city-level differences, and to build models that can reasonably project future prices.

---

## 2  Dataset  
| Field | Description |
|-------|-------------|
| `RegionID`, `RegionName`, `State`, `Metro`, `CountyName` | Geographic identifiers |
| `YYYY-MM-DD` columns | Monthly median sale-price estimates |
| `lat`, `lng` | Latitude & longitude provided by Zillow |

All raw *.csv* files are stored in `data/raw/`. Cleaned, long-format tables live in `data/processed/`.

---

## 3  Exploratory Data Analysis (EDA)  
Notebook: **`notebooks/01_eda.ipynb`**

* **Cleaning & reshaping** – removed null regions, fixed malformed dates, melted wide-to-long.  
* **Most-recent price comparison** – bar chart of Apr 2025 medians across cities.  
* **Historical range** – boxplots showing 25-year price dispersion.  
* **Annual averages** – year-by-year mean price table and line plot for top metros.  
* **Percentage growth** – compound annual growth rate (CAGR) from 2000 → 2025.  
* **Seasonality** – monthly decomposition (STL) highlights repeating summer peaks.  
* **Quick facts** – Highest median (San Francisco, CA) vs. lowest (Decatur, IL) as of Apr 2025, etc.

All figures are saved to `reports/figures/`.

---

## 4  Modeling & Forecasting  
Notebook: **`notebooks/02_modelling.ipynb`**

| Model | Key Settings | Purpose |
|-------|--------------|---------|
| **Linear Regression** | Year & month encoded as features | Baseline long-term trend |
| **ARIMA** | Auto-selected (p,d,q) via AIC | Classic univariate forecasting |
| **LSTM** | 2 layers, 64 units, window = 24 months | Captures non-linear temporal patterns |
| **Random Forest** | 500 trees, lagged features | Robust to noise, handles non-linearity |
| **XGBoost** | 200 estimators, learning_rate = 0.05 | Gradient boosting for tabular time series |

Metrics: MAE & MAPE on 2023–2025 hold-out. XGBoost achieved the lowest MAPE (~3.9 %).

---
## 5  Key Findings
* U.S. median home prices nearly **tripled** from 2000 to 2025.  
* Pronounced **seasonality**: June–August premiums average ≈ 4 % over annual mean.  
* Coastal tech hubs (SF Bay Area, Seattle, NYC) retain the highest absolute prices; Midwest markets remain most affordable.  
* Gradient-boosted trees (XGBoost) outperform deep LSTM on short-horizon forecasts with less training time.

---

## 6  Next Steps
* Incorporate macro-economic indicators (CPI, mortgage rates) as exogenous variables.  
* Experiment with Prophet, Temporal Fusion Transformer, or N-BEATS.  
* Deploy a lightweight forecasting API and interactive dashboard for real-time updates.

---

## 7  Contributors & Equal Work Allocation  

| Contributor | Primary Focus |
|-------------|---------------|
| **srikanth** | Data acquisition & cleaning |
| **ritesh** | Exploratory data analysis & visualization |
| **rewanth** | Model development & evaluation |
| **hitesh** | Documentation, reporting & project coordination |

_All contributors participated in code reviews and final presentation._
