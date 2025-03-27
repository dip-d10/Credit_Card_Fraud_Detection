# Credit Card Fraud Detection

This project focuses on building a robust machine learning model to detect fraudulent credit card transactions. Using a combination of exploratory data analysis, feature scaling, and advanced modeling techniques like XGBoost with hyperparameter tuning, this project aims to accurately distinguish between legitimate and fraudulent transactions.

## Table of Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Methodology](#methodology)
  - [Data Exploration](#data-exploration)
  - [Feature Engineering & Scaling](#feature-engineering--scaling)
  - [Model Building](#model-building)
  - [Hyperparameter Tuning](#hyperparameter-tuning)
- [Results](#results)
- [Project Structure](#project-structure)
- [Installation & Requirements](#installation--requirements)
- [Usage](#usage)
- [License](#license)

## Overview

Credit card fraud is a critical issue affecting financial institutions and consumers worldwide. This project demonstrates how to use machine learning to detect fraud in credit card transactions using a dataset that includes anonymized features (resulting from PCA), along with key features such as `Time`, `Amount`, and the binary target `Class` (where 0 represents legitimate transactions and 1 represents fraud).

## Dataset

The dataset contains:
- **PCA-Transformed Features (V1 to V28):** These columns are the result of a Principal Component Analysis (PCA) applied to anonymize and reduce the dimensionality of the original transaction features.
- **Time:** Represents the elapsed time in seconds from the first transaction.
- **Amount:** The monetary value of the transaction.
- **Class:** A binary label indicating whether the transaction is fraudulent (1) or legitimate (0).

## Methodology

### Data Exploration
- **Initial Inspection:** The data was inspected using summary statistics and visualizations (histograms for `Time` and `Amount`) to understand distributions and identify any patterns.
- **Class Imbalance:** A significant imbalance was observed, with fraudulent transactions being a very small fraction of the dataset.

### Feature Engineering & Scaling
- **Feature Scaling:** The `Amount` column was scaled using `StandardScaler` to standardize its values (mean = 0, standard deviation = 1). This is critical for many machine learning models to perform optimally.
- **Additional Feature Consideration:** Time-based features can also be engineered if necessary, but in this project, we focused primarily on scaling and utilizing the provided features.

### Model Building
- **Baseline Model:** A Logistic Regression model was initially built, but its performance was not sufficient for the highly imbalanced dataset.
- **Advanced Models:** A Random Forest and an XGBoost classifier were implemented. XGBoost, in particular, demonstrated strong performance due to its ability to handle imbalanced datasets and complex non-linear relationships.

### Hyperparameter Tuning
- **Tuning with GridSearchCV:** Hyperparameter tuning was performed on the XGBoost model using GridSearchCV. Parameters such as `learning_rate`, `max_depth`, `n_estimators`, `subsample`, and `colsample_bytree` were tuned.
- **Best Parameters:** The best hyperparameters found were:
  - `colsample_bytree`: 0.8
  - `learning_rate`: 0.2
  - `max_depth`: 7
  - `n_estimators`: 200
  - `subsample`: 0.8
  - `scale_pos_weight`: 446.52542372881356 (calculated based on the class distribution)
- **Performance:** The tuned model achieved a cross-validation AUC-ROC score of ~0.996 and a test AUC-ROC score of ~0.979.

## Results

The final tuned XGBoost model provided excellent performance for fraud detection:
- **AUC-ROC (Test):** 0.9788
- **Classification Report:**
  - **Legitimate Transactions (Class 0):** Precision and recall near 1.00
  - **Fraudulent Transactions (Class 1):** Precision of 0.89 and recall of 0.75

These metrics indicate that the model is highly effective at distinguishing between legitimate and fraudulent transactions.


