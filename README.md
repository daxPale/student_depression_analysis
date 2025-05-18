# Student Depression Analysis

## Overview

This repository contains an analysis of student depression factors and a prediction model built using machine learning techniques. The analysis explores various factors contributing to depression among students and builds a predictive model to identify at-risk individuals.

## Repository Navigation

- [Predicting_Student_Depression.pdf](Predicting_Student_Depression.pdf) - Complete research report with detailed analysis and findings
- [StudentDepression.ipynb](StudentDepression.ipynb) - Jupyter notebook with the complete code implementation
- [student_depression_dataset.csv](student_depression_dataset.csv) - Original dataset used for analysis

## Methodology

### Data Preprocessing

1.  **Loading Data:** The dataset is loaded using pandas.
2.  **Initial Cleaning:**
    - Removal of rows with '?' in 'Financial Stress'.
    - Removal of rows with 'Others' category in 'Dietary Habits' and 'Degree'.
    - Dropping the 'id' column.
3.  **Handling Categorical Variables:**
    - Exploratory Data Analysis (EDA) led to the removal of 'City' (high cardinality) and 'Profession' (low variance).
    - Remaining categorical features ('Gender', 'Dietary Habits', 'Degree') were one-hot encoded.
4.  **Feature Scaling:** Numerical features were standardized using `StandardScaler`.

### Exploratory Data Analysis (EDA)

EDA was performed to understand data distributions, identify missing values, and explore relationships between features and the target variable. Visualizations included count plots for categorical features and distribution plots for numerical features.

### Feature Engineering

- **Sleep Duration:** Textual 'Sleep Duration' (e.g., "'Less than 5 hours'") was parsed into numerical hours. Missing values after parsing were imputed with the median.
- **Binary Conversion:** 'Have you ever had suicidal thoughts ?' and 'Family History of Mental Illness' were converted into binary (0/1) representations.

### Model Training and Evaluation

1.  **Data Splitting:** The preprocessed data was split into 70% training and 30% testing sets, stratified by the 'Depression' target variable.
2.  **Models Implemented:**
    - Logistic Regression
    - Random Forest Classifier
    - XGBoost Classifier
    - Stacking Classifier (using the above three as base learners and Logistic Regression as a meta-learner)
3.  **Hyperparameter Tuning:** `GridSearchCV` with 5-fold cross-validation was used to find the optimal hyperparameters for Logistic Regression, Random Forest, and XGBoost, optimizing for ROC-AUC.
4.  **Evaluation Metrics:**
    - ROC-AUC Score
    - Accuracy
    - Classification Report (Precision, Recall, F1-Score)
    - Confusion Matrix
    - ROC Curves
    - Calibration Curves

## Results

The models performed as follows on the test set:

| Model                 | Test ROC-AUC | Test Accuracy |
| :-------------------- | :----------- | :------------ |
| Logistic Regression   | 0.9244       | 0.8504        |
| Random Forest         | 0.9207       | 0.8451        |
| XGBoost               | 0.9248       | 0.8490        |
| **Stacking Ensemble** | **0.9249**   | **0.8490**    |

## Key Findings

- Machine learning models can effectively predict student depression with high accuracy (around 85%) and ROC-AUC (around 0.925).
- The Stacking Ensemble model demonstrated the most robust performance.
- **Top Feature Importances (from Random Forest):**
  1.  Suicidal Thoughts (Binary)
  2.  Academic Pressure
  3.  Financial Stress
  4.  Age
  5.  Work/Study Hours
- These findings highlight critical areas for potential intervention and support within student populations.

## Detailed Report

For a comprehensive analysis including visualizations, statistical tests, and in-depth discussion of results, please refer to the [full PDF report](Predicting_Student_Depression.pdf).
