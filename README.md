# Used_bike_project_2_internship
It is the second project of Unified Mentor Internship.

# Used Bike Price Prediction
## 📖 Project Overview
This project involves analyzing and predicting the prices of used bikes using Exploratory Data Analysis (EDA), Feature Engineering, and Machine Learning models.

## 📂 Index
1. [Introduction](https://github.com/anmoljaincma/Used_bike_project_2_internship/blob/main/README.md#1-introduction)

2. [Dataset](https://github.com/anmoljaincma/Used_bike_project_2_internship/blob/main/README.md#2-dataset)

3. [Data Cleaning](data_cleaning.md)

4. **Exploratory Data Analysis**
   - [Price Univariate Analysis](eda_price_univariate_analysis.md)
   - [Other Variables Univariate Analysis](Bike_Data_Project_2_internship.ipynb)
   - [Bivariate Analysis](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=ouqM-8nnXfzE)

5. [Feature Engineering](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=DL2NB4N-kQUK)

6. [Feature Transformation](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=bT8mTnymeWbc)

7. **Data Visualization**
   - [Multivariate Plots](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=leTIH3yRof-y)
   - [Geographical Analysis](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=Li96U5I1QY_u)
   - [Time Series Analysis](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=Li96U5I1QY_u)

8. **Model Building**

    - [Data Splitting](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=rd-vy1V37yPi)
    - [Model Selection](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=qzW6YXqoA6S9)
    - [Model Training & Evaluation](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=89W5bc6dIPg0)

9. [Hyperparameter Tuning](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=VWP-TBYbbVkr)

10. [Conclusion & Recommendations](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=gObnaCctrWdf)

11. [Next Steps](https://colab.research.google.com/drive/1xA9RRs4hOEfvhvypMgYkVl8SR_A1lGQ3?usp=sharing#scrollTo=PwQBwRCCOYOs) 

## 1. Introduction
A machine learning project to predict the price of used bikes based on their specifications, brand, location, and other factors.

## 2. Dataset
Source: [cleaned_bike_data.csv](cleaned_bike_data.csv)  
**Columns:** model_name, model_year, kms_driven, owner, location, mileage, power, price, brand(Created later)

## 3. Data Cleaning
Removed duplicates

Standardized inconsistent entries (e.g., mileage formats)

Removed or imputed missing values

Outlier detection using IQR

## 4. Exploratory Data Analysis
Univariate Analysis
Distribution of price, mileage, power, and kms_driven.

Frequency of categorical variables (owner, brand, location).

## 5. Bivariate Analysis
Correlation between features (e.g., price vs kms_driven).



Feature Engineering
Extracted brand from model_name.

Created bike_age from model_year.

One-hot encoded categorical variables (owner, location).

Feature Transformation
Applied StandardScaler to numerical features.

Applied log transformation to skewed variables (price).

Data Visualization
Multivariate Analysis
Pairplots, boxplots to examine combined relationships.

Geographical & Time Series Analysis
Average bike price across locations.

Price trends over years using model_year.
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

