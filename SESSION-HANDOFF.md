# Session Handoff — 2026-03-14

## Done
- Repo scaffolded + pushed: github.com/cyanprot/stat1100-project04
- northprot env: venv at ~/Academia/STAT1100/.venv (sklearn 1.8, pandas 3.0, numpy 2.4)
- Jupyter kernel `stat1100` registered
- CMAPSS FD001 downloaded: data/CMAPSSData/ (train 20,631 / test 13,096 / RUL 100)
- 3 notebooks created (NOT YET EXECUTED):
  - 01-eda.ipynb (28 cells) — EDA + PCA + K-Means
  - 02-data-prep.ipynb (22 cells) — 5 prep tasks + PCA reduction
  - 03-modeling.ipynb (39 cells) — LR/RF/KNN + Monte Carlo + assert gates
- report/report.md (336 lines) — has placeholder metrics [X]
- proposal/proposal.md (75 lines) — formal proposal, 5% of grade
- 7 ADRs in docs/adrs/
- docs/course-alignment.md — all 10 tasks mapped to lecture weeks
- Git: 2 commits pushed to main

## NOT Done — Next Session Must Do
1. **Execute notebooks sequentially on northprot:**
   ```bash
   source ~/Academia/STAT1100/.venv/bin/activate
   cd ~/Academia/STAT1100/project/stat1100-project04
   jupyter nbconvert --to notebook --execute notebooks/01-eda.ipynb --output 01-eda.ipynb --ExecutePreprocessor.timeout=600
   jupyter nbconvert --to notebook --execute notebooks/02-data-prep.ipynb --output 02-data-prep.ipynb --ExecutePreprocessor.timeout=600
   jupyter nbconvert --to notebook --execute notebooks/03-modeling.ipynb --output 03-modeling.ipynb --ExecutePreprocessor.timeout=600
   ```
   Order matters: 02 creates data/processed/ files that 03 reads.

2. **Fix any execution errors** — notebooks were written without running, expect some bugs

3. **Collect real metrics** from executed notebooks:
   - RMSE (regression), F1/precision/recall (classification)
   - PCA components count, K-Means cluster stats
   - Optimal alarm threshold, Monte Carlo cost estimates

4. **Update report/report.md** — replace all [X] placeholders with real metric values

5. **Write work logs** — docs/work-logs/ (5 files, currently empty):
   - wave-0-setup.md, wave-1-eda.md, wave-1-data-prep.md
   - wave-2-modeling.md, wave-3-report.md

6. **Git commit + push** updated notebooks (with outputs) + report + work logs

## Key Context
- Dataset: NASA CMAPSS FD001, 100 engines, 21 sensors, run-to-failure
- Models: LinearRegression (Week 7) + KNN (Week 6) primary, RF extension
- RUL cap: T=130 (ADR-002), failure horizon: 30 cycles (ADR-005)
- Every code cell has What/Why/Course Reference markdown above it
- Partner: Aedrian (CS major, English native) — work approach not yet decided
- Presentation: 2026-03-31

## Project Path
`~/Academia/STAT1100/project/stat1100-project04`

## Activate Environment
```bash
source ~/Academia/STAT1100/.venv/bin/activate
```
