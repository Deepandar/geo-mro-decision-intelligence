# Geo-Aware MRO Decision Intelligence System

**Multi-criteria spares classification · Geopolitical risk integration · Hybrid Push/Pull stocking · Multi-echelon network optimization**

*v1.1 in progress*

---

## What this is

Standard reorder-point logic breaks down fast when supply chains have real geopolitical exposure — when parts originate from multiple countries with varying supply reliability, and when a stockout at a forward operating location has fundamentally different consequences than one at a rear base.

What makes MRO demand structurally different from retail forecasting is that it is not driven by consumer behavior — it is driven by asset health. Parts are not consumed on a schedule; they are consumed when equipment degrades. That distinction fundamentally shapes how this system is designed.

This project builds a structured decision support system for large-scale MRO operations involving multi-origin equipment fleets. It integrates demand behavior, functional criticality, operational context, geopolitical risk, and network constraints into a unified framework — moving from reactive inventory management to a **structured, risk-aware, and defensible decision-making approach**.

Built on 19+ years of hands-on MRO operations experience. The domain knowledge came first. The system is being built to match it.

---

## Current state (v1.1 — Foundation)

The current focus is on building the classification and data layer — the foundation for all downstream modeling.

### What's implemented:
- Multi-criteria SKU classification:
  - FNS (velocity)
  - ABC (cost weight / Pareto)
  - VED (functional criticality)
  - Location Criticality (border / high-altitude / forward / rear)
- Synthetic MRO dataset with domain-informed attributes
- Basic geo-risk and lead time modeling
- Baseline cost hypothesis:
  - holding cost
  - stockout cost
  - downtime impact

### In progress (v1.1 enhancement):
- Mapping real-world demand patterns from the M5 dataset to synthetic SKUs
- Building a hybrid demand layer combining baseline consumption and failure-driven signals

The objective of this version is to establish a solid and defensible foundation before moving into forecasting, optimization, and simulation layers.

---

## Data approach (Hybrid Demand Modeling)

The core insight driving the data architecture is that MRO demand has two distinct generating processes:

1. Routine consumption that follows statistical patterns  
2. Failure-triggered spikes driven by asset degradation  

A single dataset cannot represent both faithfully, so a hybrid approach is used.

---

### 1. Baseline Demand (Statistical Realism)

The M5 Forecasting Dataset is used to anchor baseline demand behavior. It provides real-world consumption characteristics such as:

- intermittency  
- variability  
- slow-moving and fast-moving patterns  

These patterns are mapped to synthetic SKUs to preserve realistic time-series demand behavior.

---

### 2. Failure-Driven Demand (Operational Realism)

NASA CMAPSS (Commercial Modular Aero-Propulsion System Simulation) data is used to approximate failure-driven demand behavior.

Degradation trajectories and Remaining Useful Life (RUL) signals are translated into probabilistic demand spikes, capturing the non-linear surges that occur as equipment approaches failure.

This is **not a predictive maintenance system**. Instead, CMAPSS is used to model failure-linked demand behavior in a controlled and explainable way.

This is a **controlled approximation**, designed to preserve statistical realism and operational behavior rather than directly replicate real MRO systems.

---

### 3. Domain Enrichment (MRO Context)

Synthetic enrichment fills the gaps where no public dataset exists:

- location criticality  
- geopolitical exposure  
- vintage and obsolescence  
- cost parameters  

All enrichment is calibrated to domain-realistic ranges rather than random noise.

---

### Data Layer Summary

| Layer | Source | Representation |
|------|--------|---------------|
| Baseline consumption | M5 Forecasting Dataset | Intermittent, structured demand patterns |
| Failure-driven spikes | NASA CMAPSS | Degradation-driven demand surges |
| Supply risk | Trade exposure proxies | Country-level disruption risk |
| Operational context | Synthetic (domain-calibrated) | Location, lifecycle, criticality |

---

## Target architecture

| # | Dimension | Method | Purpose |
|---|----------|--------|--------|
| 1 | Demand behavior | FNS + M5-anchored forecasting | Consumption patterns |
| 2 | Financial weight | ABC / Pareto | Cost prioritization |
| 3 | Functional impact | VED analysis | Equipment operability |
| 4 | Operational context | Location Criticality scoring | Mission readiness |
| 5 | Equipment lifecycle | RUL-informed signals + vintage + obsolescence | Failure risk |
| 6 | Supply exposure | Geopolitical risk score | Disruption probability |
| 7 | Logistics penalty | Lead time + time-distance index | Network constraints |
| 8 | Stocking policy | Hybrid push/pull | Strategic vs tactical decisions |

A cost hypothesis layer runs across all versions — evaluating holding, stockout, downtime, and obsolescence costs.

---

## Tech stack

### Current (v1.1)
- Python (pandas, numpy)
- Notebook-based modeling
- Synthetic dataset generation

### Planned (v1.2+)
- Forecasting: Prophet, XGBoost, scikit-learn  
- Optimization: PuLP (MILP)  
- MLOps: MLflow, Evidently AI, DVC  
- Visualization: Streamlit  
- Deployment: FastAPI, Docker, GitHub Actions  

---

## How this will be evaluated

- Forecast accuracy (MAPE / RMSE)
- Inventory performance:
  - holding cost  
  - service level (fill rate)
- Failure-event coverage:
  - effectiveness of RUL-informed demand modeling in reducing stockouts near failure
- Sensitivity analysis:
  - response to lead time variability and disruption shocks
- Ablation testing:
  - comparison of performance with and without the failure-driven demand layer
- Financial impact:
  - baseline vs improved cost scenarios  

The goal is not just to build models, but to **quantify decision impact**.

---

## Roadmap

- **v1.1** — Core classification + hybrid demand foundation + baseline cost model *(in progress)*  
- **v1.2** — Risk-aware network + RUL-informed stocking triggers + hybrid push/pull policy + interactive dashboard  
- **v1.3** — MILP optimization + simulation + full decision intelligence layer  

---

## Background

This project builds on 19+ years of hands-on MRO operations experience across multi-origin equipment fleets.

It is part of a structured transition into AI-driven supply chain and digital transformation roles, aligned with the MITx MicroMasters in Supply Chain Management.

---

## Evolution philosophy

This repository evolves version by version, with each stage designed to be complete, defensible, and incrementally closer to a production-grade decision intelligence system.