Got it — here’s a **short, clean `README.md`** that matches your notebook + report, without being too long. Copy-paste this into `README.md` in the repo.

````markdown
# Machine Learning Assignment — FARS Classification & Growth-Curve Regression

This repository contains two mini-projects implemented in a single Jupyter notebook (`Machine_Learning.ipynb`):

1. **Mini-Project 1 (Classification):** Tabular classification on FARS-style data, comparing multiple pipelines with cross-validated tuning.
2. **Mini-Project 2 (Regression):** Predicting bacterial growth-curve parameters (`a`, `mu`, `tau`, `a0`) from experimental conditions using tuned regression pipelines.

---

## Contents

- `Machine_Learning.ipynb` — main notebook (run this)
- `classification-dataset.csv` — classification dataset (required to run MP1)
- `fitting-results.csv` — regression dataset (required to run MP2)

---

## Methods (high-level)

### Classification (Mini-Project 1)
- Preprocessing: numeric feature scaling inside a **scikit-learn Pipeline** (leakage-safe)
- Split: **60/20/20** train/val/test with stratification
- Tuning: **5-fold Stratified CV**
- Models compared:
  - Logistic Regression
  - SVC (RBF) (calibrated probabilities)
  - Random Forest
  - Gradient Boosting (+ SelectK feature selection)
- Key metrics: **Macro F1** + **Balanced Accuracy** (imbalance-aware)

**Best overall (by Macro F1):** Gradient Boosting + SelectK  
**Strong alternative (best Balanced Accuracy):** Random Forest

### Regression (Mini-Project 2)
- Task: predict `a`, `mu`, `tau`, `a0` **separately** from experimental features (no leakage: targets excluded from features)
- Split: **60/20/20** train/val/test (shared indices across targets)
- Tuning: **5-fold CV** with `RandomizedSearchCV` (RMSE optimised)
- Models compared per target:
  - Ridge
  - SVR (RBF)
  - Random Forest
  - Gradient Boosting
- Metrics: MAE, RMSE, R²

**Best models found:**
- `a`, `mu`: Gradient Boosting
- `tau`, `a0`: Random Forest

---

## How to run

### Option A — Local
```bash
git clone https://github.com/rianeps/Machine-Learning-Assignment.git
cd Machine-Learning-Assignment
python -m venv .venv
````

Activate:

* macOS/Linux:

```bash
source .venv/bin/activate
```

* Windows (PowerShell):

```powershell
.venv\Scripts\Activate.ps1
```

Install basics:

```bash
pip install jupyter numpy pandas matplotlib scikit-learn imbalanced-learn plotly
```

Launch:

```bash
jupyter notebook
```

Open `Machine_Learning.ipynb` and run cells top-to-bottom.

### Option B — Colab

Upload `Machine_Learning.ipynb` (and the CSV files if needed) and run all cells.

---

## Notes

* Results depend slightly on randomness unless seeds are fixed (the notebook uses `random_state=42` for splits/tuning where applicable).
* All preprocessing is performed inside pipelines to avoid data leakage.

---

## Author

Nepoliyan Ria



