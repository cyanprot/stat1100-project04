# Wave 2: Model Building

**Date:** 2026-03-14
**Duration:** ~5 minutes (execution)
**Notebook:** `notebooks/03-modeling.ipynb` (39 cells)

## What Was Done

### Task 1: RUL Regression
- Linear Regression baseline: RMSE 21.00, MAE 16.84, R² 0.77
- Random Forest (GridSearchCV + GroupKFold): RMSE 17.40, MAE 12.41, R² 0.84
- Best RF params: n_estimators=200, max_depth=10, min_samples_leaf=5
- RF improvement: 17.1% RMSE reduction over LR
- Predicted-vs-actual scatter + residual plots generated

### Task 2: Failure Horizon Classification
- KNN with GridSearchCV (K=3..21 odd), GroupKFold
- Best K=19
- Validation: Critical F1=0.89, precision=0.92, recall=0.86, accuracy=0.97
- Confusion matrix: TP=536, FN=84, FP=44, TN=3406

### Task 3: Sequence Model
- LSTM discussion in markdown cells — justified non-implementation (Week 12 overview only)

### Task 4: Sensor Importance
- PCA loadings (top 5 PCs = 66.0% variance)
- RF feature_importances_
- Permutation importance
- Consensus features (top 10 in all 3): sensor_11_rmean, sensor_4_rmean, sensor_7_rmean

### Task 5: Alarm Threshold
- Deterministic sweep (threshold 10–60): optimal = 10 cycles, cost = $3,405,000
- Monte Carlo (1000 sims): mean $138,500/yr, median $130,000/yr, 95% CI [$25K, $310K]
- vs scheduled $500K/yr → savings $361,500/yr (72.3%)

### Final Test Set
- RF Regression: RMSE 18.72, MAE 13.21, R² 0.79
- KNN Classification: Critical F1=0.76, recall=0.64, accuracy=0.90

### SHAP Explainability (added 2026-03-14)
- SHAP TreeExplainer on RF regressor, 500 validation samples
- Top feature: sensor_4_rmean (mean |SHAP| = 25.51), 2x the runner-up
- Top 5: sensor_4_rmean (25.51), sensor_9_rmean (11.75), sensor_11_rmean (9.92), sensor_21_rmean (9.66), sensor_14_rmean (4.38)
- Beeswarm + bar plots generated

### Calibration Analysis (added 2026-03-14)
- KNN Brier score: raw 0.0245, calibrated (Platt) 0.0227, 7.1% improvement
- Calibration curves plotted for raw vs Platt-scaled probabilities

## Key Outputs
- Output notebook: 1.2MB (SHAP + calibration plots embedded)
- All assert validation cells passed
- SHAP/calibration images: data/processed/shap_summary.png, calibration_curves.png

## Issues
- Initial execution failed: injected cells used `data/processed/` instead of `../data/processed/` (kernel CWD = notebooks/). Fixed paths + re-executed.
- feature_info.json key was `feature_cols` not `feature_columns`. Fixed.
