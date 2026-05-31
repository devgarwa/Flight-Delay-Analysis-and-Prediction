# Flight Delay Analysis and Prediction

A data-driven study of U.S. domestic flight delays — what causes them, which are controllable, and how to predict both *whether* a delay happens and *how long* it lasts.

## Overview

Using the U.S. DOT/BTS airline delay-cause dataset (35K+ monthly carrier–airport records across 150+ airports), this project quantifies delay patterns, builds predictive models, and translates model explanations into concrete operational recommendations.

## Approach

- **Preprocessing** — column standardization, missing-value handling, and engineering of `avg_delay_per_flight` and a binary `delayed_flag` target.
- **EDA** — delay distributions; seasonal (monthly) patterns; delay split by cause; worst carriers and airports; flight-volume vs. delay relationships.
- **Classification** — Random Forest to predict whether a route/month is delayed (`arr_del15 > 0`).
- **Regression** — Random Forest to predict average delay minutes per flight.
- **Operational Aggregated Impact (OAI) score** — a custom weighted index that scores each record by *controllable* vs. *external* delay causes (late-aircraft and carrier delays weighted highest), modeled with XGBoost.
- **Explainability** — SHAP analysis on the OAI model to surface the biggest delay drivers (flight volume, cancellations, specific carriers, seasonality).

## Results

| Task | Model | Metric |
|---|---|---|
| Delay classification | Random Forest | ROC-AUC ≈ 0.94 |
| Delay duration (regression) | Random Forest | MAE ≈ 6.3 min |

**Insight:** ~75% of delay minutes come from *controllable* causes (late-aircraft rotation + carrier operations), pointing to high-leverage fixes — schedule buffers, faster turnarounds, and targeted resourcing at high-delay hubs.

## Tech Stack

Python · pandas · NumPy · scikit-learn · XGBoost · SHAP · Matplotlib · Seaborn

## Repository Structure

```
├── DevendraGarwa_21410010_AnalyticsProject.ipynb   # Full analysis + models
├── 21410010_AnalyticsProject_ReportDeck.pptx        # Presentation deck
└── README.md
```

## Key Takeaway

Pairing predictive models with SHAP explainability turns "flights are delayed" into "*these specific, controllable causes* drive most delay minutes — here's where to intervene."

> Note: the dataset is aggregated at the carrier–airport–month level (delay *causes*), so models operate on aggregated records rather than individual flight events.
