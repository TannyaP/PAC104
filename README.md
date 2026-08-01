
# Predicting Overtraining Syndrome in Athletes Using Machine Learning and Wearable Sensor Data

This repository presents our project on predicting **Overtraining Syndrome (OTS) risk in athletes** using Machine Learning and longitudinal wearable sensor data.

The project analyzes physiological, training, recovery, and performance-related patterns to identify early signs of excessive training stress. Unlike traditional approaches that rely on fixed thresholds or subjective athlete feedback, our methodology uses **personalized feature engineering and temporal Machine Learning models** to predict overtraining risk **7–14 days before significant performance deterioration or injury may occur**.

---

## Project Summary

Wearable devices are widely used to monitor athlete health, training performance, and recovery. However, excessive training without sufficient recovery can lead to **Overtraining Syndrome (OTS)**, which may cause:

* Persistent fatigue
* Reduced athletic performance
* Sleep disruption
* Abnormal physiological responses
* Increased injury risk
* Prolonged recovery periods

Traditional overtraining monitoring often relies on isolated measurements, fixed thresholds, or subjective feedback. These methods may fail to capture the gradual and personalized nature of fatigue development.

Our project aims to build a **data-driven early-warning system** that analyzes trends and interactions across multiple wearable sensor metrics to predict an athlete’s future overtraining risk.

---

## Problem Statement

Overtraining develops gradually and is difficult to detect during its early stages.

Athletes may experience performance decline only after excessive training stress has accumulated. Existing monitoring systems often lack predictive intelligence and may identify overtraining only after fatigue, performance deterioration, or injury has already occurred.

**Research Question:**

> How can Machine Learning models predict Overtraining Syndrome in athletes before significant performance deterioration or injury occurs?

---

## Proposed Framework

The proposed framework integrates:

* **PFIG — Personalized Fatigue Interaction Graph**
* **TSDM — Temporal Stress Drift Modeling**
* **SA-LSTM — Stress-Aware Long Short-Term Memory Network**

The framework combines personalized physiological baselines, feature interaction analysis, temporal fatigue trends, and sequence-based learning to estimate future overtraining risk.

### Overall Pipeline

**Raw Wearable Data**
→ Data Cleaning
→ Normalization
→ Temporal Alignment
→ Personalized Baseline Computation
→ PFIG Feature Interaction Modeling
→ TSDM Stress Drift Computation
→ Temporal Sequence Structuring
→ Static ML Model Training
→ SA-LSTM Training
→ Overtraining Risk Prediction
→ Early Warning and Actionable Insights

---

## Data Overview

### Wearable and Training Features

The system analyzes multimodal athlete data, including:

* Heart Rate
* Heart Rate Variability (HRV)
* Resting Heart Rate
* Sleep Duration
* Sleep Quality or Sleep Score
* Training Intensity
* Training Duration
* Training Load
* Recovery Intervals
* Activity Metrics
* Steps and Distance
* Calories Burned
* Performance Consistency Metrics

### Data Structure

Each record is organized using:

* Athlete ID
* Date and Timestamp
* Physiological Measurements
* Training Metrics
* Recovery Metrics
* Performance Indicators
* Overtraining Risk Label

The dataset is structured as **longitudinal time-series data**, enabling the model to analyze changes in athlete condition over several days or weeks.

---

## Prediction Targets

The framework can support multiple prediction formats:

### Binary Classification

* **Low Risk / No Overtraining**
* **High Risk / Overtraining Risk**

### Multi-Level Risk Classification

* Low Risk
* Moderate Risk
* High Risk

### Risk Probability Score

A continuous risk score ranging from:

`0 → Minimal Overtraining Risk`

to

`1 → High Overtraining Risk`

---

## Methodology

### Data Collection

Multimodal wearable sensor data is collected continuously for each athlete.

The system focuses on:

* Physiological condition
* Training workload
* Sleep and recovery
* Activity intensity
* Performance stability

Longitudinal monitoring over several weeks or months is preferred to capture gradual fatigue progression and athlete-specific behavior.

---

### Data Preprocessing

The collected data undergoes the following preprocessing steps:

* Removal of duplicate records
* Missing-value handling
* Sensor noise filtering
* Extreme outlier detection
* Feature normalization
* Time-series alignment
* Daily or session-level aggregation
* Handling class imbalance

Athlete-specific normalization is preferred because physiological values such as HRV and resting heart rate can vary significantly between individuals.

---

### Personalized Baseline Computation

A healthy baseline is calculated separately for each athlete.

Baseline metrics may include:

* Average HRV
* Average resting heart rate
* Typical sleep duration
* Normal training workload
* Standard recovery patterns

A baseline observation period of approximately **2–4 weeks** may be used when sufficient historical data is available.

The personalized baseline allows the system to identify deviations relative to an athlete’s normal condition rather than relying only on universal thresholds.

---

### PFIG — Personalized Fatigue Interaction Graph

The **Personalized Fatigue Interaction Graph (PFIG)** models relationships between physiological and training-related features.

#### Graph Nodes

* HRV
* Resting Heart Rate
* Sleep
* Training Load
* Activity Intensity
* Recovery Metrics

#### Interaction Analysis

Feature interaction weights may be calculated using:

* Rolling-window correlations
* Mutual information
* Cross-feature coupling scores

The framework computes a **Feature Interaction Importance Score (FIIS)** to identify the most influential relationships associated with fatigue development.

#### Output

* Personalized feature interaction matrix
* Important fatigue-related feature combinations
* Athlete-specific interaction patterns

---

### TSDM — Temporal Stress Drift Modeling

The **Temporal Stress Drift Modeling (TSDM)** module captures gradual deviations from an athlete’s personalized baseline.

A **Stress Drift Index (SDI)** is calculated as:

`SDI = (Current Value − Personalized Baseline) / Personalized Baseline`

Additional temporal features include:

* Rolling SDI average
* SDI trend or slope
* Cumulative training-load drift
* HRV suppression patterns
* Sleep stability trends
* Recovery Stability Entropy

#### Output

A set of engineered fatigue-state features representing how an athlete’s condition changes over time.

---

### Temporal Dataset Structuring

The time-series data is converted into a supervised Machine Learning format.

#### Input

A sequence of features from the previous **k days**, such as:

`Day 1 → Day 2 → Day 3 → ... → Day k`

#### Output

Predicted overtraining risk at a future time horizon:

`OTS Risk at Day t + h`

The proposed prediction horizon is:

* **7 days in advance**
* **14 days in advance**

This allows the system to provide an early warning before significant performance decline may occur.

---

## Machine Learning Models

The following models are used for performance comparison.

### Baseline Models

#### Logistic Regression

Used as an interpretable baseline model for overtraining-risk classification.

#### Random Forest

Captures nonlinear relationships between physiological, training, and recovery features.

#### XGBoost

Provides efficient gradient-boosted classification and can identify complex feature interactions.

---

### SA-LSTM — Stress-Aware LSTM

The **Stress-Aware Long Short-Term Memory (SA-LSTM)** model is designed to learn temporal fatigue patterns from sequential wearable data.

#### Proposed Architecture

* Input: Time-windowed fatigue-state features
* LSTM Layer: 64 or 128 units
* Dropout Layer
* Dense Layer
* Sigmoid Output Layer

#### Training Configuration

* Loss Function: Binary Cross-Entropy
* Optimizer: Adam
* Early Stopping: Used to reduce overfitting

The LSTM model is expected to perform better than static models when overtraining indicators develop gradually across time.

---

## Evaluation Metrics

Model performance will be evaluated using:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC Score
* Confusion Matrix

Special emphasis is placed on:

* **False Negatives** — cases where high overtraining risk is missed
* **Early Detection Capability** — the number of days of advance warning provided
* **Risk Prediction Consistency** across athletes

---

## Expected Results and Discussion

The proposed framework is expected to identify early overtraining patterns approximately **7–14 days before major performance deterioration**.

Potential indicators include:

* Sustained HRV suppression
* Increased resting heart rate
* Sleep disruption
* Increasing training load
* Insufficient recovery intervals
* Declining performance consistency

Temporal models such as SA-LSTM are expected to outperform static models because they analyze the progression of fatigue rather than evaluating isolated measurements.

### Key Insight

> Predicting fatigue trends and personalized deviations is more effective than monitoring individual wearable metrics using fixed thresholds.

---

## Risk Scoring System

The predicted probability can be converted into an interpretable risk score.

| Risk Probability  | Risk Level       |
| ----------------- | ---------------- |
| Less than 0.30    | 🟢 Low Risk      |
| 0.30–0.70         | 🟡 Moderate Risk |
| Greater than 0.70 | 🔴 High Risk     |

The thresholds can later be personalized based on athlete history and model calibration.

---

## Early Intervention Module

When predicted risk exceeds a defined threshold, the system may recommend:

* Reducing training intensity
* Decreasing training volume
* Increasing recovery time
* Monitoring sleep stability
* Reviewing recent workload trends
* Alerting coaches or sports-health professionals

The system is intended to support training decisions and should not be treated as a standalone medical diagnosis.

---

## Proposed Repository Structure

```text
athlete-overtraining-prediction/
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── metadata/
│
├── notebooks/
│   ├── data_exploration.ipynb
│   ├── feature_engineering.ipynb
│   └── model_evaluation.ipynb
│
├── src/
│   ├── preprocessing.py
│   ├── baseline.py
│   ├── pfig.py
│   ├── tsdm.py
│   ├── models.py
│   └── evaluation.py
│
├── models/
│   ├── logistic_regression/
│   ├── random_forest/
│   ├── xgboost/
│   └── sa_lstm/
│
├── results/
│   ├── metrics/
│   ├── plots/
│   └── confusion_matrices/
│
├── requirements.txt
├── README.md
└── LICENSE
```

---

## Technologies and Tools

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* TensorFlow / Keras
* Matplotlib
* SHAP for Explainable AI
* Jupyter Notebook or Google Colab

---

## Project Goals

* Develop an early-warning system for athlete overtraining risk
* Analyze physiological, training, sleep, and recovery patterns
* Create personalized athlete baselines
* Model interactions between fatigue-related features
* Detect temporal stress drift
* Compare static ML models with temporal deep-learning models
* Predict overtraining risk 7–14 days in advance
* Generate interpretable risk scores
* Support data-driven training and recovery decisions

---

## Future Enhancements

* Personalized fatigue thresholds for every athlete
* Integration of psychological stress indicators
* Real-time wearable data streaming
* Mobile dashboard for athletes and coaches
* Automated risk alerts
* Explainable AI using SHAP values
* Edge ML deployment on wearable devices
* Adaptive training recommendations
* Integration with injury-risk prediction
* Multi-athlete team monitoring

---

## Research Paper

The project research paper will include:

* Abstract
* Keywords
* Introduction and Motivation
* Literature Review
* Problem Statement
* Proposed PFIG–TSDM–SA-LSTM Framework
* Data Collection and Preprocessing
* Feature Engineering
* Machine Learning Methodology
* Experimental Results and Discussion
* Model Evaluation
* Conclusion and Future Work
* References

---

## Team

* Anjum Sana
* Arista Vania
* Tannya Pasricha

---

## Project Status

🟡 **Methodology and Framework Design Completed**

🔄 **Dataset Collection and Model Implementation in Progress**

⏳ **Model Training, Evaluation, and Real-Time Deployment Planned**

---

## 📝 Disclaimer

This project is designed as a Machine Learning–based decision-support and early-warning system. It does not provide a clinical diagnosis of Overtraining Syndrome. Predictions should be interpreted alongside professional coaching, sports-science, and medical guidance.

I kept the structure parallel to your paneer README but made the ML framework look more research-oriented and technically distinct.
