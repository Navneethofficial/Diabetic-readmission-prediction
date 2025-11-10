# 🏥 Diabetic Patient Readmission Prediction

A machine learning project to predict 30-day hospital readmission risk for diabetic patients, enabling targeted interventions to improve patient outcomes and reduce healthcare costs.

## 📋 Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Results](#results)
- [Key Features](#key-features)
- [Installation](#installation)
- [Usage](#usage)
- [Future Work](#future-work)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Project Overview

Hospital readmissions, particularly within 30 days of discharge, represent a significant challenge in healthcare management. This project develops a predictive model to identify diabetic patients at high risk of early readmission, allowing healthcare providers to:

- Prioritize post-discharge interventions
- Allocate resources more effectively
- Reduce avoidable rehospitalizations
- Improve patient outcomes and quality of care
- Lower overall healthcare costs

## 📊 Dataset

- **Source:** [UCI Diabetic Data Set](https://archive.ics.uci.edu/ml/datasets/Diabetes+130-US+hospitals+for+years+1999-2008)
- **Size:** ~100,000 patient encounters
- **Timeframe:** 10 years of data from 130 U.S. hospitals
- **Target Variable:** Binary classification
  - **Class 1 (Positive):** Readmitted within 30 days (`<30`)
  - **Class 0 (Negative):** Readmitted after 30+ days or not readmitted (`>30` or `NO`)
- **Class Distribution:** Imbalanced dataset with ~11.16% positive class

## 🔬 Methodology

### Problem Formulation
This is a binary classification problem with significant class imbalance. Due to the imbalanced nature of the target variable, **Average Precision (PR AUC)** was selected as the primary evaluation metric, as it provides more meaningful insights than ROC AUC for imbalanced datasets.

### Models Evaluated

#### 1. Baseline: Logistic Regression
- Used `class_weight="balanced"` to handle class imbalance
- Established baseline performance metrics

**Performance:**
- ROC AUC: 0.676
- PR AUC: 0.219

#### 2. Final Model: XGBoost Classifier
- Integrated into a scikit-learn `Pipeline`
- Hyperparameter tuning via `GridSearchCV`
- Cross-validation: `StratifiedKFold`
- Optimization metric: PR AUC

**Best Hyperparameters:**
```json
{
    "colsample_bytree": 0.7,
    "gamma": 0,
    "learning_rate": 0.05,
    "max_depth": 4,
    "min_child_weight": 5,
    "subsample": 0.8
}
```

**Performance:**
- ROC AUC: 0.684
- PR AUC: 0.235

## 📈 Results

### Model Comparison

| Model | ROC AUC | PR AUC |
|-------|---------|--------|
| **XGBoost (Tuned)** | **0.684** | **0.235** |
| Logistic Regression | 0.676 | 0.219 |

The XGBoost model outperformed the baseline, demonstrating improved ability to identify the minority positive class (30-day readmissions).

## 🔑 Key Features

The most important predictors of 30-day readmission, identified through feature importance analysis:

| Feature | Importance | Clinical Interpretation |
|---------|------------|------------------------|
| `number_inpatient` | 0.091 | History of prior inpatient admissions |
| `discharge_disposition_id_1` | 0.074 | Discharge to home |
| `discharge_disposition_id_11` | 0.068 | Discharge to specific facility type |
| `discharge_disposition_id_22` | 0.064 | Discharge disposition |
| `number_emergency` | 0.017 | History of emergency visits |
| `number_diagnoses` | 0.016 | Total number of diagnoses |
| `insulin_Down` | 0.015 | Insulin medication decreased |
| `diabetesMed_No` | 0.018 | No diabetes medication prescribed |

### Clinical Insights

1. **Prior Healthcare Utilization:** Patients with frequent prior inpatient admissions and emergency visits are at higher risk
2. **Discharge Disposition:** Where patients are discharged to (home, skilled nursing facility, etc.) is a strong predictor
3. **Medication Management:** Changes in diabetes medication and insulin dosing during hospitalization impact readmission risk

## 💻 Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/diabetic-readmission-prediction.git
cd diabetic-readmission-prediction

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Requirements
```
pandas
numpy
scikit-learn
xgboost
matplotlib
seaborn
jupyter
```

## 🚀 Usage

```python
# Load the trained model
import pickle

with open('models/xgboost_model.pkl', 'rb') as f:
    model = pickle.load(f)

# Make predictions
predictions = model.predict(X_test)
prediction_proba = model.predict_proba(X_test)[:, 1]

# Get risk scores for intervention prioritization
high_risk_patients = prediction_proba > 0.3  # Adjust threshold as needed
```

## 🔮 Future Work

1. **Threshold Optimization:** Conduct cost-benefit analysis to identify optimal decision threshold for targeting the top 20-30% highest-risk patients

2. **Advanced Feature Engineering:**
   - Explore diagnosis code combinations (`diag_1`, `diag_2`, `diag_3`)
   - Create interaction features between key predictors
   - Incorporate temporal patterns in patient history

3. **Model Explainability:**
   - Implement SHAP (SHapley Additive exPlanations) for individual patient risk profiling
   - Develop clinician-friendly dashboards for model interpretability
   - Validate feature importance with clinical experts

4. **Deployment:**
   - Develop API for real-time risk scoring
   - Integrate with electronic health record (EHR) systems
   - Create monitoring pipeline for model performance tracking

5. **External Validation:**
   - Test model on data from additional hospital systems
   - Assess model fairness across demographic groups

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss proposed changes.

## 📚 References

- UCI Machine Learning Repository: Diabetes 130-US hospitals dataset
- Chen, T., & Guestrin, C. (2016). XGBoost: A Scalable Tree Boosting System


---

**Note:** This model is intended for research and educational purposes. Clinical deployment requires appropriate validation, regulatory approval, and integration with clinical workflows.
