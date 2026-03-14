# Wave 3: Report Finalization

**Date:** 2026-03-14
**Duration:** ~20 minutes

## What Was Done
- Updated report.md with actual metrics from executed notebooks (replaced all approximate/estimated values)
- Key corrections from initial estimates:
  - LR RMSE: ~24.1 → 21.00 (model performed better than expected)
  - LR R²: ~0.58 → 0.77 (significantly better)
  - RF params: max_depth=20 → 10, min_samples_leaf=2 → 5 (less complex tree)
  - Best K: 7 → 19 (higher K for smoother boundaries in 42-dim space)
  - Critical F1: ~0.78 → 0.89 (better classification)
  - Optimal threshold: 25-30 → 10 cycles (cost model favored tight threshold)
  - Savings: ~65% → 72.3% ($361,500/yr)
- Updated cluster descriptions with actual RUL means
- Updated PCA variance explanations with actual component counts
- Added test set results table to regression section

## Key Outputs
- `report/report.md`: ~340 lines, all metrics verified against notebook outputs

## Issues
- Cluster ordering was inverted from initial assumption (Cluster 0 = critical, not healthy). Corrected in report.
