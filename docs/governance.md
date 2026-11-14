# Decision governance, access and limitations

## Stakeholders and decisions

The academic case supports analysts, planners and decision-makers who want to:
- monitor regional transaction activity against matching historical periods;
- identify where deeper district- and classification-level investigation is warranted;
- compare segments without extrapolating observed correlations into causal or investment claims.

## Documented recommendations

| Area | Proposed SMART action | Status |
|:--|:--|:--|
| Riyadh regional investigation | Review five prioritised city profiles within 30 days and obtain sign-off | Proposal |
| Three-region comparison | Produce a reviewed quarterly/class comparison of Riyadh, Makkah and Eastern Province within 60 days | Proposal |
| Forecast monitoring | Track RF against Seasonal Naive for two new quarterly refreshes | Research pilot |
| Regulatory-event tracking | Log relevant dates and review geography-specific effects after the next complete quarterly release | Proposal, not causal evaluation |

The report's 10%–30% assumed analyst-time savings were **planning scenarios**. No measured time-saving experiment or monetary-benefit claim is available.

## Row-level security

The Phase 3 report documents an **Asir_Analyst** filter configured on DimLocation[RegionEN] = "Asir" in Power BI Desktop. Its screenshots show:
- full 2025 all-region view: 201,556 transactions;
- Asir role test: 9,317 transactions and approximately SAR 4.71 billion;
- desktop role banner visible.

This demonstrates a *Desktop test of displayed regional measures*, **not** production authorization, service deployment, completed user assignments, or independent proof that the distributed PBIX includes the saved role. A separately reopened PBIX and service-level role audit would be required for stronger claims.

## Data ethics and refresh gates

- Transaction-level geography, dates and prices may pose indirect identification risks even when records are sourced publicly.
- Avoid including person-identifying attributes, student identifiers, restricted university documents or access credentials in portfolio publications.
- Record raw source URL, version/hash, quarter coverage, row count, change log, abnormal values and review outcome before releasing updated analysis.
- Proposed refresh: after each new quarterly source release, subject to source availability and reconciliation.

## Analytical limitations

- The reports use a supplied consolidated snapshot; public source availability is **not** proof of complete coverage.
- A property transaction can include multiple properties; property-level counts cannot be inferred.
- Broad categories are not validated villa/apartment transaction type series.
- Historical changes do not identify financing, regulatory or policy effects.
- Forecasts are for regional counts; pooled performance conceals locally weak fit.

[Return to case study](../README.md)
