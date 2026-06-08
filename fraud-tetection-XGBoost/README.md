
# 🚨 Credit Card Fraud Detection using Machine Learning

## 📌 Project Overview

This project builds an end-to-end fraud detection system to identify fraudulent credit card transactions using machine learning. The dataset is highly imbalanced, making it a realistic fintech-style classification problem.

The system uses:
- XGBoost for high-performance classification
- SMOTE to handle class imbalance
- SHAP for model interpretability
- StandardScaler for feature normalization
- Threshold tuning for improved fraud recall

---

## 📊 Dataset Description

The dataset contains credit card transactions made by European cardholders in 2013.

- Total transactions: 284,807
- Fraud transactions: 492 (0.17%)
- Highly imbalanced classification problem

### Features:
- Time → seconds since first transaction
- Amount → transaction value
- V1–V28 → PCA-transformed anonymized features
- Class → target variable (0 = normal, 1 = fraud)

---

## ⚙️ Project Pipeline

### 1. Data Preprocessing

- Loaded dataset using Pandas
- Scaled `Time` and `Amount` using StandardScaler

Why scaling matters:
- Ensures numerical stability
- Prevents large-value dominance during training

---

### 2. Train-Test Split

- 80% training data
- 20% testing data
- Stratified split used to preserve fraud ratio

Why stratification is important:
- Fraud cases are rare
- Ensures balanced distribution in train and test sets

---

### 3. Handling Class Imbalance (SMOTE)

Problem:
- Fraud cases represent only 0.17% of data

Solution:
- SMOTE (Synthetic Minority Oversampling Technique)

How SMOTE works:
- Generates synthetic fraud samples based on nearest neighbors
- Balances dataset without simple duplication

Why SMOTE is important:
- Helps model learn fraud patterns effectively
- Reduces bias toward majority class (normal transactions)

---

### 4. Model Training (XGBoost)

Model used:
- XGBoost Classifier

Why XGBoost:
- High performance on tabular data
- Handles non-linear relationships
- Industry-standard for fraud detection

Key parameters:
- n_estimators = 300
- max_depth = 6
- learning_rate = 0.05
- subsample = 0.8
- colsample_bytree = 0.8

Training approach:
- Model trained on SMOTE-balanced dataset
- Learns both fraud and normal patterns equally

---

### 5. Prediction Phase

Two outputs are generated:
- Class prediction → fraud / not fraud
- Probability prediction → likelihood of fraud

---

### 6. Model Evaluation

Since the dataset is imbalanced, accuracy is NOT a good metric.

### Metrics used:

#### Precision
How many predicted frauds were actually fraud.

#### Recall (MOST IMPORTANT)
How many actual frauds were correctly detected.

👉 In fraud detection, recall is critical because missing fraud is costly.

#### ROC-AUC
Measures ability to distinguish between fraud and normal transactions.

#### PR-AUC (Most important for imbalance)
Focuses only on fraud detection performance.

#### Confusion Matrix
Breaks down:
- True Positives
- False Positives
- True Negatives
- False Negatives

---

### 7. Threshold Tuning

Instead of default 0.5 threshold:

threshold = 0.3

Why:
- Lower threshold increases fraud detection (recall)
- Slight increase in false positives is acceptable in fintech

Business logic:
- It is better to flag suspicious transactions than miss fraud

---

### 8. Model Explainability (SHAP)

Problem:
- XGBoost is a black-box model

Solution:
- SHAP (SHapley Additive Explanations)

### Global Explanation:
- Identifies most important features influencing fraud detection

### Local Explanation:
- Explains why a specific transaction was classified as fraud

Why SHAP matters in fintech:
- Regulatory compliance
- Transparency in financial decisions
- Trust in AI systems

---

### 9. Model Saving

Saved artifacts:
- Trained XGBoost model (fraud_detector.pkl)
- StandardScaler (scaler.pkl)

Why saving is important:
- Enables deployment without retraining
- Allows integration into APIs and production systems

---

## 🧠 Final Outcome

This project successfully demonstrates:

✔ Fraud detection on highly imbalanced data  
✔ SMOTE-based imbalance handling  
✔ XGBoost-based classification model  
✔ Evaluation using ROC-AUC and PR-AUC  
✔ Threshold tuning for business optimization  
✔ SHAP-based model interpretability  
✔ Production-ready model saving  

---

## 💼 Resume Summary

Built an end-to-end fraud detection system using XGBoost on highly imbalanced credit card transaction data. Applied SMOTE to address class imbalance and improve minority class detection. Evaluated model performance using ROC-AUC and PR-AUC metrics and optimized decision threshold for higher fraud recall. Implemented SHAP explainability to interpret model predictions at both global and individual transaction levels. Saved trained model and preprocessing pipeline for deployment readiness.

---

## 🚀 Possible Next Improvements

- Deploy using FastAPI for real-time fraud scoring
- Build Streamlit dashboard for visualization
- Integrate SHAP explanations into UI
- Simulate real-time transaction stream
- Containerize using Docker
