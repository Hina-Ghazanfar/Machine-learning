# ML Regression — End‑to‑End Predictive Modeling

![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-blue)
![Python](https://img.shields.io/badge/Python-3.8%2B-green)
![scikit--learn](https://img.shields.io/badge/scikit--learn-1.x-orange)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

This repository contains a single notebook, **`ML_Regression.ipynb`**, that walks through a practical regression workflow:
- **EDA & Visualization:** distributions, scatter plots, box plots, correlation heatmap, pair plots.
- **Preprocessing:** train/validation split, scaling (`StandardScaler`).
- **Modeling:** `LinearRegression`, `Ridge`, `DecisionTreeRegressor`, `RandomForestRegressor`.
- **Model Selection:** cross‑validation and **`GridSearchCV`** hyperparameter tuning.
- **Feature Selection:** backward feature selection (notebook section).
- **Evaluation:** `R²`, `MAE`, `MSE` and comparative plots.

The example uses a local Excel dataset **`2022QUB.xlsx`** (not included) for demonstration. You can swap in your own dataset by updating the data‑loading cell.

---

## Repository Structure

```
.
├── ML_Regression.ipynb
├── data/
│   └── 2022QUB.xlsx           # <-- Place your dataset here
├── requirements.txt
└── README.md
```

> **Note:** The `data/` folder is ignored by Git to prevent committing private datasets.

---

## Getting Started

### 1) Clone and create a virtual environment
```bash
git clone <YOUR_REPO_URL>.git
cd <YOUR_REPO_NAME>

python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows (PowerShell)
# .venv\Scripts\Activate.ps1

pip install -r requirements.txt
```

### 2) Add the dataset
Place your Excel file at:
```
data/2022QUB.xlsx
```
If your file has a different name or location, update the path in the notebook's data‑loading cell.

### 3) Launch Jupyter
```bash
jupyter lab
# or
jupyter notebook
```
Open **`ML_Regression.ipynb`** and run all cells in order (Kernel → Restart & Run All).

---

## What the Notebook Covers

### Exploratory Data Analysis (EDA)
- Missing value checks and basic summary statistics
- Histograms/distributions and box plots
- Scatter plots to inspect relationships
- **Correlation heatmap** and **pair plots**

### Preprocessing
- Train/validation split via `train_test_split`
- Feature scaling with `StandardScaler` (where appropriate)

### Modeling & Selection
- Baseline **Linear Regression**
- Regularized **Ridge Regression**
- **Decision Tree Regressor** for non‑linear patterns
- **Random Forest Regressor** for robust performance
- Cross‑validation via `cross_val_score`
- Hyperparameter tuning using **`GridSearchCV`**
- Backward feature selection (greedy removal with re‑fit/evaluate)

### Evaluation
- **R²**, **MSE**, **MAE** with comparison across models
- Optional visual diagnostics (pred vs. actual, residuals, feature importances for tree‑based models)

---

## Reproducibility

Results depend on the random split and model seeds. Set `random_state` consistently in:
- `train_test_split(random_state=...)`
- Any model that accepts a seed (e.g., `RandomForestRegressor(random_state=...)`)
- `GridSearchCV(..., cv=K, n_jobs=-1)` for deterministic CV (subject to BLAS threading)

> Consider exporting key metrics to a CSV to track experiments over time.

---

## Adapting to Your Data

- **Target column:** Update the notebook’s `y = df["<target>"]` line to match your dataset.
- **Categorical features:** If present, insert encoding (e.g., `OneHotEncoder` in a `ColumnTransformer`).
- **Pipelines:** Wrap scaler + model in a `Pipeline` to avoid leakage during CV.
- **Model extensions:** Try `ElasticNet`, `GradientBoostingRegressor`, or `XGBRegressor` for stronger baselines.

---

## Requirements

All required packages are listed in `requirements.txt`. Install with:

```bash
pip install -r requirements.txt
```

Key libraries used in the notebook:
- `pandas`, `numpy`
- `matplotlib`, `seaborn`
- `scikit-learn`
- `openpyxl` (Excel reader engine used by pandas)
- `jupyter`

---

## License

Add your chosen license file (MIT/Apache‑2.0/BSD‑3‑Clause) and reflect it here.

## Acknowledgements

- scikit‑learn, pandas, numpy, matplotlib, and seaborn communities.
- Any data provider relevant to your dataset.

---

**Maintainer tips**  
Clear notebook outputs before committing to keep diffs small (`jupyter nbconvert --ClearOutputPreprocessor.enabled=True --inplace ML_Regression.ipynb`). Consider pinning versions in `requirements.txt` for stable builds.
