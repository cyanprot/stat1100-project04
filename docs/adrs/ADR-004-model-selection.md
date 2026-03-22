# ADR-004: Model Selection
**Date:** 2026-03-14
**Status:** Accepted

## Context
The project requires both regression (predicting continuous RUL) and classification (predicting binary failure-within-horizon). Models must be selected from or closely related to algorithms taught in STAT 1100 lectures and labs. The course covers KNN (Week 6), Linear Regression (Week 7), PCA (Week 8), and K-Means (Week 9) with hands-on notebooks. Random Forest is mentioned in Lecture 6 slides as a supervised learning algorithm but has no dedicated notebook.

## Decision
Three supervised models, explicitly tiered by course coverage:

1. **Linear Regression (primary regression baseline):** Direct application of Week 7 content. Used for continuous RUL prediction. Serves as the interpretable baseline against which other models are compared.

2. **K-Nearest Neighbors (classification and regression):** Direct application of Week 6 content. Used for binary classification (failure within 30 cycles) and optionally for RUL regression. Hyperparameter k tuned via cross-validation as taught in the KNN notebook.

3. **Random Forest (extension model):** Mentioned in Lecture 6 slides as an ensemble supervised learning method. Included as a justified extension -- clearly labeled as "beyond core course content" in the report. Provides a non-linear baseline that contextualizes LR and KNN performance.

For unsupervised learning (Task 7), PCA is applied for dimensionality reduction and visualization (Week 8), and K-Means is applied for engine health state clustering (Week 9).

## Alternatives Considered
- **XGBoost / Gradient Boosting:** Not taught in any lecture. While it would likely achieve the best performance, using it without course foundation risks appearing as "black box borrowed from the internet" rather than a deliberate, justified choice.
- **Support Vector Machine (SVM):** Mentioned briefly in Lecture 6 but not practiced in any lab or notebook. Less interpretable than LR, less intuitive than KNN, and adds no pedagogical value over RF as an extension model.
- **LSTM / Neural Network:** Covered only as a conceptual overview in Week 12. Not implemented (see ADR-007 for full rationale).
- **Ridge / Lasso Regression:** Valid extensions of LR, but regularization is not covered in the course. Adding them would require explaining concepts not in the syllabus without clear grading benefit.

## Course Reference
- Week 6: Supervised Learning -- Classification (KNN, model evaluation, confusion matrix)
- Week 7: Supervised Learning -- Regression (Linear Regression, RMSE, R-squared)
- Week 8: Unsupervised Learning -- PCA (dimensionality reduction)
- Week 9: Unsupervised Learning -- K-Means (clustering)

## Consequences
- Every model used can be traced to a specific lecture week, which strengthens the "course alignment" narrative in the report.
- Random Forest must be explicitly flagged as an extension with justification (ensemble of decision trees, conceptual extension of classification from Week 6).
- Model comparison table (LR vs KNN vs RF) becomes a natural structure for the evaluation section.
- PCA serves dual purpose: unsupervised learning task requirement + feature reduction for KNN (which suffers from curse of dimensionality).
- K-Means clustering on engine sensor profiles can identify "health states" that provide an unsupervised complement to the supervised RUL prediction.
