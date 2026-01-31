# Boston Housing Analysis: Governance-Aware Clustering & Predictive Modeling (with Explainability)

This project provides an end-to-end machine learning workflow using the Boston Housing dataset, with an emphasis on **robust evaluation, transparency, and auditability**.

Rather than focusing only on predictive accuracy, the notebook highlights governance-relevant considerations such as:

- Data quality and reproducibility  
- Model stability and generalization  
- Interpretability vs. performance trade-offs  
- Post-hoc explainability for black-box models  

Although the dataset concerns housing prices (MEDV), the primary purpose is to demonstrate how governance-oriented thinking can be embedded throughout the modeling lifecycle.

---

## Repository Structure

- `Boston_Housing_Analysis_Clustering_and_Predictive_Modeling.ipynb`  
  Full workflow: EDA → correlation → scaling → clustering → supervised modeling → SHAP explainability → robustness diagnostics → conclusions.

- `README.md`  
  Project overview, methodology, and key findings.

- `.gitignore`  
  Standard ignore rules.

---

## Project Goals and Objectives

This project conducts a comprehensive analysis of the Boston Housing dataset to understand key drivers of house prices and to compare multiple modeling approaches under governance-aware criteria.

### Objectives

1. **Data Exploration & Preparation**
   - Data quality checks (missing values, duplicates)
   - Exploratory inspection of feature distributions
   - Feature scaling where appropriate

2. **Correlation Analysis (Exploratory)**
   - Identify features most associated with the target (MEDV)
   - Use Pearson correlation for linear association
   - Use Spearman correlation as a more robust alternative for skewed or discrete variables  
   - Correlation is used for interpretive insight rather than statistical inference

3. **Unsupervised Learning**
   - Cluster neighborhoods using K-Means (CRIM, LSTAT, DIS)
   - Select cluster count using silhouette scores
   - Visualize and interpret cluster structure

4. **Supervised Learning**
   - Train/test split
   - Compare: Linear Regression, KNN, Decision Tree, Neural Network (PyTorch)
   - Evaluate with multiple metrics (R², MAE, MSE, RMSE)
   - Discuss generalization and robustness

5. **Model Interpretation**
   - Explain model behavior and trade-offs between performance and interpretability
   - Apply SHAP explainability to improve auditability of black-box models

---

## Dataset

The dataset is loaded from the CMU repository and reconstructed into:

- 506 observations  
- 13 input features  
- Target variable: **MEDV** (median home value)

---

# Chapter 1 — Data Preparation, Cleaning and Normalization

## Data Quality Checks
- Verified no missing values
- Confirmed all rows are unique (no duplicates)

This establishes a clean and auditable foundation for downstream modeling.

---

## Descriptive Statistics & Distribution Review
Key descriptive statistics and histograms were used to identify:

- skewness and heavy tails (e.g., CRIM, ZN)
- discrete or multimodal variables (e.g., RAD, TAX)
- scale differences motivating feature normalization

---

## Correlation Analysis (Pearson + Spearman)
Both correlation types were computed:

- Pearson for linear trends  
- Spearman as a rank-based robustness check  

Key drivers of MEDV include:

- **LSTAT (negative association)**
- **RM (positive association)**

These insights guide feature understanding and model selection.

---

## Scatter Plot Validation
Scatter plots confirmed intuitive relationships:

- more rooms → higher MEDV  
- higher lower-status proportion → lower MEDV  
- crime rate shows negative association (log-scale visualization)

---

## Feature Scaling
StandardScaler was applied to ensure comparability and numerical stability, especially for:

- distance-based models (KNN, K-Means)
- gradient-based models (Neural Network)

---

# Chapter 2 — Unsupervised Learning: Neighborhood Clustering

K-Means clustering was applied to CRIM, LSTAT, and DIS to explore structural patterns in neighborhood conditions.

- silhouette analysis selected an optimal **2-cluster** solution
- cluster scatter plots supported interpretation of neighborhood regimes

This step provides a governance-relevant understanding of subgroup structure prior to predictive modeling.

---

# Chapter 3 — Supervised Modeling and Robust Evaluation

## Train/Test Split
Models were trained on 80% of the data and evaluated on a held-out 20% test set.

Predictors were selected based on exploratory analysis:

- LSTAT, RM, DIS

---

## Models Evaluated

- **Linear Regression** — transparent baseline with global interpretability  
- **KNN Regressor** — strong predictive performance, evaluated via leakage-aware pipeline  
- **Decision Tree Regressor** — rule-based interpretability with complexity control  
- **Feedforward Neural Network (PyTorch)** — highest-capacity model, requiring post-hoc explainability  

All models were compared using:

- MAE, MSE, RMSE, R²  
- Cross-validation diagnostics where appropriate

---

## Leakage-Aware Evaluation (Pipeline)
For KNN, preprocessing was embedded inside a Pipeline to avoid data leakage during cross-validation.

This supports reliable generalization estimates and audit-ready methodology.

---

## Neural Network Robustness Experimentation
A learning-rate sensitivity analysis was conducted (0.0005, 0.001, 0.002), demonstrating the importance of empirical tuning even under fixed architectural specifications.

---

# Explainability and Auditability (SHAP)

The neural network achieved the best predictive performance but operates as a black box.

To improve transparency and support auditability, SHAP was applied to quantify feature contributions and provide:

- global feature influence patterns  
- local explanations for individual predictions  

SHAP results confirmed that:

- LSTAT is the strongest driver  
- RM contributes positively  
- DIS plays a secondary role  

These findings align with earlier correlation and regression analysis, supporting model validity.

---

# Exploratory Robustness Diagnostic Across Subgroups

As an additional robustness check, prediction errors were compared across neighborhoods with relatively low vs. high LSTAT values (median split).

This provides a lightweight diagnostic of whether model performance differs across socioeconomic conditions.

**Note:** This is not a formal bias or fairness audit, but an exploratory error distribution check.

---

# Model Comparison Summary

Test-set evaluation shows:

- Neural Network (lr = 0.002) achieved the lowest MSE and highest R²  
- KNN performed nearly as well with simpler logic  
- Decision Tree provided interpretable rules with moderate accuracy  
- Linear Regression served as the most transparent but weakest baseline  

---

# Governance-Oriented Takeaways

This project highlights key governance-aware ML principles:

- **Accuracy alone is insufficient** — model suitability depends on transparency and reliability  
- **Methodology matters** — leakage-aware evaluation improves trust in performance estimates  
- **Interpretability is a spectrum** — simple models are inherently auditable, complex models require explainability tools  
- **Explainability supports accountability** — SHAP bridges performance and transparency for black-box models  
- **Robustness diagnostics improve confidence** — subgroup error checks provide additional validation signals  

---

## Conclusion

This notebook demonstrates how governance considerations such as auditability, robustness, and transparency can be integrated throughout the ML development lifecycle.

The project illustrates the practical trade-off between:

- predictive performance  
- interpretability  
- accountability  

which is central to responsible deployment of machine learning systems.
