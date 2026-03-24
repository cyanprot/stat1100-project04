# Project Proposal: Predictive Maintenance for Industrial Equipment

**Course:** STAT 1100 — Introduction to Data Science
**Instructor:** Vincent Yeung
**Team Members:** Jongmin, Aedrian
**Date:** March 14, 2026

---

## 1. Problem Statement

Manufacturing companies face significant financial losses from unplanned equipment failures. Traditional scheduled maintenance strategies — replacing parts at fixed intervals regardless of condition — lead to either premature replacements (wasting resources) or unexpected breakdowns (halting production). This project applies data science techniques to predict when equipment will fail, enabling a shift from scheduled maintenance to **condition-based intervention**.

## 2. Dataset

We will use the **NASA Turbofan Engine Degradation Simulation Dataset (CMAPSS)**, specifically the FD001 subset:

- **Source:** NASA Prognostics Data Repository / Kaggle
- **Size:** 20,631 training observations across 100 engine units
- **Features:** 21 sensor measurements + 3 operational settings per time cycle
- **Target:** Remaining Useful Life (RUL) — the number of operational cycles before engine failure
- **Structure:** Time-series data where each engine runs from a healthy state to failure

We selected CMAPSS over simpler alternatives (e.g., AI4I 2020) because its time-series structure maps naturally to all 10 required project tasks, including time-series windowing, RUL label construction, and normalization across operating conditions.

## 3. Proposed Approach

Our approach applies techniques directly from STAT 1100 lectures:

### Data Preparation
1. **Time-series windowing** (Week 3, 7): Extract temporal patterns using rolling statistics
2. **Sensor feature engineering** (Week 5): Create rolling mean, standard deviation, and trend features
3. **RUL label construction** (Week 3): Design piecewise-linear labels with a cap at 130 cycles
4. **Normalization** (Week 6): Apply MinMaxScaler to sensor readings, fitted on training data only
5. **Train/test split** (Week 6): Group-based split by engine unit to prevent data leakage

### Model Building
1. **RUL Regression** (Week 7): Linear Regression baseline, with Random Forest as an extension
2. **Failure Classification** (Week 6): KNN classifier to predict failure within 30 cycles
3. **Sequence Model Discussion** (Week 12): Analysis of deep learning applicability
4. **Sensor Importance** (Week 8): PCA loadings and feature importance analysis
5. **Alarm Threshold** (Week 6): Cost-benefit analysis for maintenance scheduling decisions

### Additional Analysis
- **PCA dimensionality reduction** (Week 8) on the 21-sensor feature space
- **K-Means clustering** (Week 9) to identify engine degradation stages
- **Monte Carlo simulation** for robust cost estimation under uncertainty

## 4. Timeline

| Period | Milestone |
|--------|-----------|
| Mar 14–17 | Data preparation: download, EDA, preprocessing pipeline |
| Mar 17–19 | Model building: regression, classification, evaluation |
| Mar 19–21 | Report writing, documentation, code review |
| Mar 22–25 | Midterm break |
| Mar 26–30 | Presentation preparation |
| Mar 31 | Project presentation |

## 5. Expected Deliverables

1. **Jupyter Notebooks** (50%): Three reproducible notebooks covering EDA, data preparation, and model building
2. **Written Report** (30%): Technical report documenting all 10 tasks with justifications and business context
3. **Presentation** (20%): Non-technical presentation translating findings into maintenance recommendations for plant management

## 6. Tools and Technologies

- **Language:** Python 3.12
- **Libraries:** scikit-learn, pandas, NumPy, matplotlib, seaborn
- **Environment:** Google Colab (shared), local Python with Jupyter
- **Version Control:** GitHub ([repository link](https://github.com/cyanprot/stat1100-project04))

---

*We look forward to applying the data science techniques learned in STAT 1100 to this real-world predictive maintenance challenge.*
