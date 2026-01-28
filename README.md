# Governance-Aware Machine Learning: Model Comparison & Explainability

## Project Overview
This project demonstrates how common machine learning models can be evaluated and compared from a **governance-aware perspective**, focusing not only on predictive performance, but also on **transparency, stability, and auditability**.

While the dataset used is a housing price dataset, the primary goal of this project is **not real estate prediction**, but to illustrate how different model families behave under governance-relevant criteria such as explainability, robustness, and generalization.

## Models Evaluated
The following models were implemented and compared:

- **Linear Regression** – transparent baseline model
- **K-Nearest Neighbors (KNN)** – high-performing, distance-based model
- **Decision Tree Regressor** – interpretable model with explicit decision rules

All models were evaluated using:
- Train/test split
- 10-fold cross-validation
- Multiple performance metrics (R², MAE, MSE, RMSE)

For KNN, preprocessing and evaluation were conducted using a **Pipeline** to ensure leakage-aware cross-validation.

## Model Performance Summary
From a purely predictive perspective:
- **KNN achieved the highest test performance**, capturing local non-linear patterns effectively.
- **Decision Tree showed moderate performance**, requiring careful complexity control to avoid overfitting.
- **Linear Regression served as a transparent but limited baseline**.

However, predictive accuracy alone does not determine model suitability in regulated or high-risk contexts.

## Governance-Oriented Comparison

| Aspect | Linear Regression | KNN | Decision Tree |
|------|------------------|-----|---------------|
| Predictive Performance | Low–Medium | High | Medium |
| Transparency | High | Low | Medium–High |
| Stability Across Folds | High | Medium | Medium |
| Interpretability | Global | Low | Rule-based |
| Governance Suitability | High | Conditional | High |

## Explainability and Transparency
Explainability analysis using **SHAP (SHapley Additive exPlanations)** was conducted to support model transparency and auditability.

The SHAP analysis illustrates how individual features contribute to model predictions, enabling:
- Feature influence inspection
- Model behavior validation
- Support for governance requirements such as transparency and explainability

## Key Governance Takeaways
- **High performance does not imply high trustworthiness**: KNN achieved the best accuracy but lacks inherent interpretability.
- **Model simplicity supports auditability**: Linear Regression and Decision Trees offer clearer reasoning paths, which are essential in regulated domains.
- **Evaluation methodology matters**: Leakage-aware cross-validation is critical for reliable performance estimation.
- **Explainability tools complement black-box models**: SHAP helps bridge the gap between performance and accountability.

## Repository Structure

- **Boston_Housing_Analysis_Clustering_and_Predictive_Modeling.ipynb**  
  Main notebook containing the complete end-to-end analysis, including EDA, clustering, supervised modeling, and explainability.

- **README.md**  
  Project overview, methodology, and key findings.

- **.gitignore**  
  Git ignore rules.

## Why This Matters
In domains such as healthcare, finance, or regulated AI systems, model selection must balance:
- Predictive accuracy
- Transparency
- Robustness
- Auditability

This project demonstrates how governance considerations can be embedded into the model development and evaluation process, rather than treated as an afterthought.
