# ADR-001: Dataset Selection
**Date:** 2026-03-14
**Status:** Accepted

## Context
Project 04 (Predictive Maintenance) requires selecting a dataset that naturally supports the 10 required project tasks: data collection, wrangling, EDA, visualization, supervised classification, supervised regression, unsupervised learning, model evaluation, deployment considerations, and communication. Two candidate datasets were shortlisted: NASA CMAPSS (turbofan engine degradation) and AI4I 2020 (synthetic manufacturing failure).

## Decision
Use NASA CMAPSS FD001 sub-dataset.

FD001 specifically: single operating condition, single fault mode (HPC degradation), 100 training engines, 100 test engines. This is the simplest of the four CMAPSS sub-datasets, offering the cleanest storytelling for a 15-minute presentation while still requiring non-trivial data engineering.

The 10 required tasks map naturally to CMAPSS's time-series structure:
- Time-series windowing and rolling statistics (Task 3: Wrangling)
- RUL label construction from raw cycle counts (Task 3: Wrangling)
- Sensor correlation analysis across degradation phases (Task 4: EDA)
- Normalization across operating settings (Task 3: Wrangling)
- Binary classification via failure horizon threshold (Task 5: Classification)
- Continuous RUL regression (Task 6: Regression)
- PCA on 21 sensor channels (Task 7: Unsupervised)

## Alternatives Considered
- **AI4I 2020 Predictive Maintenance Dataset:** Flat tabular data with 10,000 rows and pre-computed features. Simpler to work with, but the time-series windowing task (Task 3) and RUL label construction would be forced/artificial since the data is already single-observation-per-machine. Poor fit for demonstrating data pipeline skills.
- **CMAPSS FD002:** 6 operating conditions, 260 engines. Requires per-condition normalization stratification -- added complexity with no additional grading benefit.
- **CMAPSS FD003:** Multiple fault modes. Introduces multi-label complexity unnecessary for an intro course project.
- **CMAPSS FD004:** 6 conditions + multiple faults. Most complex sub-dataset, highest overfitting risk, hardest to present clearly in 15 minutes.

## Course Reference
Week 2: Data Collection and Data Sources. Lecture 2 covers data source evaluation criteria including fitness for purpose, data quality, and ethical considerations. CMAPSS is a publicly available NASA benchmark -- no privacy or ethical concerns.

## Consequences
- All feature engineering (RUL labels, rolling windows, sensor selection) must be implemented from scratch -- no pre-computed labels exist.
- Dataset is well-studied in literature, so we can validate our results against published benchmarks (e.g., RMSE ~13-17 for classical ML on FD001).
- Single operating condition means MinMaxScaler is sufficient (no per-condition stratification needed).
- 100 engines is small enough that overfitting is a real risk -- model complexity must be carefully controlled (see ADR-003, ADR-004).
