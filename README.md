# Geo-Aware MRO Decision Intelligence System

**A Production-Grade Strategic Digital Twin for Maintenance, Repair & Overhaul (MRO) Operations**

![MITx MicroMasters](https://img.shields.io/badge/Aligned-MITx%20MicroMasters%20in%20SCM-green)

---

## Overview

The **Geo-Aware MRO Decision Intelligence System** is a purpose-built strategic digital twin designed for complex Maintenance, Repair & Overhaul (MRO) environments — where traditional ERP and MRP systems consistently fall short.

It addresses critical challenges including:
- Extreme lead-time volatility due to multi-origin geopolitical exposure (US, Russia, France, Germany, Sweden, Israel, Domestic)
- Highly intermittent and lumpy demand patterns
- Multi-echelon spare parts networks spanning Forward, Border, and Rear depots
- High mission criticality combined with obsolescence and financial risk

**Version 1.1 (Core Foundation)** delivers a complete, production-quality system including multi-criteria classification, intermittent demand forecasting, Bayesian geo-risk scoring, Newsvendor-based replenishment logic, and game-theoretic supplier qualification.

---

## What Makes This Different

| Capability              | Standard ERP / MRP                  | This System                                      |
|-------------------------|-------------------------------------|--------------------------------------------------|
| Demand Forecasting      | ARIMA / Moving Average              | Croston's Method + SBA (intermittent demand)     |
| Supplier Risk           | Qualitative scorecard               | Bayesian posterior updated from UN Comtrade      |
| SKU Classification      | ABC only                            | **ABC × VED × FNS × Location** (27-class taxonomy) |
| Supplier Strategy       | Lowest-bid selection                | Nash Equilibrium game-theoretic analysis         |
| Reorder Policy          | Fixed safety stock                  | Criticality-weighted Newsvendor with geo-risk adjustment |
| Reproducibility         | Ad-hoc scripts                      | MLflow + DVC + Docker + GitHub Actions CI/CD     |

---

## Architecture

```bash
geo-aware-mro-decision-system/
├── data/
│   ├── raw/           # M5, UN Comtrade, NASA CMAPSS
│   ├── processed/     # DVC-tracked artifacts
│   └── external/      # Synthetic SKU Master
├── notebooks/
│   ├── 01_sku_intelligence.ipynb      # 27-class taxonomy + Cᵢ Index
│   ├── 02_demand_forecasting.ipynb    # Croston's, SBA, Holt-Winters, ARIMA
│   ├── 03_risk_scoring.ipynb          # Bayesian geo-risk + Newsvendor
│   └── 04_supplier_qualification.ipynb# Decision Trees + Nash Equilibrium
├── src/
│   ├── classifiers/          # ABC, VED, FNS, Location, Multi-criteria
│   ├── forecasting/          # Croston's, SBA, Holt-Winters, ARIMA, Demand Router
│   ├── risk/                 # Bayesian risk, Newsvendor
│   ├── game_theory/          # Nash games (2x2 & 3-player), Strategic Risk Scorer
│   └── utils/
├── tests/                    # Unit tests for core modules
├── app.py                    # Plotly Dash interactive dashboard
├── mlflow/                   # Experiment tracking
├── docs/                     # Documentation


## Data Architecture

The system follows a **hybrid, traceable, and reproducible** data pipeline that combines real-world public datasets with domain-specific synthetic MRO data.

### Data Sources

| Source                  | Purpose                                      | Type                  |
|-------------------------|----------------------------------------------|-----------------------|
| **M5 Forecasting Dataset** | Realistic intermittent & lumpy demand patterns | Time-series (Retail) |
| **UN Comtrade**         | Geopolitical sourcing exposure & trade flows | International trade  |
| **NASA CMAPSS**         | Equipment degradation and failure modeling   | Predictive maintenance |
| **Synthetic SKU Master**| MRO-specific attributes (VED, Location Criticality, Vintage, Obsolescence, etc.) | Custom-generated     |

### High-Level Data Flow

```mermaid
flowchart TD
    A[Raw Data Sources] --> B[UN Comtrade API]
    A --> C[M5 Walmart Dataset]
    A --> D[NASA CMAPSS]
    A --> E[Synthetic SKU Generator]

    B & C & D & E --> F[DuckDB Data Warehouse]

    F --> G[Data Processing & Feature Engineering]
    
    G --> H[SKU Intelligence Layer]
    H --> I1[ABC × VED × FNS × Location Classification<br>(27-class taxonomy)]
    H --> I2[Composite Criticality Index Cᵢ]

    G --> J[Demand Forecasting Engine]
    J --> J1[Croston's Method]
    J --> J2[SBA - Syntetos-Boylan Approximation]
    J --> J3[Holt-Winters]
    J --> J4[ARIMA]

    G --> K[Bayesian Geo-Risk Layer]
    K --> K1[Prior → Posterior Risk Update]

    G --> L[Newsvendor & Replenishment Logic]

    G --> M[Game Theory Module]
    M --> M1[Nash Equilibrium Supplier Games]

    I1 & I2 & J & K & L & M --> N[Enriched SKU Master]

    N --> O[Plotly Dash Dashboard]
    N --> P[MLflow Experiment Tracking]
    N --> Q[DVC Versioned Pipeline]
├── dvc.yaml
├── MLproject
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── .github/workflows/ci.yml
