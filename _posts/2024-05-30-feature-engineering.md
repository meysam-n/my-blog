---
title: "Feature Engineering: The Art of ML Data Preparation"
description: "Master the techniques that transform raw data into powerful model features."
date: 2024-05-30
categories: [Machine Learning]
tags: [feature-engineering, data-science, preprocessing, machine-learning]
---

Feature engineering is often the difference between a mediocre model and a great one. It's where domain knowledge meets data science.

## What Is Feature Engineering?

Feature engineering is the process of using domain knowledge to create features that make machine learning algorithms work better.

## Handling Missing Values

```python
import pandas as pd

# Fill with mean/median/mode
df['age'].fillna(df['age'].median(), inplace=True)

# Fill with a constant
df['category'].fillna('Unknown', inplace=True)

# Create a "missing" indicator
df['age_missing'] = df['age'].isna().astype(int)
```

## Encoding Categorical Variables

### One-Hot Encoding

```python
pd.get_dummies(df['color'], prefix='color')
# Result: color_red, color_blue, color_green
```

### Label Encoding

```python
from sklearn.preprocessing import LabelEncoder
le = LabelEncoder()
df['size_encoded'] = le.fit_transform(df['size'])
```

## Scaling and Normalization

```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler

# StandardScaler: Mean = 0, Std = 1
scaler = StandardScaler()
df['age_scaled'] = scaler.fit_transform(df[['age']])

# MinMaxScaler: Range [0, 1]
scaler = MinMaxScaler()
df['age_normalized'] = scaler.fit_transform(df[['age']])
```

## Creating New Features

### Date/Time Features

```python
df['date'] = pd.to_datetime(df['date'])
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day_of_week'] = df['date'].dt.dayofweek
df['is_weekend'] = df['day_of_week'].isin([5, 6]).astype(int)
```

## Feature Selection

```python
from sklearn.ensemble import RandomForestClassifier

rf = RandomForestClassifier()
rf.fit(X, y)

importance = pd.DataFrame({
    'feature': X.columns,
    'importance': rf.feature_importances_
}).sort_values('importance', ascending=False)
```

## Conclusion

Good feature engineering requires both technical skills and domain expertise. Invest time in understanding your data, and your models will reward you with better performance.
