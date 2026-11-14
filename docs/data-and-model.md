# Data preparation and semantic model

> Documented from the MIS 521 Group 2 Phase 2 report. This is a **design description** rather than a complete executable ETL pipeline.

## Dataset boundaries

- Consolidated MOJ-linked real-estate **sales** transactions supplied to the academic group.
- **1,439,706** distinct transaction references; **25** consecutive quarters, **2020 Q1–2026 Q1**.
- Full calendar-year comparisons only for 2024 vs 2025. The first quarter of 2026 is not a complete year.
- The restored **2025 Q2** contributes **42,518** references to the supplied snapshot. This is not a claim about every real-world transaction in that quarter.

## Quality gates

| Check | Observed result | Treatment |
|:--|:--|:--|
| Region labels | 16 spellings mapped into 13 regions | Standardise before relationship keys |
| Unique transaction reference | No duplicates or blanks in the supplied consolidated file | Preserve transaction-grain fact table |
| Nonpositive area | 1 transaction | Retain for volume/value; blank its analytical m² unit price |
| Source unit-price review flags | 9,812 transactions | Retain; calculate separate sensitivity metric |
| Geography | 15,623 Region-City-District combinations | Check relationship keys and unmatched facts |
| DimDate | 2,282 daily calendar rows | Establish Year → Quarter → Month filters |

Thresholds used in the source for price-area screening (< SAR 1/m² or > SAR 100,000/m²) were **review criteria**, not government market limits or definitive errors.

## Conceptual model

| Entity | Role | Contents |
|:--|:--|:--|
| **FactSales** | Transaction-level fact | Reference, date, location/class keys, price, valid analytical area, review fields |
| **DimDate** | Calendar dimension | Dates, year, quarter, month |
| **DimLocation** | Geographic dimension | Region, city, district |
| **DimPropertyClass** | Category dimension | Source property-classification labels |
| **Sales_Quality** | Disconnected audit | Full-file quality metrics independent of dashboard filters |

Each dimension filters FactSales through an active one-to-many relationship. Region → City → District is the navigation hierarchy. The audit table is deliberately disconnected.

## Metric definitions

1. **Total transactions:** distinct transaction references.
2. **Total transaction value:** sum of recorded transaction prices in nominal SAR.
3. **Average transaction value:** total value divided by distinct transaction count.
4. **Median SAR per m²:** median of valid transaction-level (price ÷ positive area). Not a ratio of total value to total area.
5. **YoY transaction growth:** count movement versus the equivalent previous-year period, only where period coverage permits.

## Reproducibility boundary

The DAX expressions, Power Query steps, original PBIX, source snapshot and test logs are **not present** in this public-style case-study folder. These descriptions must not be presented as deployable source code. The group reports describe independent numerical reconciliations and two-page dashboard review.

[Return to case study](../README.md)
