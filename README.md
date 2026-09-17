# 🏦 Banking Market Prediction: Decision Tree Classifier (B.Y.T.E Task 4)

End-to-end machine learning pipeline analyzing direct marketing campaign data to predict whether a client will subscribe to a term deposit.

---

## 📊 Dataset Overview
- **Source:** [UCI Machine Learning Repository - Bank Marketing](https://archive.ics.uci.edu/ml/datasets/bank+marketing) (`bank-additional-full.csv`)
- **Context:** Direct marketing phone campaigns managed by a Portuguese banking institution.
- **Target Variable (`y`):** Binary classification (`1` = subscribed, `0` = did not subscribe).
- **Dimensions:** 41,188 rows × 21 columns.

---

## ⚙️ Project Workflow

### 1. Data Exploration
- **Initial Inspection:** Evaluated shape, data types, and summary statistics across all 41,188 records and 21 attributes.
- **Correlation Analysis:** Built a numerical correlation heatmap, revealing strong positive relationships among macroeconomic indicators (`euribor_3m`, `number_employed`, `employment_variation_rate`).

### 2. Data Cleaning
- **Standardization:** Converted column identifiers to clean `snake_case` (e.g., `emp.var.rate` ➔ `employment_variation_rate`).
- **Outlier Handling:** Flagged extreme distribution outliers in `duration` and filtered feature range to the 10th–90th percentiles.
- **Deduplication:** Identified and removed duplicate record rows.
- **Target Encoding:** Mapped string labels (`'yes'`/`'no'`) to binary targets (`1`/`0`).
- **Missing Value Management:** Converted `'unknown'` string tokens to standard `NaN` and dropped incomplete rows.

### 3. Training & Hyperparameter Tuning
- **Leakage Prevention:** Dropped the `duration` feature from predictors (known strictly post-call completion).
- **Data Splitting:** Applied an 80/20 train-validation split for unbiased evaluation.
- **Baseline Establishment:** Recorded ~90.23% baseline accuracy via majority-class naive prediction (`0` / No).
- **Pipeline Optimization:** Built an `OrdinalEncoder` + `DecisionTreeClassifier` pipeline. Iterated `max_depth` (1–15) to evaluate bias-variance trade-offs, locking in `max_depth = 4` to mitigate overfitting.

---

## 📈 Model Evaluation Metrics (`max_depth = 4`)

| Metric | Score / Performance | Interpretation |
| :--- | :--- | :--- |
| **Training Accuracy** | 97.00% | High model fit on training partition |
| **Testing Accuracy** | 89.00% | Generalization benchmark (vs. 90.23% baseline) |
| **Precision** | 0.47 | ~47% of predicted subscriptions were actual hits |
| **Recall** | 0.40 | Captured ~40% of all true positive subscriptions |

> **Confusion Matrix Insight:** Explicitly captures classification trade-offs under severe class imbalance.

---

## 💡 Feature Importance & Key Insights

### Top 5 Predictive Drivers
1. **`number_employed`** (Quarterly indicator of employment level)
2. **`consumer_confidence_index`** (Monthly indicator of consumer sentiment)
3. **`previous_outcome`** (Outcome of the previous marketing campaign)
4. **`month`** (Last contact month of the year)
5. **`euribor_3m`** (3 month rate euro interbank offered rate)

### Core Strategic Takeaways
* **Macro > Micro:** Macroeconomic indicators dictate subscription likelihood significantly more than personal demographics (age, job, marital status).
* **Economic Climate Correlation:** Tight linkage between labor force metrics (`number_employed`) and customer conversion willingness.
* **Behavioral Inertia:** Prior positive interaction (`previous_outcome`) acts as a massive multiplier for repeat conversions.
