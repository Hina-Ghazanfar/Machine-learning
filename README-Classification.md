# ML Classification — End‑to‑End Supervised Pipeline

![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-blue)
![Python](https://img.shields.io/badge/Python-3.8%2B-green)
![scikit--learn](https://img.shields.io/badge/scikit--learn-1.x-orange)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

This repository contains **`ML_Classification.ipynb`**, a concise, production‑style workflow for binary/multi‑class **classification** with scikit‑learn. It covers:

- **EDA & Visualization:** summary checks, scatter plots, correlation heatmap
- **Preprocessing:** stratified train/validation split, scaling (`StandardScaler` / `MinMaxScaler`), label encoding
- **Models:** `LogisticRegression`, `SVC`, `DecisionTreeClassifier`, `RandomForestClassifier`
- **Model Selection:** cross‑validation with `StratifiedKFold`, hyperparameter tuning via **`GridSearchCV`**
- **Feature Selection:** backward/iterative selection (section in the notebook)
- **Evaluation:** accuracy, ROC‑AUC, ROC curve, precision‑recall curve, confusion matrix & `classification_report`

The example reads a local Excel dataset **`2022QUB.xlsx`** (not included). You can plug in your own dataset by adjusting the data‑loading cell.

---

## Repository Structure

```
.
├── ML_Classification.ipynb
├── data/
│   └── 2022QUB.xlsx           # <-- Place your dataset here
├── requirements.txt
├── .gitignore
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
If your file uses a different name or path, update the data‑loading cell in the notebook accordingly.

### 3) Launch Jupyter
```bash
jupyter lab
# or
jupyter notebook
```
Open **`ML_Classification.ipynb`** and run the cells sequentially (Kernel → Restart & Run All).

---

## Notebook Outline

- **Data Preprocessing**
  - Missing value checks, basic cleaning
  - Encoding labels (`LabelEncoder` where relevant)
  - Scaling features with `StandardScaler` / `MinMaxScaler` (as appropriate)
  - Stratified split using `train_test_split` and/or `StratifiedKFold`

- **Feature Engineering**
  - Derived features and selection (backward stepwise shown)

- **Checking Features by Plotting**
  - Scatter plots and correlation heatmap to inspect relationships

- **Modeling & Tuning**
  - Baselines: `LogisticRegression`, `SVC`
  - Tree‑based: `DecisionTreeClassifier`, `RandomForestClassifier`
  - `cross_val_score` and **`GridSearchCV`** for hyperparameter search

- **Evaluation**
  - Metrics: `accuracy_score`, **ROC‑AUC**
  - Plots: **ROC curve**, **Precision‑Recall curve**
  - **Confusion matrix** and `classification_report`

> The notebook is written to make it easy to swap models, adjust hyperparameter grids, and iterate quickly.

---

## Reproducibility

- Fix `random_state` in `train_test_split`, CV splitters (`StratifiedKFold`), and any stochastic models (e.g., `RandomForestClassifier(random_state=...)`).
- Keep feature scaling **inside** a `Pipeline` (e.g., `make_pipeline(StandardScaler(), SVC(...))`) during CV to avoid data leakage.
- Optionally export metrics to CSV to track experiments over time.

---

## Adapting to Your Data

- **Target column:** Update `y = df["<target>"]` to match your dataset.
- **Categoricals:** If you have categorical features, consider a `ColumnTransformer` with `OneHotEncoder`.
- **Imbalance:** For imbalanced classes, consider `class_weight='balanced'` or `imblearn` methods (SMOTE), and use **PR‑AUC** in addition to ROC‑AUC.
- **Model Extensions:** Add `GradientBoostingClassifier`, `XGBClassifier`, or `CalibratedClassifierCV` for probability calibration if needed.

---

## Requirements

Install with:
```bash
pip install -r requirements.txt
```

Key libraries used by the notebook:
- `pandas`, `numpy`
- `matplotlib`, `seaborn`
- `scikit-learn`
- `scipy`
- `openpyxl` (Excel reader engine for pandas)
- `jupyter`

---

## License

Add a license file (MIT/Apache‑2.0/BSD‑3‑Clause) and reflect the choice here.

## Acknowledgements

- scikit‑learn, pandas, numpy, matplotlib, and seaborn communities.
- Any data provider relevant to your use case.

---

**Maintainer tips**  
Clear notebook outputs before commit to keep diffs small:
```bash
jupyter nbconvert --ClearOutputPreprocessor.enabled=True --inplace ML_Classification.ipynb
```
Pin versions in `requirements.txt` for stable builds.