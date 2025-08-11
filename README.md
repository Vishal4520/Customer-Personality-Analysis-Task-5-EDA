
# 📊 Customer Personality Analysis – Task 5 EDA

## 🔹 Steps Performed

1. **Import libraries** – Loaded Pandas, Matplotlib, and Seaborn for data handling and visualization.
2. **Load dataset** – Read the file `cleaned_customer_personality_analysis.xlsx.csv` from `E:\DA Project`.
3. **Initial inspection** – Used `df.head()`, `df.shape`, `df.info()`, and `df.describe()` to understand data structure.
4. **Missing value & duplicate check** – Verified with `df.isnull().sum()` and `df.duplicated().sum()`.
5. **Column categorization** – Split into numeric (`num_cols`) and categorical (`cat_cols`) lists.
6. **Univariate analysis** –

   * Histograms for numeric features.
   * Countplots for categorical features.
   * Boxplots to detect outliers.
7. **Bivariate/multivariate analysis** –

   * Correlation heatmap to study relationships.
   * Pairplot for visual patterns between variables.
   * Scatterplots for selected variable pairs.
8. **Observations** – Wrote insights after each visualization.
9. **Summary** – Compiled main findings and possible business implications.

---

## 1️⃣ Correlation Heatmap

```python
plt.figure(figsize=(10,6))
sns.heatmap(df[num_cols].corr(), annot=True, cmap='coolwarm', center=0)
plt.title("Correlation Heatmap")
plt.show()
```

**Observations:**

* Strong positive correlations between spending categories like `mntwines`, `mntmeatproducts`, `mntgoldproducts`, and `total_spend` (> 0.7).
* `income` has a moderate positive correlation with high-value products (wines, meats).
* `recency` has a negative correlation with spending — recent customers spend more.
* Household size variables (`kidhome`, `teenhome`) have slight negative correlation with luxury product spending.

---

## 2️⃣ Pairplot (Sample of Numeric Columns)

```python
sns.pairplot(df[['income','mntwines','mntmeatproducts','mntgoldproducts','total_spend']], diag_kind='kde')
plt.show()
```

**Observations:**

* Higher `income` generally relates to higher product spending.
* Clusters in spending patterns suggest different customer segments.
* Wine and meat spending strongly increase together.

---

## 3️⃣ Histograms (Numeric Distributions)

```python
df[num_cols].hist(bins=20, figsize=(14,10))
plt.tight_layout()
plt.show()
```

**Observations:**

* `age` is concentrated between 30–60 years.
* `income` is right-skewed; majority earn under \$60K.
* Some spending variables have many zeros (non-buyers).

---

## 4️⃣ Boxplots (Outlier Detection)

```python
for col in num_cols:
    plt.figure(figsize=(6,2))
    sns.boxplot(x=df[col])
    plt.title(col)
    plt.show()
```

**Observations:**

* `income` has high-value outliers (premium customers).
* `age` has outliers above 90 — possible data errors.
* Spending columns have outliers representing high spenders.

---

## 5️⃣ Scatterplots (Two-Variable Relationships)

```python
sns.scatterplot(data=df, x='income', y='mntwines')
plt.title("Income vs Wine Spending")
plt.show()

sns.scatterplot(data=df, x='age', y='income')
plt.title("Age vs Income")
plt.show()

---

**Observations:**

* Income vs Wine Spending: upward trend — higher income → higher wine purchases.
* Age vs Income: no strong pattern; some older customers have high incomes.
  _________________________________________

## 📌 Summary

1. Higher-income customers spend more, especially on premium products.
2. Product spending categories are highly correlated — potential for cross-selling.
3. Recent buyers are more active spenders.
4. Income and spending are skewed — few high-value customers dominate revenue.
5. Outliers exist in income and age — may need handling.
6. Potential customer segments based on spending patterns.

---
