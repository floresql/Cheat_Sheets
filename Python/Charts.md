# Python Charts Cheat Sheet

### 1. Basic Comparisons (Bar & Line)
Best for showing trends over time or comparing categorical data.

```python
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px

# Bar Chart (Matplotlib)
categories = ['A', 'B', 'C']
values = [10, 20, 15]
plt.bar(categories, values, color='skyblue')
plt.title("Bar Chart Example")

# Line Chart (Seaborn)
# Ideal for trends and time-series data
sns.lineplot(x=[1, 2, 3, 4], y=[10, 15, 13, 17])
plt.title("Line Trend")

# Interactive Line (Plotly)
fig = px.line(x=[1, 2, 3], y=[4, 5, 6], title="Interactive Line")
fig.show()
```

---

### 2. Distributions (Histogram & Box Plot)
Used to see the spread and outliers of your data.

```python
# Histogram (Seaborn)
# kde=True adds a smoothing line
sns.histplot(data=df, x="score", bins=20, kde=True)

# Box Plot (Matplotlib)
# Shows Median, Quartiles, and Outliers
plt.boxplot(df['age'])
```

---

### 3. Relationships (Scatter & Heatmap)
Used to find correlations between two or more variables.

```python
# Scatter Plot (Seaborn)
# hue adds a third dimension via color
sns.scatterplot(data=df, x="total_bill", y="tip", hue="day")

# Heatmap (Seaborn)
# Great for Correlation Matrices
corr = df.corr()
sns.heatmap(corr, annot=True, cmap='coolwarm')
```

---

### 4. Interactive Charts (Plotly)
High-level charts that allow hovering, zooming, and filtering.

```python
# Interactive Scatter Plot
fig = px.scatter(df, x="gdp", y="life_exp", size="pop", color="continent",
                 hover_name="country", log_x=True, size_max=60)
fig.show()

# Interactive Pie Chart
fig = px.pie(df, values='sales', names='city', title='Sales by City')
fig.show()
```

---

### 5. Figure Styling & Layouts
Controlling how your charts look.

```python
# Set global style (Seaborn)
sns.set_theme(style="whitegrid")

# Create Subplots (1 row, 2 columns)
fig, axes = plt.subplots(1, 2, figsize=(10, 4))
sns.histplot(df['col1'], ax=axes[0])
sns.histplot(df['col2'], ax=axes[1])

# Save Plot
plt.savefig('my_chart.png', dpi=300)
```
