# 📘 Detailed Methodology Documentation

## AI-Based Crop Health Monitoring Using Drone Multispectral Data

This document provides an in-depth breakdown of the methodological approach used in this project.

---

## Table of Contents

1. [Data Description](#1-data-description)
2. [Exploratory Data Analysis](#2-exploratory-data-analysis)
3. [Feature Engineering](#3-feature-engineering)
4. [Machine Learning Pipeline](#4-machine-learning-pipeline)
5. [Validation Framework](#5-validation-framework)
6. [Explainable AI (XAI)](#6-explainable-ai-xai)
7. [Spatial Analysis](#7-spatial-analysis)
8. [Agronomic Interpretation](#8-agronomic-interpretation)

---

## 1. Data Description

### 1.1 Dataset Overview

The dataset consists of synthetic multispectral crop data simulating drone-captured agricultural imagery. Each record represents a field pixel/zone with associated vegetation indices and spatial coordinates.

### 1.2 Features

| Feature | Type | Description |
|---------|------|-------------|
| `Grid_X` | Numeric | X-coordinate on the field grid |
| `Grid_Y` | Numeric | Y-coordinate on the field grid |
| `NDVI` | Numeric (0-1) | Normalized Difference Vegetation Index |
| `GNDVI` | Numeric (0-1) | Green Normalized Difference Vegetation Index |
| `SAVI` | Numeric (0-1) | Soil-Adjusted Vegetation Index |
| `EVI` | Numeric (0-1) | Enhanced Vegetation Index |
| `Moisture_Index` | Numeric | Leaf water content indicator |
| `NDRE` | Numeric (0-1) | Normalized Difference Red Edge Index |
| `Health_State` | Binary | Target: 0 = Healthy, 1 = Stressed |

### 1.3 Vegetation Index Formulas

**NDVI (Normalized Difference Vegetation Index)**

```
NDVI = (NIR - Red) / (NIR + Red)
```

- Range: -1 to +1 (healthy vegetation: 0.2 to 0.9)
- Interpretation: Higher values indicate denser, healthier vegetation

**GNDVI (Green NDVI)**

```
GNDVI = (NIR - Green) / (NIR + Green)
```

- More sensitive to chlorophyll concentration variations
- Better at detecting nitrogen status

**SAVI (Soil-Adjusted Vegetation Index)**

```
SAVI = ((NIR - Red) / (NIR + Red + L)) × (1 + L)
```

- L = soil brightness correction factor (typically 0.5)
- Minimizes soil background effects in sparse vegetation

**EVI (Enhanced Vegetation Index)**

```
EVI = G × ((NIR - Red) / (NIR + C1 × Red - C2 × Blue + L))
```

- G = gain factor, C1, C2 = atmospheric correction coefficients, L = canopy background adjustment
- Optimized for high biomass regions, reduces atmospheric influences

---

## 2. Exploratory Data Analysis

### 2.1 Data Quality Assessment

- **Missing Values**: Check for null/NaN values
- **Outlier Detection**: Box plots and IQR-based detection
- **Distribution Analysis**: Histograms and density plots for each feature
- **Skewness/Kurtosis**: Statistical normality assessment

### 2.2 Target Variable Analysis

- **Class Distribution**: Healthy vs. Stressed ratio
- **Imbalance Assessment**: Determine if SMOTE or other balancing is needed
- **Visualization**: Bar charts and pie charts of class proportions

### 2.3 Correlation Analysis

- **Pearson Correlation Matrix**: Linear relationships between indices
- **Multicollinearity Detection**: Identify highly correlated features (r > 0.8)
- **VIF Analysis**: Variance Inflation Factor to quantify multicollinearity

### 2.4 Spatial Pattern Analysis

- **Stress Distribution Maps**: Visualize where stress occurs on the field
- **Clustering Patterns**: Identify if stress is spatially clustered or random
- **Grid-Level Statistics**: Aggregated metrics per grid cell

---

## 3. Feature Engineering

### 3.1 Feature Selection Strategy

**Recursive Feature Elimination (RFE)**

RFE is used to select the optimal subset of features:

1. Train model with all features
2. Rank features by importance
3. Remove least important feature
4. Repeat until optimal subset is found

```python
from sklearn.feature_selection import RFE
from sklearn.ensemble import RandomForestClassifier

selector = RFE(RandomForestClassifier(), n_features_to_select=5)
selector.fit(X_train, y_train)
selected_features = X.columns[selector.support_]
```

### 3.2 Multicollinearity Handling

**Variance Inflation Factor (VIF)**

VIF quantifies multicollinearity severity:

| VIF Value | Interpretation |
|-----------|----------------|
| 1 | No correlation |
| 1 - 5 | Moderate correlation |
| > 5 | High correlation (consider removing) |
| > 10 | Severe multicollinearity (remove) |

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor

vif_data = pd.DataFrame()
vif_data["feature"] = X.columns
vif_data["VIF"] = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
```

### 3.3 Feature Scaling

- **StandardScaler**: Standardizes features (mean=0, std=1)
- Applied after train-test split to prevent data leakage

---

## 4. Machine Learning Pipeline

### 4.1 Class Imbalance Handling

**SMOTE (Synthetic Minority Over-sampling Technique)**

SMOTE generates synthetic samples for the minority class:

1. Select a minority sample
2. Find its k-nearest neighbors
3. Create synthetic sample between them

```python
from imblearn.over_sampling import SMOTE

smote = SMOTE(random_state=42)
X_resampled, y_resampled = smote.fit_resample(X_train, y_train)
```

### 4.2 Model Selection

**Random Forest Classifier**

Chosen for:

- ✅ High accuracy with minimal tuning
- ✅ Handles non-linear relationships
- ✅ Built-in feature importance
- ✅ Robust to outliers
- ✅ Works well with correlated features

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(
    n_estimators=100,
    max_depth=None,
    min_samples_split=2,
    random_state=42
)
```

### 4.3 Evaluation Metrics

| Metric | Formula | Use Case |
|--------|---------|----------|
| **Accuracy** | (TP + TN) / Total | Overall correctness |
| **Precision** | TP / (TP + FP) | When false positives are costly |
| **Recall** | TP / (TP + FN) | When false negatives are costly |
| **F1-Score** | 2 × (Precision × Recall) / (Precision + Recall) | Balanced evaluation |
| **AUC-ROC** | Area under ROC curve | Discrimination ability |

---

## 5. Validation Framework

### 5.1 Train-Test Split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)
```

### 5.2 Stratified K-Fold Cross-Validation

Ensures class proportions are maintained in each fold:

```python
from sklearn.model_selection import StratifiedKFold, cross_val_score

cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
scores = cross_val_score(model, X, y, cv=cv, scoring='accuracy')
print(f"CV Accuracy: {scores.mean():.3f} ± {scores.std():.3f}")
```

### 5.3 Jackknife Estimation

Leave-one-out resampling for stability assessment:

```python
def jackknife_accuracy(model, X, y):
    n = len(y)
    predictions = []
    for i in range(n):
        X_train = np.delete(X, i, axis=0)
        y_train = np.delete(y, i)
        model.fit(X_train, y_train)
        pred = model.predict(X[[i]])
        predictions.append(pred[0] == y[i])
    return np.mean(predictions), np.std(predictions)
```

### 5.4 Chi-Square Goodness of Fit

Tests if model predictions match expected distribution:

```python
from scipy.stats import chi2_contingency

observed = confusion_matrix(y_test, y_pred).flatten()
chi2, p_value, dof, expected = chi2_contingency(observed.reshape(2, 2))
```

---

## 6. Explainable AI (XAI)

### 6.1 SHAP (SHapley Additive exPlanations)

**Global Feature Importance**

SHAP values reveal how each feature contributes to predictions:

```python
import shap

explainer = shap.TreeExplainer(model)
shap_values = explainer.shap_values(X_test)

# Summary plot
shap.summary_plot(shap_values[1], X_test, feature_names=feature_names)
```

**Interpretation:**

- Features with higher SHAP values have greater impact
- Positive SHAP pushes prediction toward "Stressed"
- Negative SHAP pushes prediction toward "Healthy"

### 6.2 LIME (Local Interpretable Model-agnostic Explanations)

**Instance-Level Explanations**

LIME explains individual predictions:

```python
from lime.lime_tabular import LimeTabularExplainer

explainer = LimeTabularExplainer(
    X_train.values,
    feature_names=feature_names,
    class_names=['Healthy', 'Stressed'],
    mode='classification'
)

explanation = explainer.explain_instance(
    X_test.iloc[0].values,
    model.predict_proba
)
explanation.show_in_notebook()
```

---

## 7. Spatial Analysis

### 7.1 Stress Probability Mapping

Generate field-level stress probability maps:

```python
# Predict stress probabilities
stress_probs = model.predict_proba(X_field)[:, 1]

# Create heatmap
plt.figure(figsize=(12, 10))
scatter = plt.scatter(
    df['Grid_X'], df['Grid_Y'],
    c=stress_probs, cmap='RdYlGn_r',
    s=100, edgecolors='black', linewidths=0.5
)
plt.colorbar(scatter, label='Stress Probability')
plt.title('Crop Stress Probability Map')
```

### 7.2 High-Risk Zone Identification

```python
# Identify high-risk zones (stress probability > 0.7)
high_risk = df[stress_probs > 0.7]
print(f"High-risk zones: {len(high_risk)} ({len(high_risk)/len(df)*100:.1f}%)")
```

### 7.3 Grid-Level Aggregation

```python
# Aggregate by grid cell
grid_stats = df.groupby(['Grid_X', 'Grid_Y']).agg({
    'stress_prob': 'mean',
    'NDVI': 'mean',
    'Moisture_Index': 'mean'
}).reset_index()
```

---

## 8. Agronomic Interpretation

### 8.1 Drone Operation Planning

Based on stress maps, optimize drone flight paths:

1. **Priority Zones**: High stress probability areas for targeted scouting
2. **Sampling Strategy**: Proportional sampling based on stress severity
3. **Flight Path Optimization**: Minimize flight time while covering critical zones

### 8.2 Intervention Recommendations

| Stress Indicator | Likely Cause | Recommended Action |
|------------------|--------------|-------------------|
| Low NDVI | Poor vegetation density | Fertilizer application, replanting |
| Low Moisture Index | Water stress | Irrigation adjustment |
| Low GNDVI | Nitrogen deficiency | Nitrogen fertilizer application |
| Clustered stress | Disease/pest | Targeted pesticide treatment |

### 8.3 Decision Support Matrix

```
Stress Level Assessment:
┌─────────────┬───────────────┬────────────────────────┐
│ Probability │ Risk Level    │ Action                 │
├─────────────┼───────────────┼────────────────────────┤
│ 0.0 - 0.3   │ Low           │ Routine monitoring     │
│ 0.3 - 0.5   │ Moderate      │ Increased monitoring   │
│ 0.5 - 0.7   │ High          │ Ground-truth scouting  │
│ 0.7 - 1.0   │ Critical      │ Immediate intervention │
└─────────────┴───────────────┴────────────────────────┘
```

---

## References

1. **NDVI**: Rouse, J.W., et al. (1974). "Monitoring Vegetation Systems in the Great Plains with ERTS"
2. **SHAP**: Lundberg, S.M., & Lee, S.I. (2017). "A Unified Approach to Interpreting Model Predictions"
3. **LIME**: Ribeiro, M.T., et al. (2016). "Why Should I Trust You?: Explaining the Predictions of Any Classifier"
4. **SMOTE**: Chawla, N.V., et al. (2002). "SMOTE: Synthetic Minority Over-sampling Technique"
5. **Random Forest**: Breiman, L. (2001). "Random Forests"

---

<div align="center">

**📚 For questions or clarifications, please open an issue on GitHub.**

</div>
