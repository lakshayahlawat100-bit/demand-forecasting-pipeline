# Demand Forecasting & Inventory Optimization Pipeline

> End-to-end ML forecasting pipeline built on SAP operational data — predicting parts demand across 15 truck model variants at 87% accuracy, reducing emergency procurement events by 30%.

---

## Overview

This project implements a production-grade demand forecasting system for automotive parts inventory. Built during client engagement with **Daimler Trucks AG**, the pipeline ingests 3 years of SAP ERP data, trains time-series models, and surfaces predictions through an executive Power BI dashboard.

The system runs fully automated on a weekly schedule — zero manual intervention required after deployment.

---

## Problem Statement

The procurement team was operating on static monthly reports with a 2-week lag. This caused:
- Frequent emergency procurement events (high cost, high urgency)
- Overstock on slow-moving variants
- No visibility into demand by region or supplier

**Goal:** Build a forecasting system that predicts parts demand per truck variant, per region, 4 weeks ahead — with enough accuracy to drive real procurement decisions.

---

## Architecture

```
SAP ERP Data
     │
     ▼
Data Ingestion (Python + SQL Server)
     │
     ▼
Feature Engineering
  - Lag features (7d, 14d, 28d)
  - Rolling averages
  - Seasonal decomposition
  - Variant & region encoding
     │
     ▼
Model Training
  - Prophet (primary time-series model)
  - Scikit-Learn (Random Forest for anomaly correction)
  - StatsModels (ARIMA baseline comparison)
     │
     ▼
Model Evaluation & Selection
  - MAPE, RMSE, MAE
  - Backtesting on 6-month holdout
     │
     ▼
Power BI Dashboard (Executive Output)
  - Forecast vs Actual by region / model / supplier
  - Procurement alert flags
  - Weekly auto-refresh
```

---

## Tech Stack

| Layer | Tools |
|-------|-------|
| Language | Python 3.10 |
| Data Ingestion | SQL Server, SAP ERP connectors |
| Feature Engineering | Pandas, NumPy |
| Modelling | Prophet, Scikit-Learn, StatsModels |
| Orchestration | Python scripts (Windows Task Scheduler) |
| Visualisation | Power BI (DAX, RLS, drill-through) |
| Version Control | Git, CI/CD |

---

## Results

| Metric | Result |
|--------|--------|
| Forecast Accuracy | **87% (MAPE < 13%)** |
| Emergency Procurement Reduction | **30%** |
| Manual Effort Eliminated | **12+ hours per weekly cycle** |
| Time-to-Adoption | **6 weeks post-launch** |
| Truck Variants Covered | **15** |
| Data Volume | **3 years, 20M+ rows** |

---

## Key Files

```
├── ingestion/
│   └── sap_extractor.py          # SAP to SQL Server pipeline
├── features/
│   └── feature_engineering.py    # Lag, rolling, seasonal features
├── models/
│   ├── prophet_model.py          # Primary forecasting model
│   ├── rf_correction.py          # Anomaly correction layer
│   └── evaluation.py             # MAPE, RMSE, backtesting
├── pipeline/
│   └── run_weekly.py             # Full automated pipeline runner
├── dashboard/
│   └── forecast_dashboard.pbix   # Power BI report file
└── README.md
```

---

## How to Run

```bash
# Install dependencies
pip install pandas numpy prophet scikit-learn statsmodels pyodbc

# Run full pipeline
python pipeline/run_weekly.py --env production

# Run model evaluation only
python models/evaluation.py --backtest --months 6
```

---

## Author

**Lakshay Ahlawat** — Senior Data Analyst & Engineer
[github.com/lakshayahlawat100-bit](https://github.com/lakshayahlawat100-bit)
