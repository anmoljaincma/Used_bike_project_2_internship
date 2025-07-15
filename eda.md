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

## 💰 Univariate Analysis – Price

We explored the `price` column using histograms, boxplots, and categorical segmentation to understand how used bike prices are distributed.

---

### 📊 1. Distribution Plot

We plotted a histogram to visualize the overall distribution of prices:

```python
import matplotlib.pyplot as plt
import seaborn as sns
import matplotlib.ticker as ticker

plt.figure(figsize=(12, 6))  # Make plot wide enough
ax = sns.histplot(data=df, x='price', bins=50, kde=True, color='skyblue')

# Format X-axis with commas (₹ 10,000 instead of 10000)
ax.xaxis.set_major_formatter(ticker.FuncFormatter(lambda x, _: f'{int(x):,}'))

plt.title('Distribution of Bike Prices')
plt.xlabel('Price (₹)')
plt.ylabel('Number of Bikes')
plt.xticks(rotation=45)  # Rotate for readability
plt.grid(True)
plt.tight_layout()
plt.show()
```
**Note**: All screenshots of graph are given in EDA docx file.
### 🔍 Observations:
The distribution is right-skewed, with most bikes priced in the lower range.


Majority of bikes fall under ₹2,50,000, with fewer listings in the high-end range.


## 📊 2. Bar Plot of Price Segments (₹0 – ₹2.5L)
To explore this further, we created price segments from ₹0 to ₹2.5L and visualized the frequency using a bar plot.
```python

# Step 1: Define bins and labels
bins = [0, 50000, 100000, 150000, 200000, 250000]
labels = ['0–50K', '50K–1L', '1L–1.5L', '1.5L–2L', '2L–2.5L']

# Step 2: Create a new column with price segment
df['price_segment'] = pd.cut(df['price'], bins=bins, labels=labels, include_lowest=True)

# Step 3: Count bikes in each segment
segment_counts = df['price_segment'].value_counts().sort_index()

# Step 4: Plot
plt.figure(figsize=(10, 6))
sns.barplot(x=segment_counts.index, y=segment_counts.values, palette='pastel')

plt.title('Bike Count by Price Segment (₹0–2.5L)')
plt.xlabel('Price Segment')
plt.ylabel('Number of Bikes')
plt.grid(True)
plt.tight_layout()
plt.show()
```
**Note**: All screenshots of graph are given in EDA docx file.
### 🔍 Insights:
Most bikes are listed in the **₹0–₹50K** range.

The second-highest volume is in the **₹50K–₹1L** segment.

This confirms a strong focus on **budget-friendly used bikes** in the dataset.

#### ✅ These insights help in defining pricing strategies, identifying high-volume segments, and selecting features for price prediction models


