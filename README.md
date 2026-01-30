# 🌾 AI-Based Crop Health Monitoring Using Drone Multispectral Data

<div align="center">

[![Python Version](https://img.shields.io/badge/python-3.12-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Made with SHAP](https://img.shields.io/badge/Made%20with-SHAP-green.svg)](https://github.com/slundberg/shap)
[![Made with LIME](https://img.shields.io/badge/Made%20with-LIME-green.svg)](https://github.com/marcotcr/lime)

**An end-to-end AI pipeline for precision agriculture, leveraging drone-captured multispectral vegetation indices to detect and predict crop stress.**

[View Project](#-project-overview) • [Getting Started](#-getting-started) • [Methodology](#-methodology) • [Results](#-key-results) • [Documentation](docs/METHODOLOGY.md)

</div>

---

## 📌 Project Overview

This repository presents a comprehensive machine learning solution for **automated crop health monitoring** using multispectral imagery data captured by agricultural drones. The system analyzes vegetation indices to classify crop health states (Healthy vs. Stressed) and provides actionable insights for precision agriculture applications.

### 🎯 Key Objectives

- **Detect crop stress early** using multispectral vegetation indices (NDVI, GNDVI, SAVI, EVI, etc.)
- **Build robust ML models** with comprehensive validation and cross-validation
- **Provide explainable AI insights** using SHAP and LIME interpretability frameworks
- **Generate spatial stress maps** for targeted drone scouting and intervention planning
- **Deliver actionable agronomic recommendations** based on data-driven analysis

**🔗 Repository:** [https://github.com/AvirupRoy2195/AI-Based-Crop-Health-Capstone](https://github.com/AvirupRoy2195/AI-Based-Crop-Health-Capstone)

---

## 🏗️ System Architecture

The project follows a modular, end-to-end pipeline architecture designed for scalability and interpretability:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           DATA ACQUISITION LAYER                             │
│  ┌───────────────────┐  ┌───────────────────┐  ┌───────────────────┐        │
│  │  Multispectral    │  │  Vegetation       │  │  Spatial          │        │
│  │  Drone Imagery    │──▶  Indices (NDVI,   │──▶  Coordinates      │        │
│  │                   │  │  GNDVI, SAVI...)  │  │  (Grid X, Y)      │        │
│  └───────────────────┘  └───────────────────┘  └───────────────────┘        │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                          ADVANCED ANALYTICS LAYER                            │
│  ┌───────────────────┐  ┌───────────────────┐  ┌───────────────────┐        │
│  │  Root Cause       │  │  Multicollinearity│  │  Exploratory      │        │
│  │  Analysis (RCA)   │  │  Check (VIF)      │  │  Data Analysis    │        │
│  └───────────────────┘  └───────────────────┘  └───────────────────┘        │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         MACHINE LEARNING PIPELINE                            │
│  ┌───────────────────┐  ┌───────────────────┐  ┌───────────────────┐        │
│  │  Feature          │  │  Class Balance    │  │  Model Training   │        │
│  │  Selection (RFE)  │──▶  (SMOTE)          │──▶  (Random Forest)  │        │
│  └───────────────────┘  └───────────────────┘  └───────────────────┘        │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                          VALIDATION FRAMEWORK                                │
│  ┌───────────────────┐  ┌───────────────────┐  ┌───────────────────┐        │
│  │  Stratified       │  │  Jackknife        │  │  Chi-Square       │        │
│  │  K-Fold CV        │  │  Estimation       │  │  Goodness of Fit  │        │
│  └───────────────────┘  └───────────────────┘  └───────────────────┘        │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                     EXPLAINABILITY & VISUALIZATION                           │
│  ┌───────────────────┐  ┌───────────────────┐  ┌───────────────────┐        │
│  │  SHAP             │  │  LIME             │  │  Spatial Stress   │        │
│  │  (Global XAI)     │  │  (Local XAI)      │  │  Heatmaps         │        │
│  └───────────────────┘  └───────────────────┘  └───────────────────┘        │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Pipeline Components

| Component | Description | Key Techniques |
|-----------|-------------|----------------|
| **Data Acquisition** | Ingestion of drone-captured multispectral data | NDVI, GNDVI, SAVI, EVI, Moisture Index |
| **Root Cause Analysis** | Statistical identification of stress drivers | Correlation analysis, feature importance |
| **Multicollinearity Check** | Elimination of redundant features | Variance Inflation Factor (VIF) |
| **Feature Selection** | Optimal feature subset selection | Recursive Feature Elimination (RFE) |
| **Class Balancing** | Handling imbalanced datasets | SMOTE (Synthetic Minority Oversampling) |
| **Model Training** | Binary classification of crop health | Random Forest Classifier |
| **Cross-Validation** | Robust model performance estimation | Stratified K-Fold CV |
| **Stability Testing** | Variance estimation & outlier detection | Jackknife Resampling |
| **Goodness of Fit** | Statistical validation | Chi-Square Distribution Test |
| **Explainability** | Model interpretability | SHAP (global), LIME (local) |
| **Spatial Visualization** | Field-level stress mapping | Heatmaps, Grid Aggregation |

---

## 📂 Repository Structure

```
AI-Based-Crop-Health-Capstone/
│
├── 📓 AI_Crop_Health_Final_Complete.ipynb   # Main analysis notebook
│                                             # Contains all code, analysis, and visualizations
│
├── 📊 Synthetic Multispectral Crops Data.xlsx # Input dataset
│                                             # Drone-captured vegetation indices & coordinates
│
├── 📄 AI Based Crop Health Capstone.pdf      # Project specification document
│                                             # Original capstone requirements
│
├── 📖 README.md                              # Project documentation (this file)
│
├── 📁 docs/                                  # Additional documentation
│   └── METHODOLOGY.md                        # Detailed methodology breakdown
│
├── 📄 CONTRIBUTING.md                        # Contribution guidelines
│
└── 📄 LICENSE                                # MIT License
```

---

## 🚀 Getting Started

### Prerequisites

Ensure you have **Python 3.10+** installed. The project requires the following dependencies:

```bash
# Core Data Science Stack
pip install pandas numpy matplotlib seaborn

# Machine Learning
pip install scikit-learn imbalanced-learn

# Explainable AI
pip install shap lime

# Statistical Analysis
pip install statsmodels scipy

# Excel Support
pip install openpyxl
```

Or install all dependencies at once:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn shap lime statsmodels scipy openpyxl
```

### Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/AvirupRoy2195/AI-Based-Crop-Health-Capstone.git
   cd AI-Based-Crop-Health-Capstone
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Launch the notebook:**
   ```bash
   jupyter notebook AI_Crop_Health_Final_Complete.ipynb
   ```

4. **Run all cells** to execute the full pipeline and generate results.

---

## 🔬 Methodology

The project follows a structured 6-task methodology:

### Task 1: Data Understanding & Exploration
- Initial data inspection and quality assessment
- Target variable (Health State) analysis
- Comprehensive EDA with visualizations
- Correlation analysis between vegetation indices
- Spatial pattern analysis

### Task 2: Machine Learning Model Development
- Feature engineering and selection using RFE
- Data preprocessing and scaling
- Class imbalance handling with SMOTE
- Model training and hyperparameter tuning
- Multi-metric evaluation (Accuracy, Precision, Recall, F1, AUC-ROC)

### Task 3: Spatial Analysis & Visualization
- Field-level prediction generation
- Stress probability heatmaps
- High-risk zone identification
- Grid-level aggregation for drone flight planning

### Task 4: Drone & Agronomy Interpretation
- Actionable insights generation
- Comprehensive drone operation planning
- Agronomic recommendations based on stress patterns

### Task 5: Model Validation
- Stratified K-Fold Cross-Validation
- Jackknife stability estimation
- Chi-Square goodness of fit testing
- Confidence interval computation

### Task 6: Reflection & Future Improvements
- Project summary and key learnings
- Limitation analysis
- Future enhancement roadmap
- Final conclusions

> 📚 For detailed methodology, see [docs/METHODOLOGY.md](docs/METHODOLOGY.md)

---

## 📊 Key Results

### Model Performance

| Metric | Score |
|--------|-------|
| **Accuracy** | ~95% (Cross-validated) |
| **Precision** | High |
| **Recall** | High |
| **F1-Score** | Balanced |
| **AUC-ROC** | Excellent |

### Key Findings

- 🌿 **NDVI** and **Moisture Index** identified as **primary stress indicators**
- 📈 High model reliability confirmed via **Jackknife stability testing**
- 🗺️ **Spatial clustering** of stress zones enables targeted interventions
- 🔍 **SHAP/LIME** provide transparent, trustworthy explanations for predictions

### Explainability Insights

- **SHAP Analysis**: Reveals global feature importance, identifying which vegetation indices contribute most to stress predictions
- **LIME Analysis**: Provides local, instance-level explanations for individual predictions, enabling case-by-case decision support

---

## 📈 Vegetation Indices Used

| Index | Full Name | Description |
|-------|-----------|-------------|
| **NDVI** | Normalized Difference Vegetation Index | Measures vegetation greenness and density |
| **GNDVI** | Green NDVI | Chlorophyll absorption indicator |
| **SAVI** | Soil-Adjusted Vegetation Index | Minimizes soil brightness effects |
| **EVI** | Enhanced Vegetation Index | Optimized for high biomass regions |
| **Moisture Index** | Leaf Water Content Index | Indicates plant water stress |
| **NDRE** | Normalized Difference Red Edge | Sensitive to chlorophyll content |

---

## 🛠️ Technologies & Tools

<div align="center">

| Category | Technologies |
|----------|-------------|
| **Language** | Python 3.12 |
| **Data Processing** | pandas, NumPy |
| **Visualization** | Matplotlib, Seaborn |
| **Machine Learning** | scikit-learn, imbalanced-learn |
| **Explainable AI** | SHAP, LIME |
| **Statistical Analysis** | statsmodels, SciPy |
| **Development** | Jupyter Notebook, VS Code |

</div>

---

## 🔮 Future Improvements

1. **Deep Learning Integration**: Implement CNNs for raw multispectral image analysis
2. **Time-Series Analysis**: Add temporal modeling for growth stage prediction
3. **Real-Time Processing**: Deploy as edge computing solution on drones
4. **Multi-Crop Support**: Extend model to support diverse crop types
5. **Weather Integration**: Incorporate meteorological data for improved predictions
6. **Anomaly Detection**: Implement unsupervised anomaly detection for novel stress types

---

## 🤝 Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to submit improvements and fixes.

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Avirup Roy**

- GitHub: [@AvirupRoy2195](https://github.com/AvirupRoy2195)

---

## 🙏 Acknowledgments

- **SHAP Library** for powerful explainability tools
- **LIME Library** for local interpretability
- **scikit-learn** for comprehensive ML toolkit
- Agricultural domain research supporting vegetation index methodologies

---

<div align="center">

**⭐ If you found this project useful, please consider giving it a star!**

Made with ❤️ for Precision Agriculture

</div>
