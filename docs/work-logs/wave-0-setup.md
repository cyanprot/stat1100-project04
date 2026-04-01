# Wave 0: Environment Setup

**Date:** 2026-03-14
**Duration:** ~30 minutes

## What Was Done
- Created project directory on development server: `~/Academia/STAT1100/project/stat1100-project04`
- Cloned repo from `github.com/cyanprot/stat1100-project04`
- Configured git (user: Jongmin Lee, email: cyan@northprot.com)
- Created Python venv at `~/Academia/STAT1100/.venv`
- Installed packages: pandas 3.0.1, numpy 2.4.3, scikit-learn 1.8.0, matplotlib 3.10, seaborn 0.13, jupyterlab, ipykernel
- Registered Jupyter kernel: `stat1100`
- Downloaded CMAPSS dataset from NASA (286KB zip → extracted FD001-FD004)

## Key Outputs
- venv functional: `python -c "import sklearn, pandas, numpy"` passes
- CMAPSS data: `data/CMAPSSData/train_FD001.txt` (3.5MB, 20,631 rows)
- Jupyter kernel registered: `stat1100`

## Issues
- Initial notebook paths used `data/CMAPSSData` (project-root relative) instead of `../data/CMAPSSData` (notebook-relative). Fixed by updating DATA_DIR in 01-eda and 02-data-prep.
