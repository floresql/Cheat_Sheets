# Matplotlib & Seaborn Cheat Sheet: Data Visualization

### 1. Basic Plotting (Matplotlib)
The foundation for most Python visualizations.

```python
import matplotlib.pyplot as plt
import numpy as np

# Basic Line Plot
x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.plot(x, y, label='Sine Wave', color='blue', linestyle='--')
plt.title('My First Plot')
plt.xlabel('X Axis')
plt.ylabel('Y Axis')
plt.legend()
plt.grid(True)
plt.show()  # Display the plot
```

---

### 2. Statistical Visualization (Seaborn)
Built on top of Matplotlib for high-level, beautiful statistical graphics.

```python
import seaborn as sns
import pandas as pd

# Setting a theme
sns.set_theme(style="darkgrid")

# Load a built-in dataset
tips = sns.load_dataset("tips")

# Scatter Plot (with regression line)
sns.regplot(data=tips, x="total_bill", y="tip")

# Categorical Plot (Box Plot)
sns.boxplot(data=tips, x="day", y="total_bill", hue="smoker")

# Count Plot (Bar chart for frequencies)
sns.countplot(data=tips, x="time")
```

---

### 3. Distribution & Relationships
Visualizing how data is spread and how variables interact.

```python
# Histogram with Kernel Density Estimate (KDE)
sns.histplot(tips['total_bill'], kde=True, bins=20)

# Pairplot (Show relationships between all numeric columns)
sns.pairplot(tips, hue="sex")

# Heatmap (Correlation Matrix)
corr = tips.corr(numeric_only=True)
sns.heatmap(corr, annot=True, cmap='coolwarm')
```

---

### 4. Customizing Figure Size & Subplots
Controlling the layout of your visuals.

```python
# Single plot size
plt.figure(figsize=(10, 6))

# Subplots: 1 row, 2 columns
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

# Plot on the first subplot
sns.barplot(ax=axes[0], data=tips, x="day", y="tip")
axes[0].set_title("Tips by Day")

# Plot on the second subplot
sns.scatterplot(ax=axes[1], data=tips, x="total_bill", y="tip")
axes[1].set_title("Bill vs Tip")

plt.tight_layout() # Prevent overlapping labels
```

---

### 5. Saving Your Work
Exporting plots to files.

```python
plt.savefig('my_plot.png', dpi=300) # Save as high-res PNG
plt.savefig('my_plot.pdf')         # Save as PDF
```
