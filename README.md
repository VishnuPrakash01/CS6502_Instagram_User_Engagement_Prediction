# User Engagement Prediction using PySpark

## Overview

This project focuses on predicting **user engagement on Instagram** using machine learning techniques in a distributed data environment. Built on Databricks with PySpark, the project implements a full end-to-end pipeline including data preprocessing, feature engineering, model building, evaluation, and user segmentation.

## Dataset

The dataset used in this project can be accessed from Kaggle:

[Social Media User Analysis Dataset](https://www.kaggle.com/datasets/rockyt07/social-media-user-analysis/data)

## Project Workflow

### 1. Data Loading

* Data is loaded from a Databricks managed table:
  ```
  workspace.default.instagram_usage_lifestyle
  ```
* The dataset contains user behavior, demographic, and lifestyle features.

---

### 2. Exploratory Data Analysis (EDA)
* Dataset overview and schema inspection
* Missing value analysis
* Duplicate row and duplicate `user_id` checks
* Summary statistics for:
  * Numerical features
  * Categorical features
* Feature distribution analysis
* Correlation analysis with target variable:
  * Target: `user_engagement_score`
* Heatmap visualization of key correlations
* Skewness detection and classification

---

### 3. Data Preprocessing & Feature Engineering

#### Data Cleaning
* Removed irrelevant columns:
  * `user_id`, `app_name`, `last_login_date`

#### Feature Transformation
* Converted:
  * `account_creation_year` → `account_age`

#### Binary Encoding
* Converted Yes/No → 1/0:
  * `has_children`
  * `uses_premium_features`
  * `two_factor_auth_enabled`
  * `biometric_login_used`

#### Skewness Handling

* Applied log transformation to:
  * `followers_count`
  * `following_count`
  * `sessions_per_day`
  * `user_engagement_score` (target variable)

#### Feature Scaling

* Z-score normalization applied to:
  * `followers_count`
  * `following_count`

#### Categorical Encoding

* Manual One-Hot Encoding for multiple categorical features
* Avoided dummy variable trap by dropping one category

---

### 4. Multicollinearity Handling (VIF Analysis)

* Used **Variance Inflation Factor (VIF)** to detect multicollinearity
* Sampled dataset (2%) for efficient computation
* Removed:

  * Constant features
  * Highly correlated engagement metrics
* Manual feature elimination based on domain knowledge

---

### 5. Dataset Preparation

* Final cleaned dataset: `df_cleaned`
* Target variable:

  ```
  user_engagement_score
  ```
* Data split:

  * Training: 80%
  * Validation: 10%
  * Test: 10%

---

## Model Building

### Models Implemented

* Linear Regression
* Decision Tree Regressor
* Random Forest Regressor
* Gradient Boosted Trees (GBT)

### Pipeline

* Feature assembly using `VectorAssembler`
* Integrated ML pipeline using Spark ML

---

### Evaluation Metrics

* R² Score
* RMSE (Root Mean Squared Error)

Evaluation performed on:

* Training set
* Validation set

---

### Feature Importance & Interpretability

* Linear models:
  * Coefficient analysis

* Tree-based models:
  * Feature importance ranking

---

## Feature Selection Strategy

Three modeling stages were implemented:
 1. Initial Model
 2. Reduced Model
 3. Final Model

Top 11 features were selected. The dataset is trained by the best model GBT after tuning.

---

## User Segmentation (Clustering)

### KMeans Clustering
* Applied KMeans clustering for user segmentation
* Features scaled using `StandardScaler`
* Number of clusters: **k = 5**

### Insights
* Identified distinct user behavior groups based on:
  * Session frequency
  * Engagement activity
  * Lifestyle indicators

### Visualizations
* Cluster comparison (bar charts)
* Behavioral scatter plots:
  * Sessions per day vs average session duration

---

## Tech Stack
* **Platform**: Databricks
* **Language**: Python
* **Big Data Processing**: PySpark
* **Machine Learning**: Spark MLlib
* **Statistical Analysis**: Statsmodels, SciPy
* **Visualization**: Matplotlib, Seaborn
* **Data Handling**: Pandas, NumPy

---

## How to Run

1. Open the notebook in Databricks
2. Import all the libraries
3. Run all cells sequentially
4. Ensure access to the dataset:
   ```
   workspace.default.instagram_usage_lifestyle
   ```

---

## Output

* Predicted user engagement scores
* Model performance metrics (R², RMSE)
* Feature importance insights
* User segmentation clusters
* Visual analytics (correlation heatmaps, cluster plots)

---

## Notes

* Target variable is **log-transformed** to handle skewness
* Feature scaling and encoding are essential for model performance
* VIF analysis is used to reduce multicollinearity

---

## Collaboration

This project is developed in a shared Databricks notebook environment where multiple team members contribute collaboratively.

---

