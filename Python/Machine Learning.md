# Scikit-Learn Machine Learning Cheat Sheet

### 1. Basic Workflow
```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# 1. Split Data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# 2. Scale Features
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

# 3. Train Model
model = LogisticRegression()
model.fit(X_train, y_train)

# 4. Predict & Evaluate
preds = model.predict(X_test)
print(f"Accuracy: {accuracy_score(y_test, preds)}")
```

### 2. Common Models
- **Regression:** `LinearRegression`, `RandomForestRegressor`
- **Classification:** `SVC`, `KNeighborsClassifier`
- **Clustering:** `KMeans`
