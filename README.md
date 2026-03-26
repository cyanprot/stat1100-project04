# Predictive Maintenance for Industrial Equipment

**STAT 1100 — Introduction to Data Science | Langara College | Spring 2026**

Aedrian Formento & Jongmin Lee | Instructor: Vincent Yeung

---

## Overview

Data-driven predictive maintenance system using the NASA CMAPSS turbofan engine dataset. Predicts Remaining Useful Life (RUL) and triggers cost-optimized maintenance alerts based on sensor degradation patterns.

**Key Results:**
- Random Forest RUL regression: **RMSE 17.40** (val), **18.72** (test), R² 0.79
- KNN failure classification (K=19): **F1 0.89** (val), threshold-optimized
- Monte Carlo cost simulation: **72.3% savings** vs scheduled maintenance ($361,500/year for 100-engine fleet)

## Repository Structure

```
├── notebooks/
│   ├── 01-eda.ipynb              ← Exploratory Data Analysis + PCA + K-Means
│   ├── 02-data-prep.ipynb        ← 5 data preparation tasks + pipeline
│   └── 03-modeling.ipynb         ← 5 model tasks + SHAP + Monte Carlo
├── report/
│   └── report.md                 ← Full written report (30% of grade)
├── proposal/
│   └── proposal.md               ← Project proposal (5% of grade)
├── presentation/
│   ├── presentation.html         ← 11-slide presentation (16:9)
│   └── presentation.pdf          ← PDF export
├── docs/
│   ├── adrs/                     ← 7 Architecture Decision Records
│   ├── course-alignment.md       ← Lecture-to-task mapping
│   └── work-logs/                ← Per-phase execution logs
├── data/
│   ├── CMAPSSData/               ← Raw NASA dataset (gitignored)
│   └── processed/                ← Preprocessed CSVs + feature info
└── .gitignore
```

## Dataset

[NASA CMAPSS FD001](https://data.nasa.gov/) — 100 turbofan engines, 21 sensors, run-to-failure time series.

## Techniques Used (STAT 1100 Curriculum)

| Week | Topic | Application |
|------|-------|-------------|
| 3 | Data Wrangling | RUL label construction, piecewise-linear cap at 130 |
| 5 | EDA | Sensor behavior, constant sensor detection, correlation |
| 6 | Classification | KNN (K=19), confusion matrix, F1, threshold optimization |
| 7 | Regression | Linear Regression baseline, Random Forest, RMSE/MAE/R² |
| 8 | PCA | Dimensionality reduction, sensor importance via loadings |
| 9 | K-Means | Engine degradation stage clustering (3 clusters) |
| 11 | CI/CD | GitHub, assert-based validation gates |
| 12 | Deep Learning | LSTM discussion (not implemented — justified in ADR-007) |

## How to Run

```bash
# Clone and set up
git clone https://github.com/cyanprot/stat1100-project04.git
cd stat1100-project04
python3 -m venv .venv && source .venv/bin/activate
pip install pandas numpy scikit-learn matplotlib seaborn shap jupyterlab

# Run notebooks in order
jupyter lab notebooks/
```

Or open directly in [Google Colab](https://colab.research.google.com/) — each notebook downloads the dataset automatically.

## License

MIT License
