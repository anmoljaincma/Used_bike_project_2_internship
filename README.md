# Used_bike_project_2_internship
It is the second project of Unified Mentor Internship.

# Used Bike Price Prediction
## 📖 Project Overview
This project involves analyzing and predicting the prices of used bikes using Exploratory Data Analysis (EDA), Feature Engineering, and Machine Learning models.

## 📂 Index
1. Introduction

2. Dataset

3. Data Cleaning

4. Exploratory Data Analysis

- Univariate Analysis

- Bivariate Analysis

- Multivariate Analysis

- Geographical & Time Series Analysis

5. Feature Engineering

6. Feature Transformation

7. Model Building

- Data Splitting

- Model Selection

- Model Training & Evaluation

8. Hyperparameter Tuning

9. Results & Insights

10. Conclusion & Recommendations

## 1. Introduction
A machine learning project to predict the price of used bikes based on their specifications, brand, location, and other factors.

## 2. Dataset
Source: [Mention dataset source]

Columns: model_name, model_year, kms_driven, owner, location, mileage, power, price, brand(Created later)

Data Cleaning
Removed duplicates

Standardized inconsistent entries (e.g., mileage formats)

Removed or imputed missing values

Outlier detection using IQR

Exploratory Data Analysis
Univariate Analysis
Distribution of price, mileage, power, and kms_driven.

Frequency of categorical variables (owner, brand, location).

Bivariate Analysis
Correlation between features (e.g., price vs kms_driven).

Multivariate Analysis
Pairplots, boxplots to examine combined relationships.

Geographical & Time Series Analysis
Average bike price across locations.

Price trends over years using model_year.

Feature Engineering
Extracted brand from model_name.

Created bike_age from model_year.

One-hot encoded categorical variables (owner, location).

Feature Transformation
Applied StandardScaler to numerical features.

Applied log transformation to skewed variables (price).

Model Building
Data Splitting
80% training and 20% testing using train_test_split.

Model Selection
Linear Regression, Ridge, Lasso

Random Forest, Gradient Boosting

Model Training & Evaluation
Metrics: MAE, MSE, RMSE, R²

Best model: Gradient Boosting Regressor

Hyperparameter Tuning
Used GridSearchCV to optimize Random Forest & Gradient Boosting hyperparameters.

Results & Insights
Key Factors Influencing Price: brand, power, mileage, kms_driven, ownership.

Best Model: Gradient Boosting with R² = 1.0 and lowest RMSE.

Conclusion & Recommendations
Gradient Boosting performed best for predicting used bike prices.

Future improvements:

Add more features like bike condition & seller type.

Use advanced models like XGBoost or LightGBM.

Deploy the model as an API or web app for real-time predictions.

