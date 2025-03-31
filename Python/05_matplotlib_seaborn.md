# 📊 Matplotlib & Seaborn Cheat Sheet

## 📥 Importing
```python
import matplotlib.pyplot as plt
import seaborn as sns
```

## 📈 Line Plot
```python
plt.plot([1, 2, 3], [4, 5, 6])
plt.title("Line Chart")
plt.show()
```

## 📊 Bar Chart
```python
plt.bar(["A", "B", "C"], [10, 20, 15])
```

## 📉 Histogram
```python
plt.hist(data, bins=10)
```

## 📦 Box Plot
```python
sns.boxplot(x="category", y="value", data=df)
```

## 🟢 Scatter Plot
```python
sns.scatterplot(x="x", y="y", data=df)
```

## 🎨 Styling
```python
plt.xlabel("X Axis")
plt.ylabel("Y Axis")
sns.set_style("whitegrid")
```

📚 Learn more: [Seaborn Docs](https://seaborn.pydata.org/)
