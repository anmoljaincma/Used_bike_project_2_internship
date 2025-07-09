
# 🚲 Used Bike Dataset – Data Cleaning 

This project involved cleaning a real-world **used bike dataset** as a part. The dataset contained several inconsistencies, mixed formats, and missing values that needed to be addressed before analysis or modeling.

---

## 📊 Dataset Overview

The dataset includes the following features:

- `model_name`: Name of the bike model  
- `model_year`: Year the bike was manufactured  
- `kms_driven`: Total kilometers driven  
- `owner`: Ownership category (first, second, etc.)  
- `location`: City or region where the bike is listed  
- `mileage`: Fuel efficiency (kmpl)  
- `power`: Engine power (BHP)  
- `cc`: Engine capacity (cubic centimeters)  
- `brand`: Brand of the bike  
- `price`: Selling price of the bike (target variable)

---

## 🧼 Data Cleaning Steps

### ✅ 1. Handled Missing Values

- Checked for missing values across all columns using `df.isnull().sum()`
- Dropped rows containing missing values in any critical column (e.g., `power`, `mileage`, `cc`, `price`)
- Ensured the final dataset is clean and free of NaN entries

```python
# Check missing values
df.isnull().sum()

# Drop rows with missing values
df.dropna(inplace=True)
```
---  

### ✅ 2. Removed Duplicate Rows

```python
df.drop_duplicates(inplace=True)
```

---

### ✅ 3. Cleaned `kms_driven`

- Removed non-numeric characters like commas and units (`"km"`, `"kms"`)
- Converted to float
- Dropped rows with values less than 500 (likely data entry errors)

```python
df['kms_driven'] = df['kms_driven'].astype(str).str.replace(',', '')
df['kms_driven'] = df['kms_driven'].str.extract(r'(\d+)').astype(float)
df = df[df['kms_driven'] > 500]
```

---

### ✅ 4. Cleaned `power`

- Extracted numeric values from strings like `"6.16kW (8.36Ps)"`, `"15.5 PS"`, `"11.64KW (15.6 BHP)"`
- Converted all values to **BHP** using standard formulas:
  - `1 PS = 0.98632 BHP`
  - `1 kW = 1.34102 BHP`
- Replaced invalid or unreadable entries with `NaN`

```python
# Making every value uniform in power column
import re
import numpy as np

def convert_power(value):
    if pd.isna(value):
        return np.nan

    value = str(value).lower().strip()

    # Try extracting from parentheses first
    if '(' in value and ')' in value:
        inner = re.search(r'\((.*?)\)', value)
        if inner:
            val = inner.group(1).strip()
            match = re.search(r'(\d+\.?\d*)\s*(bhp|ps)', val)
            if match:
                number = float(match.group(1))
                unit = match.group(2)
                if unit == 'ps':
                    return round(number * 0.98632, 2)
                elif unit == 'bhp':
                    return round(number, 2)

    # Fallback: search outside parentheses
    match = re.search(r'(\d+\.?\d*)\s*(kw|ps|bhp)', value)
    if match:
        number = float(match.group(1))
        unit = match.group(2)
        if unit == 'kw':
            return round(number * 1.34102, 2)
        elif unit == 'ps':
            return round(number * 0.98632, 2)
        elif unit == 'bhp':
            return round(number, 2)

    return np.nan

df['power'] = df['power'].apply(convert_power)
```

---

### ✅ 5. Cleaned `mileage`

- Extracted numeric values from formats like `"35 kmpl"`, `"63kmpl"`, `"28 Kms"`
- For ranges like `"45-55 kmpl"`, calculated the average (e.g., `50.0`)
- Dropped invalid values such as `"Liquid Cooled"` or empty strings
- Converted to float type
- Removed rows where mileage < 10 kmpl (likely incorrect or noise)

```python
def clean_mileage(value):
    if pd.isna(value):
        return np.nan
    value = str(value).lower()
    if '-' in value:
        parts = re.findall(r'\d+\.?\d*', value)
        if len(parts) == 2:
            return (float(parts[0]) + float(parts[1])) / 2
    match = re.search(r'\d+\.?\d*', value)
    if match:
        return float(match.group())
    return np.nan

df['mileage'] = df['mileage'].apply(clean_mileage)
df = df[df['mileage'] >= 10]
```


---

### ✅ 6. Cleaned `price`

- Replaced values equal to `0` with `NaN` (as 0 is not a valid bike price)
- Dropped rows where `price` was missing

```python
df['price'] = df['price'].replace(0, np.nan)
df.dropna(subset=['price'], inplace=True)
```

---
### ✅ 7. Standardized Text Fields (Bike Names & Locations)

- Trimmed unnecessary leading/trailing spaces in text columns using Google Sheets' **TRIM** function
- Cleaned and corrected inconsistent bike model names (e.g., `" Pulsar 150"` → `"Pulsar 150"`)
- Used **Google Sheets suggestions** to fix wrong location names (e.g., `"uthagamdala"` corrected to `"udhagamandala"`, `"hanamankonda"` → `"hanamkonda"`)

  ---
  
## ✅ Final Dataset

- Total rows after cleaning: **4927**
- Cleaned dataset saved as: `cleaned_bike_data.csv`

```python
df.to_csv('cleaned_bike_data.csv', index=False)
```

---




## 🧠 Tools Used

- **Python** – For scripting and data manipulation
- **Pandas** – Data cleaning and transformation
- **NumPy** – Numerical operations
- **Regular Expressions (`re`)** – Pattern extraction from text columns
- **Google Colab** – Cloud-based Python notebook environment

---

## 📈 Next Steps

- Perform Exploratory Data Analysis (EDA)
- Feature Engineering (e.g., compute `bike_age` from `model_year`)
- Build regression models to predict `price`
- Create graphs to visualise using Python.

---

## 🙌 Acknowledgment

This cleaning was completed as part of a **Project 2 of Data Analytics Internship**. The objective was to practice real-world data cleaning techniques and prepare the dataset for further analysis and modeling.

---
