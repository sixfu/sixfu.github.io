---
title: Understand the partial dependency plot and feature importance
---

# Machine Learning Interpretability Concepts

## 1. What is Partial Dependence?

Partial dependence is a technique used to understand the relationship between a subset of features and the predicted outcome of a machine learning model. It shows how the predicted response changes as a feature (or features) vary, while marginalizing over the effects of all other features.

- **How it works:** For a chosen feature \(X_s\), partial dependence computes the expected model prediction by averaging over the distributions of all other features \(X_c\), i.e.

  \[
  \hat{f}_{X_s}(x_s) = \mathbb{E}_{X_c} [\hat{f}(x_s, X_c)]
  \]

- **Purpose:** Helps interpret complex "black-box" models like random forests, boosting, or neural nets by visualizing how each feature influences predictions.

- **Visual Representation:** Partial Dependence Plots (PDPs) plot the feature values on the x-axis and the average predicted output on the y-axis.

- **Limitations:** Assumes independence between features and may mislead when features interact strongly.

---

## 2. What is Feature Importance in Random Forest?

Feature importance in Random Forest (RF) quantifies how influential each feature is in predicting the target variable. It helps identify which variables contribute most to the model’s decisions.

- **Typical Methods:**

  - **Mean Decrease in Impurity (MDI):** Average reduction in node impurity (e.g., Gini impurity) brought by splitting on the feature, averaged over all trees.
  
  - **Permutation Importance:** Measures the increase in prediction error when the feature's values are randomly permuted, breaking its association with the target.

- **Interpretation:** Higher feature importance values mean the feature contributes more to the model’s predictive power.

---

## 3. Similar Feature Importance Concepts in Other Models

| Model                     | Feature Importance Concept                | Description                                                               |
|---------------------------|------------------------------------------|---------------------------------------------------------------------------|
| **Decision Tree**         | Mean Decrease in Impurity (MDI)          | Same as in RF but computed on a single tree.                              |
| **XGBoost**               | Gain, Weight, Cover                       | - **Gain:** Improvement in accuracy by splits using the feature.          |
|                           |                                          | - **Weight:** Number of times the feature is used in splits.              |
|                           |                                          | - **Cover:** Number of samples affected by splits on the feature.        |
|                           | **SHAP values**                           | Model-agnostic importance measuring feature contribution to predictions.  |

- **Tree-based models (DT, RF, XGBoost)** often provide built-in importance scores based on how splits improve model fit.
- **Permutation importance** and **SHAP values** are model-agnostic and used broadly across models for interpretability.

---

*References:*  
- Partial dependence and PDPs: [interpret.ml](https://interpret.ml/docs/pdp.html), [scikit-learn docs](https://scikit-learn.org/stable/modules/partial_dependence.html)  
- RF Feature importance: Breiman (2001), sklearn documentation  
- XGBoost importance: [XGBoost manual](https://xgboost.readthedocs.io/en/stable/python/python_api.html#xgboost.XGBClassifier.get_booster)  
- SHAP: Lundberg & Lee (2017)

