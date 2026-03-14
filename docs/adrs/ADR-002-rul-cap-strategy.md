# ADR-002: RUL Cap Strategy
**Date:** 2026-03-14
**Status:** Accepted

## Context
CMAPSS provides raw cycle data per engine (e.g., engine runs for 192 cycles total). The Remaining Useful Life (RUL) label for each row is computed as max_cycle - current_cycle, producing values ranging from 0 to ~350+. However, early in an engine's life, degradation is undetectable by sensors -- a row at cycle 10 (RUL=340) and cycle 50 (RUL=300) look effectively identical in sensor readings. Forcing a regression model to distinguish between these "very healthy" states wastes model capacity on noise.

## Decision
Apply a piecewise-linear RUL cap at T=130 cycles. Any row with computed RUL > 130 is clipped to 130.

This produces a label distribution where:
- RUL in [0, 130]: linear decay, model learns degradation trajectory
- RUL > 130: all clamped to 130, model treats as "healthy, not yet degrading"

T=130 is the CMAPSS literature standard, established by Heimes (2008) and widely adopted in subsequent publications (Ramasso & Saxena 2014, Li et al. 2018).

## Alternatives Considered
- **No cap (raw linear RUL):** Labels range from 0 to 350+. Model wastes capacity distinguishing RUL=300 from RUL=250 when sensor readings are identical. Empirically shown to increase RMSE by 15-25% in literature.
- **Exponential decay:** RUL = exp(-alpha * (max_cycle - current_cycle)). More theoretically motivated (degradation often follows exponential curves), but adds a hyperparameter (alpha) and provides marginal benefit over piecewise-linear for FD001. More complex to explain in presentation.
- **Lower cap (T=100):** Loses some information in the early degradation phase. T=130 is the established standard; deviating requires justification we don't have.
- **Higher cap (T=150+):** Diminishing returns. Sensor readings in the 130-150 RUL range already show minimal variation.

## Course Reference
Week 3: Data Wrangling and Data Pipelines. Label engineering (transforming raw data into model-ready targets) is a form of data transformation covered in the wrangling lecture. The RUL cap is our most significant wrangling decision.

## Consequences
- The regression target is bounded in [0, 130], which makes RMSE more interpretable (errors are meaningful within this range).
- Classification threshold (ADR-005) must be set well below 130 to be within the "active degradation" zone.
- This is a domain-specific decision that must be explicitly justified in the report -- it demonstrates understanding of the problem beyond just applying algorithms.
- Training labels become right-censored at 130, which is acceptable for the models we use (LR, RF, KNN) but would require special handling for probabilistic models.
