# Python Code - Exploratory Data Analysis (EDA)

## Project
**Task 5 - Exploratory Data Analysis**

Dataset: **TechX_Sales_Dataset (1).csv**

---

# Import Required Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings

warnings.filterwarnings("ignore")

sns.set_style("whitegrid")
pd.set_option("display.max_columns", None)
```

---

# Load Dataset

```python
df = pd.read_csv("TechX_Sales_Dataset (1).csv")
```

---

# Display First Five Rows

```python
df.head()
```

---

# Display Last Five Rows

```python
df.tail()
```

---

# Dataset Shape

```python
df.shape
```

---

# Dataset Information

```python
df.info()
```

---

# Statistical Summary

```python
df.describe()
```

---

# Column Names

```python
df.columns
```

---

# Data Types

```python
df.dtypes
```

---

# Missing Values

```python
df.isnull().sum()
```

---

# Duplicate Values

```python
df.duplicated().sum()
```

---

# Remove Duplicates

```python
df.drop_duplicates(inplace=True)
```

---

# Convert Date Column

```python
df["Order_Date"] = pd.to_datetime(df["Order_Date"])
```

---

# Unique Values

```python
df.nunique()
```

---

# Category Count

```python
df["Category"].value_counts()
```

---

# Region Count

```python
df["Region"].value_counts()
```

---

# Product Count

```python
df["Product"].value_counts()
```

---

# Correlation Matrix

```python
df.select_dtypes(include=np.number).corr()
```

---

# Histogram

```python
plt.figure(figsize=(8,5))

sns.histplot(
    data=df,
    x="Sales",
    bins=30,
    kde=True
)

plt.title("Sales Distribution")
plt.xlabel("Sales")
plt.ylabel("Frequency")

plt.show()
```

**Observation**

- Shows distribution of Sales.
- Helps identify skewness and spread.

---

# Boxplot

```python
plt.figure(figsize=(8,5))

sns.boxplot(
    x=df["Sales"]
)

plt.title("Sales Boxplot")

plt.show()
```

**Observation**

- Detects outliers.
- Shows spread of sales.

---

# Scatter Plot

```python
plt.figure(figsize=(8,5))

sns.scatterplot(
    data=df,
    x="Sales",
    y="Profit"
)

plt.title("Sales vs Profit")

plt.show()
```

**Observation**

- Identifies relationship between Sales and Profit.

---

# Correlation Heatmap

```python
plt.figure(figsize=(8,6))

sns.heatmap(
    df.select_dtypes(include=np.number).corr(),
    annot=True,
    cmap="coolwarm"
)

plt.title("Correlation Heatmap")

plt.show()
```

**Observation**

- Displays positive and negative correlations among numerical variables.

---

# Pair Plot

```python
sns.pairplot(
    df.select_dtypes(include=np.number)
)

plt.show()
```

**Observation**

- Shows pairwise relationships among numerical features.

---

# Sales by Region

```python
plt.figure(figsize=(8,5))

sns.barplot(
    data=df,
    x="Region",
    y="Sales"
)

plt.title("Sales by Region")

plt.show()
```

**Observation**

- Compares sales performance across different regions.

---

# Sales by Category

```python
plt.figure(figsize=(8,5))

sns.barplot(
    data=df,
    x="Category",
    y="Sales"
)

plt.title("Sales by Category")

plt.show()
```

**Observation**

- Shows which product category generates the highest sales.

---

# Quantity Distribution

```python
plt.figure(figsize=(8,5))

sns.histplot(
    data=df,
    x="Quantity",
    bins=15,
    kde=True
)

plt.title("Quantity Distribution")

plt.show()
```

---

# Monthly Sales Trend

```python
df["Month"] = df["Order_Date"].dt.month

monthly_sales = df.groupby("Month")["Sales"].sum()

plt.figure(figsize=(10,5))

monthly_sales.plot(
    marker="o"
)

plt.title("Monthly Sales Trend")
plt.xlabel("Month")
plt.ylabel("Total Sales")

plt.grid(True)

plt.show()
```

**Observation**

- Displays monthly sales performance.

---

# Monthly Profit Trend

```python
monthly_profit = df.groupby("Month")["Profit"].sum()

plt.figure(figsize=(10,5))

monthly_profit.plot(
    marker="o",
    color="green"
)

plt.title("Monthly Profit Trend")
plt.xlabel("Month")
plt.ylabel("Total Profit")

plt.grid(True)

plt.show()
```

---

# Top Products by Sales

```python
top_products = (
    df.groupby("Product")["Sales"]
    .sum()
    .sort_values(ascending=False)
)

plt.figure(figsize=(12,5))

top_products.plot(kind="bar")

plt.title("Top Products by Sales")
plt.xlabel("Product")
plt.ylabel("Sales")

plt.show()
```

---

# Profit by Category

```python
plt.figure(figsize=(8,5))

sns.barplot(
    data=df,
    x="Category",
    y="Profit"
)

plt.title("Profit by Category")

plt.show()
```

---

# Average Sales by Region

```python
df.groupby("Region")["Sales"].mean()
```

---

# Average Profit by Region

```python
df.groupby("Region")["Profit"].mean()
```

---

# Top 10 Highest Sales

```python
df.nlargest(10, "Sales")
```

---

# Top 10 Highest Profit

```python
df.nlargest(10, "Profit")
```

---

# Final Business Insights

- The dataset is clean with no missing values.
- Duplicate records were checked and removed if present.
- Sales distribution helps understand customer purchasing patterns.
- Outliers were identified using boxplots.
- Scatter plots revealed the relationship between Sales and Profit.
- Correlation heatmap highlighted dependencies between numerical features.
- Monthly sales trends provide insights into seasonal demand.
- Regional analysis identifies high-performing markets.
- Category analysis highlights the best-performing product categories.
- Product analysis identifies top revenue-generating products.

---

# Conclusion

Exploratory Data Analysis (EDA) helped uncover meaningful patterns, trends, and relationships within the sales dataset. The analysis provides valuable insights into sales performance, profitability, regional contributions, and product demand, enabling data-driven business decisions.
