
# 🚲 Used Bike Dataset – Data Cleaning Project

This project involved cleaning a real-world **used bike dataset** as part of a data analytics internship. The dataset contained several inconsistencies, mixed formats, and missing values that needed to be addressed before analysis or modeling.

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

### ✅ 1. Removed Duplicate Rows

```python
df.drop_duplicates(inplace=True)
```

---

### ✅ 2. Standardized Categorical Columns

```python
df['brand'] = df['brand'].str.strip().str.lower()
df['owner'] = df['owner'].str.strip().str.lower()
df['location'] = df['location'].str.strip().str.lower()
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

### ✅ 6. Cleaned `cc` (Engine Capacity)

- Extracted numeric values from entries like `"149 cc"`, `"200CC"`, or `"124.7 cc"`
- Removed non-numeric values and kept only valid numerical entries
- Converted to float for analysis

```python
df['cc'] = df['cc'].astype(str).str.extract(r'(\d+\.?\d*)').astype(float)
```

---

### ✅ 7. Cleaned `price`

- Replaced values equal to `0` with `NaN` (as 0 is not a valid bike price)
- Dropped rows where `price` was missing

```python
df['price'] = df['price'].replace(0, np.nan)
df.dropna(subset=['price'], inplace=True)
```

---

## ✅ Final Dataset

- Total rows after cleaning: **4970**
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
- Create dashboards using Power BI or Tableau

---

## 🙌 Acknowledgment

This project was completed as part of a **Data Analytics Internship**. The objective was to practice real-world data cleaning techniques and prepare the dataset for further analysis and modeling.

---
