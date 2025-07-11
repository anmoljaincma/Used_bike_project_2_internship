## 📊 1. Descriptive Statistics (`df.describe()`)

We begin EDA by examining basic descriptive statistics for the numerical features using:

```python
print(df.describe())
```
**Note**: All screenshots are given in EDA docx file given in repository.

### 📌 Key Insights:
1. model_year ranges from 1970 to 2021 with a median around 2016.

2. kms_driven shows high variability (max = 100,000 km), suggesting wide usage differences.

3. mileage ranges from 12 to 95 kmpl, with an average of ~42.

4. power has an outlier max of 197.3 BHP (possibly a superbike).

5. price ranges widely from ₹2,000 to ₹19 lakhs (likely some outliers or luxury bikes).


```python
df.describe(include='object')
```
**Note**: All screenshots are given in EDA docx file given in repository.

### 📌 Key Insights:  
1. model_name has 1,034 unique values; the most common is Royal Enfield Classic 350cc 2017 (78 listings).

2. owner is dominated by first owner entries (4,237 out of 4,913).

3. location includes 438 unique city/place entries — Delhi appears most frequently (904 times).

