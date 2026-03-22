# Course Alignment: STAT 1100 → Project 04

This document maps every technique used in Project 04 (Predictive Maintenance) to the specific STAT 1100 lecture where it was taught. This ensures our project demonstrates mastery of course material.

## Task-to-Lecture Mapping

| # | Project Task | Type | Week | Lecture Topic | Technique from Class | Extension? |
|---|---|---|---|---|---|---|
| 1 | Time-series windowing | Data Prep | 3, 7 | Data Wrangling, Regression | `train_test_split`, `groupby`, rolling operations | Yes — windowing extends taught concepts |
| 2 | Sensor feature engineering | Data Prep | 5 | EDA and Visualization | `df.agg()`, `df.describe()`, correlation heatmap | Partial — rolling stats extend EDA |
| 3 | RUL label construction | Data Prep | 3 | Data Wrangling | `df.assign()`, `df.loc[]`, label engineering | Yes — project-specific label design |
| 4 | Normalisation | Data Prep | 6, 7 | Classification, Regression | `MinMaxScaler`, `StandardScaler` | No — directly from KNN + PCA notebooks |
| 5 | Train/test split by engine | Data Prep | 6 | Classification | `train_test_split(stratify=y)` | Partial — group-based split extends stratified split |
| 6 | RUL regression | Model | 7 | Supervised Learning – Regression | `LinearRegression`, RMSE, MAE, R² | No — directly from Week 7 |
| 7 | Failure horizon classification | Model | 6 | Supervised Learning – Classification | `KNeighborsClassifier`, confusion matrix, F1 | No — directly from Week 6 |
| 8 | Sequence model discussion | Model | 12 | Basic Deep Learning | Conceptual discussion only | Discussed, not implemented |
| 9 | Sensor importance analysis | Model | 8 | PCA and Factor Analysis | PCA loadings, explained variance, scree plot | No — directly from Week 8 |
| 10 | Alarm threshold analysis | Model | 6 | Classification | Precision-recall curve, threshold tuning | No — directly from KNN notebook |
| + | K-Means engine clustering | EDA | 9 | Unsupervised Learning – K-Means | `KMeans(n_clusters=k)`, elbow method, silhouette | No — directly from Week 9 |
| + | PCA dimensionality reduction | Prep | 8 | PCA and Factor Analysis | `PCA(n_components=k)`, variance ratio | No — directly from Week 8 |

## Week-by-Week Coverage

| Week | Topic | How It Appears in Our Project |
|------|-------|-------------------------------|
| 1 | Introduction to Data Science | Project context: what is predictive maintenance as a DS problem |
| 2 | Data Collection and Sources | Dataset selection rationale (ADR-001): why NASA CMAPSS |
| 3 | Data Wrangling and Pipelines | RUL label construction, data cleaning, pipeline design |
| 4 | Data Governance and Ethics | Report section on responsible use of predictive models, false positive/negative consequences |
| 5 | EDA and Visualization | Full EDA notebook: sensor analysis, correlation heatmaps, distribution plots |
| 6 | Classification and Model Eval | KNN classification for failure horizon, confusion matrix, threshold optimization |
| 7 | Regression | Linear regression for RUL prediction, RMSE/MAE/R² metrics, cross-validation |
| 8 | PCA and Factor Analysis | PCA for sensor dimensionality reduction, loadings interpretation, scree plot |
| 9 | K-Means Clustering | Engine clustering by degradation stage, elbow method, silhouette analysis |
| 10 | Deployment, UAT, Communication | Presentation: translating model findings into maintenance recommendations |
| 11 | CI/CD, Git, Reproducibility | GitHub repo with version control, assert validation cells in notebooks |
| 12 | Basic Deep Learning | LSTM discussion in report (why we chose classical ML over deep learning) |

## sklearn Patterns Used (Consistent with Course Notebooks)

All our code follows the same pattern taught in STAT 1100:
```python
from sklearn.preprocessing import MinMaxScaler          # Week 6, 8
from sklearn.model_selection import train_test_split     # Week 6
from sklearn.model_selection import GridSearchCV         # Week 6-7
from sklearn.neighbors import KNeighborsClassifier       # Week 6
from sklearn.linear_model import LinearRegression        # Week 7
from sklearn.ensemble import RandomForestRegressor       # Extension (mentioned Week 6)
from sklearn.decomposition import PCA                    # Week 8
from sklearn.cluster import KMeans                       # Week 9
from sklearn.metrics import mean_squared_error, r2_score # Week 7
from sklearn.metrics import confusion_matrix, f1_score   # Week 6
```
