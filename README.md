# 📊 Credit Card Customer Segmentation Analysis

## 🎯 Project Overview & Business Problem

In the credit card industry, adopting a one-size-fits-all strategy leads to sub-optimal customer engagement and increased financial risk. Customer segmentation enables financial institutions to group cardholders into distinct segments based on transaction history, purchasing patterns, payment behaviors, and credit utilization.

This project delivers an end-to-end unsupervised machine learning framework to segment credit card holders. Using **K-Means Clustering** and **Agglomerative Hierarchical Clustering**, the analysis discovers underlying customer behaviors, provides actionable business strategies, and offers clear recommendations for real-world deployment.

---

## 📂 Repository Structure

```
├── data/
│   └── DataSet(W4).csv.xls          # Credit card customer dataset
├── notebooks/
│   └── week4_clustering.ipynb       # Jupyter notebook with code, outputs & visuals
├── README.md                        # Project documentation & summary
└── requirements.txt                 # Required Python packages
```

---

## 🔍 Detailed Data Description

The analysis uses customer behavioral data tracking credit card activity. Key features analyzed include:

| Feature | Description |
|---|---|
| `BALANCE` | Total account balance amount remaining to be paid by the customer |
| `PURCHASES` | Total dollar value of all purchases made by the account |
| `ONEOFF_PURCHASES` | Maximum purchase amount done in a single transaction |
| `INSTALLMENTS_PURCHASES` | Total value of purchases made in installment payments |
| `CASH_ADVANCE` | Total cash advance drawn by the user |
| `PURCHASES_FREQUENCY` | How frequently purchases are being made (0 to 1) |
| `CASH_ADVANCE_FREQUENCY` | How frequently cash in advance is drawn |
| `CREDIT_LIMIT` | Limit of credit card available for the user |
| `PAYMENTS` | Total amount of payments made by the user |
| `MINIMUM_PAYMENTS` | Minimum amount of payment made by the user |
| `PRC_FULL_PAYMENT` | Percent of full payment paid by the user |

---

## 🛠️ Project Methodology & Workflow

### 1. Data Preprocessing & EDA
- Imputed missing values in `CREDIT_LIMIT` and `MINIMUM_PAYMENTS` using median values to preserve data integrity.
- Scaled all numerical features using `StandardScaler` to prepare for distance-based clustering algorithms.

### 2. Part 1 — K-Means Clustering
- Determined the optimal number of clusters (**k = 3**) using the Elbow Method (WCSS) and validated cluster cohesion via Silhouette Scores.
- Analyzed cluster characteristics using feature mean profiles, relative percentage comparisons, and correlation heatmaps to define distinct customer personas.

### 3. Part 2 — Hierarchical Clustering
- Sampled 300 observations to compute hierarchical linkage matrices using Ward's minimum variance method.
- Constructed a clear dendrogram with a horizontal cut threshold line to confirm the 3-cluster structure.
- Applied `AgglomerativeClustering` (k = 3) and evaluated structural alignment with K-Means using cross-tabulation (`pd.crosstab`).

---

## 💡 Key Customer Segments & Business Strategies

### Cluster 0 — Low-Engagement Transactors
Low balance, minimal purchase activity, low card usage frequency.
**Strategy:** Target with cash-back incentives, promotional offers, and engagement campaigns to boost card utilization.

### Cluster 1 — VIP / High-Spenders
High credit limits, heavy purchases (one-off & installments), consistent payments.
**Strategy:** Retain with premium rewards, travel perks, credit limit increases, and exclusive VIP card upgrades.

### Cluster 2 — Cash Advance / High-Risk
High balance reliance, low purchase activity, very high cash advance frequency.
**Strategy:** Enforce stricter risk parameters, offer structured balance transfer plans, and monitor for potential default risk.

---

## 🔬 Model Comparison & Recommendations

- **Structural Agreement:** The cross-tabulation matrix demonstrates high alignment between K-Means and Hierarchical Clustering, particularly in separating VIP High-Spenders and Cash Advance Heavy users.
- **Algorithm Choice:** K-Means Clustering is recommended for real-world production deployment.
- **Business Justification:**
  - **Scalability:** K-Means operates efficiently at O(N) computational complexity, effortlessly scaling to millions of banking records.
  - **Production Inference:** Allows marketing and risk systems to instantly map new customer accounts to existing centroids via `.predict()` without re-fitting the dataset.
