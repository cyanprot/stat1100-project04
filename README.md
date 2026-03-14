# Project 04 — Predictive Maintenance for Industrial Equipment

**STAT 1100 · Langara College · Spring 2026**
**Last updated:** 2026-03-14

---

## 1. Project Overview

A manufacturing company experiences costly unplanned equipment failures that halt production. Our goal is to build a predictive maintenance system that shifts from scheduled maintenance to **condition-based intervention** — predicting when an engine will fail before it actually does.

### Dataset: NASA CMAPSS

We're using the **NASA Turbofan Engine Degradation Simulation Dataset (CMAPSS)**:

- ~20,000 rows across 100 engine units
- Each engine runs from healthy to failure (run-to-failure time series)
- 21 sensor readings + 3 operating condition settings per time step
- Our job: predict **Remaining Useful Life (RUL)** — how many cycles until failure

This dataset is publicly available and widely used in predictive maintenance research. It maps perfectly to all 10 required project tasks.

---

## 2. Team

| | Jongmin | Aedrian |
|---|---|---|
| **Strengths** | Python, data science workflow, AI tooling | Computer Science, English (native), presentation |
| **Program** | Bioinformatics | Computer Science |
| **Contact** | WhatsApp (existing chat) | WhatsApp (existing chat) |

---

## 3. Deliverables & Grading

### What we submit

| Deliverable | Weight | Description |
|---|---|---|
| **Written Report** | 30% | Windowing strategy, RUL label design, sensor normalisation decisions, model justifications |
| **Notebook** | 50% | End-to-end reproducible pipeline: raw data → final model predictions |
| **Presentation** | 20% | Translate model findings into maintenance intervention recommendations for plant management |

### How the Group Project grade breaks down (20% of course total)

| Component | Weight | What it means |
|---|---|---|
| Proposal | 5% | Project selection + initial plan |
| Team Work | 10% | Ongoing collaboration evidence |
| Peer Review | 5% | Each member evaluates the other's contribution |
| Final Report | 10% | Quality of final deliverables |

> **Note on Peer Review:** The instructor expects contributions to be balanced across all areas. We should both be involved in every phase — not just "one person codes, one person writes."

---

## 4. Work Approach — Let's Discuss

Here are three approaches we can take. Each has trade-offs. **Let's pick the one that works best for both of us**, or mix and match.

### Option A: Sprint & Review

One person builds the core notebook first, then the other reviews and writes the report.

```
Week 1 (Mar 14-17): Person 1 builds notebook (Data Prep + Modeling)
Week 1 (Mar 17-21): Person 2 writes report based on notebook, Person 1 reviews
Week 2 (Mar 22-30): Both work on presentation
Mar 31: Present
```

- **Pro:** Fast. Uses each person's strongest skills efficiently.
- **Con:** Less balanced. Risk of one person doing most of the coding.

### Option B: Parallel Tracks

Split by deliverable from the start and work simultaneously.

```
Person 1: Notebook (Data Prep + Model Building) — owns the .ipynb
Person 2: Report (research + justification) + Presentation — owns the .md/.slides
Daily sync on WhatsApp
```

- **Pro:** No blocking. Clear ownership.
- **Con:** Less overlap in skills. Peer review might flag uneven coding contribution.

### Option C: Teach & Build (Pair Programming)

Work on everything together in real-time. One person codes, the other writes justification in the same notebook.

```
Daily 1-2 hour Colab sessions together
Coder: writes Python cells
Writer: writes markdown cells explaining decisions
Both commit to GitHub
```

- **Pro:** Most balanced. Both learn everything. Peer review safe.
- **Con:** Requires synced schedules. Slower overall.

### Our recommendation

**A hybrid approach** will probably work best:
1. Start together (Option C style) for the first session to align on the dataset and approach
2. Then split into focused tracks (Option A/B) for speed
3. Regroup for review before submission

**What do you think? Open to other ideas too.**

---

## 5. Timeline

### Phase 1: Core Work (Mar 14–21)

Goal: Finish notebook + report draft before midterms.

| Date | Milestone | Who |
|---|---|---|
| **Mar 14 (Sat)** | Download CMAPSS dataset, initial EDA, understand data structure | Both |
| **Mar 15 (Sun)** | Data Prep tasks 1-3: windowing, feature engineering, RUL labels | TBD |
| **Mar 16 (Mon)** | Data Prep tasks 4-5: normalisation, train/test split | TBD |
| **Mar 17 (Tue)** | Model Building tasks 1-2: regression + classification baselines | TBD |
| **Mar 18 (Wed)** | Model Building tasks 3-5: advanced model, sensor importance, alarm threshold | TBD |
| **Mar 19 (Thu)** | Report draft — all justifications written | TBD |
| **Mar 20 (Fri)** | Review + polish notebook and report | Both |
| **Mar 21 (Sat)** | Final check, submit if needed | Both |

### Phase 2: Presentation (Mar 22–30)

| Date | Milestone | Who |
|---|---|---|
| **Mar 22-25** | Midterms / break | — |
| **Mar 26-29** | Build presentation slides (Google Slides) | Both |
| **Mar 30** | Rehearse | Both |
| **Mar 31** | Present | Both |

> **TBD** = we'll assign based on the approach we choose together.

---

## 6. Task Breakdown

These are the 10 required tasks from the project spec. Every task needs to be completed.

### Data Preparation (5 tasks)

| # | Task | What we need to do | Difficulty |
|---|---|---|---|
| 1 | **Time-series windowing** | Segment each engine's sensor history into fixed-length windows for model input | Medium |
| 2 | **Sensor feature engineering** | Create rolling statistics (mean, std, slope) from raw sensor readings | Medium |
| 3 | **RUL label construction** | Calculate remaining cycles until failure for each time step; decide on piecewise-linear vs raw RUL | Medium |
| 4 | **Normalisation across operating conditions** | Sensors behave differently under different operating regimes; normalise within each regime | Easy-Medium |
| 5 | **Train/test split by engine unit** | Split by engine ID (not by row) to prevent data leakage | Easy |

### Model Building (5 tasks)

| # | Task | What we need to do | Difficulty |
|---|---|---|---|
| 1 | **Regression model for RUL** | Predict remaining useful life as a continuous value (e.g., Random Forest, Linear Regression) | Medium |
| 2 | **Classification model for failure horizon** | Binary classification: will this engine fail within N cycles? | Medium |
| 3 | **Sequence model (optional advanced)** | LSTM or similar for time-series — bonus points but not required | Hard (optional) |
| 4 | **Sensor importance analysis** | SHAP values or feature importance to identify which sensors matter most | Easy-Medium |
| 5 | **Alarm threshold analysis** | At what predicted RUL should we trigger a maintenance alert? Cost-benefit analysis | Medium |

---

## 7. Collaboration Setup

### GitHub Repository

We'll use a GitHub repo for version control. Here's how to get started:

**1. Clone the repo** (after you've been added as a collaborator):
```bash
git clone https://github.com/<repo-url>
cd stat1100-project04
```

**2. Create a branch for your work:**
```bash
git checkout -b aedrian/report-draft
```

**3. Commit and push:**
```bash
git add .
git commit -m "Add report section on windowing strategy"
git push origin aedrian/report-draft
```

**4. Create a Pull Request** on GitHub to merge into `main`.

> Don't worry if this is new — Week 11 covers Git in class, and we can walk through it together.

### Google Colab

This is where we'll run our Python notebooks. No setup needed — just a Google account.

1. Go to [colab.research.google.com](https://colab.research.google.com)
2. File → Open notebook → GitHub tab → paste our repo URL
3. Edit and run cells in your browser
4. File → Save a copy in GitHub → commit back to the repo

### Google Slides

For the presentation. We'll create a shared slide deck closer to Mar 26.

### Repo Structure (planned)

```
stat1100-project04/
├── README.md              ← this plan
├── data/
│   └── CMAPSSData/        ← raw dataset files
├── notebooks/
│   ├── 01-eda.ipynb       ← exploratory data analysis
│   ├── 02-data-prep.ipynb ← all 5 data preparation tasks
│   └── 03-modeling.ipynb  ← all 5 model building tasks
├── report/
│   └── report.md          ← written report (or Google Docs link)
└── presentation/
    └── slides-link.md     ← link to Google Slides
```

---

## 8. Getting Started (Day 1 Checklist)

- [ ] Both: Accept GitHub repo invite
- [ ] Both: Open the repo in Google Colab, verify it runs
- [ ] Both: Download CMAPSS dataset and upload to `data/`
- [ ] Both: Run `01-eda.ipynb` together — look at the data, discuss first impressions
- [ ] Decide: Which work approach (A / B / C / hybrid) do we want?
- [ ] Decide: Who takes which tasks for Day 2?

---

## 9. Assessment Criteria (from project spec)

Keep these in mind throughout — this is what we're graded on:

1. **Data Preparation Quality** — correctness of each step; justify every decision; prevent data leakage
2. **Model Building Rigour** — appropriate algorithm selection; proper train/val/test discipline; hyperparameter tuning; business-suited metrics
3. **Interpretability & Explainability** — SHAP values or feature importance; connect model output to business insights
4. **Evaluation Depth** — go beyond accuracy; cost-sensitive analysis, calibration where appropriate
5. **Communication Quality** — clear report; reproducible notebook; non-technical presentation

---

*Let's build something good. Questions, ideas, or concerns — drop them in the chat anytime.*
