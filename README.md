# Geo-Aware MRO Decision Intelligence System

**Multi-criteria spares classification · Geopolitical risk integration · Hybrid Push/Pull stocking · Multi-echelon network optimization**

*v1.1 in progress*

---

## What this is

Standard reorder-point logic breaks down fast when your supply chain has real geopolitical exposure — when parts come from six different countries, some of which are increasingly complicated to source from, and when a stockout at a forward operating location has completely different consequences than one at a rear base.

This project builds a structured decision support system for large-scale MRO operations involving multi-origin equipment fleets. It integrates demand behavior, functional criticality, operational location, geopolitical risk, and network constraints into a single quantifiable framework — moving from reactive inventory management to something you can actually defend.

Built on 19+ years of hands-on MRO operations experience. The domain knowledge came first. The system is being built to match it.

---

## Current state (v1.1 — Foundation)

The focus right now is the classification and data layer — the groundwork everything else will sit on.

**What's implemented:**
- Multi-criteria SKU classification: FNS (velocity), ABC (cost weight), VED (functional criticality), Location Criticality (border / high-altitude / forward / rear)
- Synthetic MRO dataset with domain-realistic attributes — not random noise
- Basic geo-risk and lead time modeling
- Baseline cost hypothesis: holding cost, stockout cost, downtime impact

The point of this version is to get the foundation right, not to rush the interesting parts.

---

## Target architecture

| # | Dimension | Method | Purpose |
|---|---|---|---|
| 1 | Demand behavior | FNS classification | Consumption patterns |
| 2 | Financial weight | ABC / Pareto | Cost prioritization |
| 3 | Functional impact | VED analysis | Equipment operability |
| 4 | Operational context | Location Criticality scoring | Mission readiness |
| 5 | Equipment lifecycle | Vintage + electronic intensity + obsolescence | Upgrade and end-of-life risk |
| 6 | Supply exposure | Geopolitical risk score | Disruption probability |
| 7 | Logistics penalty | Lead time + time-distance index | Network constraints |
| 8 | Stocking policy | Hybrid push/pull | Strategic vs. tactical decisions |

A cost hypothesis layer runs across all versions — baseline vs. improved outcomes across holding, stockout, downtime, and obsolescence costs.

---

## Data approach

Hybrid — combining real-world demand anchors with synthetic MRO-specific enrichment where data is not publicly available.

- **v1.1:** Synthetic SKU master built with MRO-realistic attributes
- **v1.2+:** Demand anchored to the M5 Forecasting Dataset; supply risk calibrated via UN Comtrade trade exposure proxies; synthetic enrichment for vintage and obsolescence Controlled, explainable, and defensible.

---

## Stack

**Now:** Python (pandas, numpy) · Notebook-based modeling

**Planned:** Prophet + XGBoost · PuLP (MILP) · MLflow + Evidently AI · Streamlit · FastAPI + Docker + GitHub Actions

---
## How this will be evaluated

- Forecast accuracy (MAPE / RMSE)
- Inventory performance (holding cost, service level)
- Sensitivity to lead time and disruption shocks
- Financial impact (baseline vs improved cost scenarios)

The goal is not just to build models, but to quantify decision impact.
----

## Roadmap

- **v1.1** — Core classification + baseline cost model *(in progress)*
- **v1.2** *(Aug–Oct 2026)* — Risk-aware network + hybrid push/pull policy + interactive dashboard
- **v1.3** — MILP optimization + simulation + full decision intelligence layer

---

## Background

Part of a structured transition from MRO operations into AI-driven supply chain and digital transformation roles. Running alongside the MITx MicroMasters in Supply Chain Management.

This repository will evolve version by version, with each stage designed to be complete and defensible on its own.