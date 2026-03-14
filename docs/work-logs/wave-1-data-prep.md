# Wave 1: Data Preparation

**Date:** 2026-03-14
**Duration:** ~10 minutes (execution)
**Notebook:** `notebooks/02-data-prep.ipynb` (22 cells)

## What Was Done
1. **RUL label construction (Task 3):** Piecewise-linear cap at T=130. Raw range [0, 361] → capped [0, 130]. 7,633/20,631 rows at cap.
2. **Normalization (Task 4):** MinMaxScaler fit on train only. Dropped 7 constant sensors (1, 5, 6, 10, 16, 18, 19) → 14 useful sensors.
3. **Feature engineering (Task 2):** Rolling mean + std (window=5) per sensor → 28 rolling features. Total: 14 raw + 28 rolling = 42 features.
4. **Windowing justification (Task 1):** Rolling stats (42 features) vs explicit window flattening (420 features). Documented dimensionality reduction rationale.
5. **Train/val split (Task 5):** GroupShuffleSplit 80/20 by engine unit. Train: 16,561 rows (80 engines), Val: 4,070 rows (20 engines). Zero engine overlap verified.
6. **PCA reduction:** 42 features → 21 components (95% variance). PC1 = 47.3%.

## Key Outputs
- `data/processed/train.csv`: 14.7MB (16,561 rows × 56 cols)
- `data/processed/val.csv`: 3.6MB (4,070 rows × 56 cols)
- `data/processed/test.csv`: 89KB (100 rows × 56 cols)
- `data/processed/feature_info.json`: 2KB (feature names, RUL cap)

## Issues
- None. Notebook ran clean after path fix.
