# 📞 Telecom Churn Prediction with Random Forest

This project demonstrates how to predict **telecom churn** using a **Random Forest** classifier. The tutorial covers data preprocessing (handling missing values, encoding, scaling), hyperparameter tuning, model evaluation, and advanced visualizations for interpretability. 

---

## 🎯 **Objective**
- **Build** a robust pipeline to predict churn (Yes/No) for telecom subscribers.
- **Preprocess** the dataset by dropping non-informative columns, converting data types, and handling missing values.
- **Train** a **Random Forest** classifier with hyperparameter tuning via **GridSearchCV**.
- **Evaluate** model performance using classification metrics, confusion matrix, and **ROC AUC**.
- **Visualize** results using an **interactive ROC curve**, a **mosaic-style confusion matrix**, a **SHAP beeswarm plot**, and a **learning curve** with error bars.

---

## 📂 **Dataset Overview**
- **File:** `telecom_churn.csv`
- **Rows:** ~7,000 
- **Columns:** 21 total, including demographic and subscription-related features:
  - `customerID` (dropped)
  - `gender`, `SeniorCitizen`, `Partner`, `Dependents`
  - `tenure`, `PhoneService`, `MultipleLines`
  - `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`
  - `StreamingTV`, `StreamingMovies`
  - `Contract`, `PaperlessBilling`, `PaymentMethod`
  - `MonthlyCharges`, `TotalCharges`
  - `Churn` (Yes/No) → **Target** (0/1)

**Target Variable:**  
- `Churn` → 0 (No), 1 (Yes)

---

## 🏗️ **Model: Random Forest Classifier**
A **Random Forest** is an ensemble of decision trees, each trained on a bootstrapped subset of data and features:
- **Robustness:** Handles non-linear relationships well.
- **Feature Importance:** Provides insights into which features matter most.
- **Reduced Overfitting:** Aggregates multiple trees, lowering variance.


**Best Cross-Validation Accuracy:** ~0.8010

---

**🌀 Data Preprocessing**

- **Drop customerID:** Non-predictive column removed.
- **Convert Churn:** Map "Yes" → 1, "No" → 0.
- **Handle TotalCharges:** Convert to float and fill invalid or missing values with the median.
- **Numerical vs. Categorical:**
  - **Numerical:** SeniorCitizen, tenure, MonthlyCharges, TotalCharges.
  - **Categorical:** All remaining columns (to be encoded using OneHotEncoder).
- **Scaling:** Use StandardScaler for numerical columns.
- **Training Set Shape:** (5634, 30)
- **Test Set Shape:** (1409, 30)

_No missing values remain after cleaning._

---

**📊 Performance Metrics**  
_On the test set:_

| **Metric**                 | **Value** |
|----------------------------|-----------|
| **Accuracy**               | ~80%      |
| **Precision (No Churn)**   | 0.84      |
| **Recall (No Churn)**      | 0.90      |
| **Precision (Churn)**      | 0.66      |
| **Recall (Churn)**         | 0.53      |
| **F1-Score (Churn)**       | 0.59      |
| **ROC AUC Score**          | 0.84      |

**Confusion Matrix**

| **Actual**         | **Predicted No Churn** | **Predicted Churn** |
|--------------------|------------------------|---------------------|
| **No Churn (0)**   | 933                    | 102                 |
| **Churn (1)**      | 175                    | 199                 |

---

**📈 Results and Visualizations**

**✅ 1. Interactive ROC Curve (AUC = ~0.84)**  
- Displays TPR vs. FPR with a diagonal baseline.
- The area under the curve of ~0.84 indicates moderate to strong ranking capability.

**✅ 2. Mosaic-Style Confusion Matrix**  
- Uses a bar chart to show how actual vs. predicted classes break down.
- 933 true negatives and 199 true positives are the largest segments.
- Reveals approximately 175 churners missed (false negatives).

**✅ 3. SHAP Beeswarm Plot**  
- SHAP (SHapley Additive exPlanations) clarifies feature contributions.
- **Key Features (example):**  
  - **tenure:** Longer subscription reduces churn.
  - **MonthlyCharges:** Higher charges can push customers to leave.
  - **Contract:** One- or two-year contracts lower churn.
  - **SeniorCitizen:** May have unique churn behavior.

**✅ 4. Learning Curve with Error Bars**  
- Shows training set size versus accuracy for both training and validation sets.
- Training accuracy starts high (~0.92) and slightly decreases with more data.
- Validation accuracy remains around 0.78–0.80, indicating stable performance.
