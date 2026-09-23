# Bankmarketing_project
## 📋 Project Description

This project applies end-to-end data science methodology to a **bank marketing dataset** containing **210 customer records** with **7 financial behaviour features**. The primary goal is to understand customer payment patterns and predict the **probability of full payment** — a key metric for banking risk and marketing strategy.
# 📂 Dataset

**Source:** [Kaggle — House Price Regression Dataset (bank_marketing_part1_Data.csv)](https://www.kaggle.com/)  
**File:** `bank_marketing_part1_Data.csv`  
**Rows:** 210 | **Columns:** 7 | **Missing values:** None

| Column | Type | Description |
|--------|------|-------------|
| `spending` | float | Total customer spending |
| `advance_payments` | float | Advance payments made |
| `probability_of_full_payment` | float | **TARGET** — full payment likelihood (0–1) |
| `current_balance` | float | Current account balance |
| `credit_limit` | float | Assigned credit limit |
| `min_payment_amt` | float | Minimum payment amount |
| `max_spent_in_single_shopping` | float | Max single-transaction spend |

---

## 🔬 Methods & Techniques

### Exploratory Data Analysis
- Histograms with mean/median overlays for all features
- Box plots for outlier detection
- Pearson correlation heatmap (lower-triangle)
- Pairplots (KDE diagonal) for key feature relationships
- Scatter plots with regression lines to the target variable
- Quartile-based analysis of spending vs payment probability

### Feature Engineering (5 new features)
```
spend_to_credit_ratio  = spending / credit_limit
payment_efficiency     = advance_payments / spending
balance_utilisation    = current_balance / credit_limit
min_payment_ratio      = min_payment_amt / spending
max_spend_ratio        = max_spent_in_single_shopping / spending
```

### Customer Segmentation
- **Algorithm:** K-Means (StandardScaler normalised)
- **k selection:** Elbow (WCSS) + Silhouette Score (k=2..8)
- **Visualisation:** PCA 2D projection + Radar (spider) chart

### Regression Models (10 total)
Linear Regression · Ridge · Lasso · ElasticNet · Decision Tree ·  
Random Forest · Gradient Boosting · Extra Trees · KNN (k=7) · SVR (RBF)

### Best Model
All models achieve **R² > 0.97**. Linear/regularised models top CV leaderboard (~0.99).  
`GradientBoostingRegressor` tuned with GridSearchCV achieves **R² > 0.99** on the test set.

---

## 🛠️ Technologies Used

| Category | Library / Tool | Version |
|----------|---------------|---------|
| Language | Python | 3.11+ |
| Data | pandas, numpy | ≥2.0, ≥1.24 |
| Stats | scipy | ≥1.11 |
| ML | scikit-learn, joblib | ≥1.3, ≥1.3 |
| Visualisation | matplotlib, seaborn | ≥3.7, ≥0.12 |
| Notebook | JupyterLab | ≥4.0 |

---

## 🚀 Setup Instructions

### 1. Clone / download the project
```bash
git clone <your-repo-url>
cd bank_marketing_project
```

### 2. (Recommended) Create a virtual environment
```bash
python3 -m venv venv
source venv/bin/activate        # macOS / Linux
# venv\Scripts\activate         # Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Add the dataset
Place `bank_marketing_part1_Data.csv` in the project root (same folder as the notebook).

### 5. Launch JupyterLab
```bash
jupyter lab
```

### 6. Run the notebook
Open **`Poornima_bankmarketing.ipynb`** → **Kernel → Restart & Run All**

---

## 📊 Output Files

After running the notebook, the following files are generated:

| File | Description |
|------|-------------|
| `bank_marketing_engineered.csv` | Dataset with engineered features and cluster labels |
| `best_model.pkl` | Serialised best model pipeline (joblib) |
| `plots_distributions.png` | Distribution histograms for all 7 features |
| `plots_boxplots.png` | Box plots for outlier detection |
| `plots_correlation.png` | Pearson correlation heatmap |
| `plots_pairplot.png` | Pairplot of key features |
| `plots_scatter.png` | Scatter plots vs target |
| `plots_quartile_analysis.png` | Spending / credit by payment probability quartile |
| `plots_feature_correlation.png` | Feature correlation with target (bar chart) |
| `plots_elbow.png` | Elbow + silhouette charts for optimal k |
| `plots_clusters_pca.png` | PCA 2D cluster visualisation |
| `plots_radar.png` | Radar chart of cluster profiles |
| `plots_model_comparison.png` | R² and MAE comparison across all 10 models |
| `plots_actual_vs_predicted.png` | Actual vs predicted + residual distribution |
| `plots_feature_importance.png` | Feature importances / coefficients |

---

## 📁 Project Structure

```
bank_marketing_project/
├── Poornima_bankmarketing.ipynb      ← Main notebook
├── bank_marketing_part1_Data.csv     ← Input dataset
├── requirements.txt                  ← Python dependencies
├── README.md                         ← This file
├── Poornima_ProjectReport.docx       ← Full project report
│
│   ── Generated after running notebook ──
├── bank_marketing_engineered.csv
├── best_model.pkl
└── plots_*.png                       ← All visualisation outputs
```

---

## 🔑 Key Findings

- **Spending, advance_payments, credit_limit, current_balance** are nearly perfectly correlated (r > 0.97) — they all measure the same underlying financial activity.
- **payment_efficiency** (advance payments / spending) is the most informative engineered feature.
- The target variable is **highly predictable (R² > 0.99)** — payment probability is largely determined by a customer's spending and credit profile.
- **Cluster analysis** reveals distinct high-value vs low-value customer segments, directly actionable for targeted marketing campaigns.
- **min_payment_amt** is the most independent feature — possibly a bank-assigned threshold rather than organic customer behaviour.

---

## 📄 Report

A full written project report is available in **[`Poornima_ProjectReport.docx`](Poornima_ProjectReport.docx)**, covering all sections from executive summary through conclusions and recommendations.

---

*Built with Python · scikit-learn · pandas · matplotlib · seaborn · JupyterLab*
