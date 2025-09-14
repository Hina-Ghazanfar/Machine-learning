# ML Clustering — Unsupervised Learning Pipeline

![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-blue)
![Python](https://img.shields.io/badge/Python-3.8%2B-green)
![scikit--learn](https://img.shields.io/badge/scikit--learn-1.x-orange)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

This repository provides **`ML_Clustering.ipynb`**, a practical, end-to-end **unsupervised learning** workflow for exploratory clustering. It focuses on building intuition around cluster structure and validating it quantitatively.

**What it includes**
- **EDA & Preprocessing:** basic inspection, `StandardScaler` for feature scaling
- **Dimensionality Reduction:** **PCA** for visualization in 2D
- **Clustering:** **KMeans** with
  - **Elbow method** (`inertia_`) to suggest *k*
  - **Silhouette analysis** (`silhouette_score`) to assess cluster separation
- **Hierarchical Analysis:** **dendrogram** using `scipy.cluster.hierarchy` (`linkage`, `dendrogram`)
- **Visualization:** scatter plots (PCA components), heatmaps/cluster trends

> The notebook reads a local Excel dataset **`2022QUB.xlsx`** (not included). Replace it with your data by updating the data-loading cell.

---

## Repository Structure

```
.
├── ML_Clustering.ipynb
├── data/
│   └── 2022QUB.xlsx           # <-- Place your dataset here
├── requirements.txt
├── .gitignore
└── README.md
```

> **Note:** The `data/` folder is Git-ignored to keep private datasets out of the repo.

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
If your file name/path differs, update the data-loading cell in the notebook.

### 3) Launch Jupyter
```bash
jupyter lab
# or
jupyter notebook
```
Open **`ML_Clustering.ipynb`** and run cells top-to-bottom (Kernel → Restart & Run All).

---

## Notebook Outline

### 1. Data Preparation
- Inspect schema and missing values
- **Scale** numerical features with `StandardScaler`

### 2. Dimensionality Reduction
- **PCA** to 2 principal components for plotting
- Optional variance explained ratio to justify dimensionality

### 3. Clustering
- **KMeans**
  - Choose *k* with **elbow method**
  - Validate clusters with **silhouette score**
- Assign labels and analyze cluster profiles (group means/medians)

### 4. Hierarchical Clustering (Diagnostics)
- Compute **linkage** (e.g., "ward", "complete")
- Plot **dendrogram** to inspect hierarchical structure

### 5. Visualization
- 2D PCA scatter colored by cluster label
- Heatmaps/boxplots as needed to compare clusters

---

## Reproducibility

- Set `random_state` for KMeans to make runs deterministic:
  ```python
  kmeans = KMeans(n_clusters=k, random_state=42)
  ```
- Keep scaling inside a `Pipeline` if you extend to multiple methods.

---

## Adapting to Your Data

- **Feature selection:** Remove non-informative columns, standardize units.
- **Categoricals:** Consider encoding before scaling/Clustering.
- **Alternative algorithms:** Try `DBSCAN` (density-based), `AgglomerativeClustering` (hierarchical), or `GaussianMixture` (model-based) depending on data shape and noise.
- **Validation:** Compare **silhouette**, **Calinski–Harabasz**, and **Davies–Bouldin** for a fuller picture.

---

## Requirements

Install with:
```bash
pip install -r requirements.txt
```

Key packages used:
- `pandas`, `numpy`
- `matplotlib`, `seaborn`
- `scikit-learn`
- `scipy`
- `openpyxl` (Excel support for pandas)
- `jupyter`

---

## License

Add your preferred license (MIT/Apache-2.0/BSD-3-Clause) and include a `LICENSE` file.

## Acknowledgements

- scikit-learn, pandas, numpy, matplotlib, seaborn
- SciPy community for hierarchical clustering utilities

---

**Maintainer tips**  
Clear outputs before committing:
```bash
jupyter nbconvert --ClearOutputPreprocessor.enabled=True --inplace ML_Clustering.ipynb
```
Pin exact versions in `requirements.txt` for stable builds.
