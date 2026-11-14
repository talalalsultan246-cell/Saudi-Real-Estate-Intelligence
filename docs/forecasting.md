# Forecasting methods and validation

**Target:** next-quarter number of recorded real-estate transactions per administrative region. **Not** sale price, investment return, or a villa-specific series.

## Design and split

- The Python extension is separate from the delivered Power BI reporting model.
- **273 eligible region-quarter rows** from 2021 Q1 onward.
- **208 development rows (2021 Q1–2024 Q4)** and **65 retrospective holdout rows (2025 Q1–2026 Q1)**.
- Within development, **156 initial training rows** precede **52 expanding-window validation observations** from four 2024 forecast origins.
- One-quarter-ahead time ordering; encoding fitted on the corresponding training fold; **no random split**.
- A **200-tree RandomForestRegressor** and Seasonal Naive (the same quarter one year previously).
- Earlier broader model search also contained XGBoost; its development WAPE was lower than RF's.

## Reported measured results

| Criterion | Random Forest | Seasonal Naive |
|:--|--:|--:|
| Development validation WAPE | 19.77% | 27.32% |
| Retrospective holdout WAPE | 24.95% | 45.44% |
| Retrospective holdout MAE | 898.70 | 1,636.71 |

The report also states **RF holdout RMSE = 1,989.99**, pooled **R² = 0.790**, and **10/13 negative region-specific R²**.

**WAPE** = sum(|actual − predicted|) / sum(|actual|) × 100, over the specified evaluation observations. MAE uses the mean absolute error, RMSE the root mean squared error. Lower WAPE does **not** mean a corresponding classification accuracy.

**Inference boundary:** Prior holdout observations were inspected in the wider experiment. The subsequently reported focused RF comparison is retrospective, not a clean post-selection confirmatory assessment. Regional error variation is substantial; the report notes quarter-level holdout WAPE spanning **8.16%–49.21%**. The RF prototype was **not** the universally strongest candidate: XGBoost attained **17.20%** on earlier development validation versus **19.77%** for RF.

## Exploratory horizon, not a live forecast

The model produced exploratory estimates for **2026 Q2**, refit through 2026 Q1. By November 2026 this forecast target lies in the past, but the team's supplied transaction file ends in March 2026. The estimates must not be represented as current forward-looking predictions or verified against unseen Q2 actuals.

## What must happen before deployment

1. Obtain later source releases and establish fresh, untouched chronological test periods.
2. Compare several model families and a seasonal benchmark across regions.
3. Review model calibration, interval coverage and geographic stability.
4. Record source version, feature freeze date, error tables and reviewer sign-off.

[Return to case study](../README.md)
