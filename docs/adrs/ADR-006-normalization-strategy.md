# ADR-006: Normalization Strategy
**Date:** 2026-03-14
**Status:** Accepted

## Context
CMAPSS FD001 has 21 sensor channels with widely varying scales (e.g., temperature in hundreds of degrees vs. pressure ratios near 1.0). Distance-based models like KNN are extremely sensitive to feature scale -- a sensor ranging [500, 650] would dominate distance calculations over a sensor ranging [0.95, 1.05] despite both containing equally important degradation information. Linear Regression coefficients also become uninterpretable without normalization.

Additionally, 7 of the 21 sensors (sensors 1, 5, 6, 10, 16, 18, 19) are constant or near-constant across all engines and cycles in FD001. These carry no discriminative information and must be removed before normalization to avoid division-by-zero (MinMaxScaler) or zero-variance issues (StandardScaler).

## Decision
1. **Drop constant sensors:** Remove sensors 1, 5, 6, 10, 16, 18, 19 (7 sensors), retaining 14 informative sensors.
2. **Apply MinMaxScaler:** Scale all retained features to [0, 1] range.
3. **Fit on training data only:** The scaler is fitted (min/max values computed) exclusively on the training set. The same fitted scaler is then applied (transform only) to the test set. This prevents data leakage -- test set statistics must not influence any preprocessing step.

Since FD001 has a single operating condition, there is no need for per-condition stratified normalization. A single global scaler is sufficient.

## Alternatives Considered
- **StandardScaler (z-score normalization):** Equally valid and used in the PCA notebook (Week 8). We chose MinMaxScaler because (a) the KNN notebook uses MinMaxScaler, maintaining consistency with course materials, and (b) [0, 1] bounded outputs are more interpretable in visualizations and feature importance discussions.
- **Per-condition normalization:** Required for FD002/FD003/FD004 where different operating conditions shift sensor baselines. Unnecessary for FD001 (single condition) and would add complexity for no benefit.
- **RobustScaler (median/IQR):** Resistant to outliers, but CMAPSS sensor data is well-behaved (no extreme outliers in FD001). Adds a concept (IQR-based scaling) not covered in course materials.
- **No normalization:** Catastrophic for KNN (distance metric dominated by high-magnitude sensors). Harmful for LR (coefficient interpretation breaks). Only RF is scale-invariant, but we need consistent preprocessing across all models.
- **Keeping constant sensors:** They contribute zero information but add dimensionality. Dropping them is standard practice in all CMAPSS literature and reduces noise in PCA visualization.

## Course Reference
- Week 6: KNN notebook uses MinMaxScaler for feature normalization before distance computation.
- Week 8: PCA notebook uses StandardScaler before computing principal components.
- Both lectures emphasize the importance of fitting preprocessing on training data only to prevent data leakage.

## Consequences
- All features are in [0, 1] range, making KNN distance calculations fair across sensors.
- LR coefficients become directly comparable in magnitude (larger coefficient = more influential feature).
- PCA on normalized features produces meaningful principal components (no single sensor dominates variance due to scale).
- The scaler object must be saved (pickled) alongside the trained model for deployment (Week 10) -- any new data must be transformed with the same min/max values.
- 14 sensors x 3 rolling statistics (ADR-003) + 14 raw values = ~56 features, all normalized to [0, 1].
