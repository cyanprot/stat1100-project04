# Wave 1: Exploratory Data Analysis

**Date:** 2026-03-14
**Duration:** ~15 minutes (execution)
**Notebook:** `notebooks/01-eda.ipynb` (28 cells)

## What Was Done
- Loaded FD001 train (20,631 rows), test (13,096 rows), RUL (100 engines)
- Engine lifespan analysis: 128–362 cycles, mean 206.3, median 199.0
- 21-sensor subplots for sample engine — identified degradation trends
- Multi-engine overlay (5 engines) — confirmed consistent degradation patterns
- Constant sensor detection: sensors 1, 5, 10, 16, 18, 19 flagged (std < threshold)
- Correlation heatmap: 7 strongly correlated pairs (|r| > 0.8), e.g., sensor_9 ↔ sensor_14 (r=0.963)
- PCA on 15 useful sensors: PC1 = 60.2% variance, 10 components for 95%
- K-Means clustering (k=3): Cluster 0 (critical, mean RUL=21.9), Cluster 1 (degrading, mean RUL=105.7), Cluster 2 (healthy, mean RUL=155.6)
- Silhouette analysis: best k=2 (score 0.428), used k=3 for interpretability
- Test set RUL distribution: 25/100 engines critical (≤30), 8/100 healthy (>130)

## Key Outputs
- Output notebook: 2.7MB (plots embedded as base64 PNG)
- No files saved to disk (EDA is exploratory only)

## Issues
- None. Notebook ran clean on first execution after path fix.
