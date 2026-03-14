# ADR-005: Failure Horizon Threshold
**Date:** 2026-03-14
**Status:** Accepted

## Context
The classification task requires converting continuous RUL into a binary label: "will this engine fail within N cycles?" The choice of N (the failure horizon) directly affects class balance, model utility, and real-world interpretability. Too small and the positive class is rare (imbalanced data problem); too large and the prediction is not actionable ("this engine will fail sometime in the next 100 cycles" is not useful for maintenance scheduling).

## Decision
Set the failure horizon threshold at 30 cycles.

Binary label: label_binary = 1 if RUL <= 30, else 0.

In the FD001 training data, this produces approximately 30% positive class (engines within 30 cycles of failure) and 70% negative class. This is a manageable imbalance that does not require SMOTE, class weighting, or other resampling techniques -- standard accuracy, precision, recall, and F1 are all meaningful metrics at this ratio.

From a domain perspective, 30 cycles represents a realistic maintenance scheduling window: enough lead time to plan a turbofan engine inspection or replacement, but close enough to failure that the prediction carries operational urgency.

## Alternatives Considered
- **15 cycles:** Approximately 15% positive class in FD001 training data. Creates significant class imbalance requiring SMOTE or class weights. While more operationally precise ("imminent failure"), the imbalance handling adds pipeline complexity and potential for artifacts (SMOTE on time-series-derived features is debatable).
- **50 cycles:** Approximately 45% positive class, nearly balanced. However, predicting failure 50 cycles out is less actionable -- many engines show minimal sensor degradation at this horizon, making the classification task harder for the model and the prediction less useful for maintenance teams.
- **Multiple thresholds (multi-class):** E.g., "healthy / degrading / critical" with thresholds at 60 and 15. More informative but converts the problem to multi-class classification, which is not covered in the KNN notebook (binary only). Adds complexity without clear grading benefit.

## Course Reference
Week 6: Supervised Learning -- Classification. The lecture covers class balance considerations, confusion matrix interpretation (precision, recall, F1), and threshold-based decision making. Our 70/30 split is close enough to balanced that we can use standard metrics without special handling, while still demonstrating awareness of the imbalance issue.

## Consequences
- ~30% positive class allows straightforward use of accuracy, precision, recall, F1 without resampling.
- The threshold is a hyperparameter we can discuss in the report as a domain-driven choice, demonstrating understanding beyond pure ML.
- KNN classification results can be directly compared across k values using F1-score as the primary metric.
- If a model achieves high recall at this threshold, it means we catch most engines within 30 cycles of failure -- a compelling narrative for the presentation.
- The 30-cycle threshold must be consistent with the RUL cap (130 cycles, ADR-002): since 30 << 130, all engines in the "failure zone" are well within the degradation phase where sensors are informative.
