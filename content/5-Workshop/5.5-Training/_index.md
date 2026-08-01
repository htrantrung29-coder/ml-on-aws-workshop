---
title: "5.5 Model Training"
date: 2026-07-31
weight: 5
chapter: false
pre: "<b>5.5 </b>"
---

## Baseline Model

Using XGBoost with default parameters:

| Parameter | Value |
|-----------|-------|
| max_depth | 5 |
| n_estimators | 100 |
| learning_rate | 0.1 |
| eval_metric | logloss |

## Training Code

```python
import xgboost as xgb
from sklearn.metrics import accuracy_score, classification_report
import joblib
import boto3
from config import bucket
import pandas as pd

# Load data
train_df = pd.read_csv(f"s3://sagemaker-ap-southeast-2-921736623375/data/processed/train.csv")
test_df = pd.read_csv(f"s3://sagemaker-ap-southeast-2-921736623375/data/processed/test.csv")

FEATURES = ["Pclass","Sex","Age","SibSp","Parch","Fare","Embarked","FamilySize","IsAlone","Title"]
TARGET = "Survived"

X_train, y_train = train_df[FEATURES], train_df[TARGET]
X_test, y_test = test_df[FEATURES], test_df[TARGET]

# Train baseline
model = xgb.XGBClassifier(
    max_depth=5,
    n_estimators=100,
    learning_rate=0.1,
    eval_metric="logloss",
    random_state=42,
)
model.fit(X_train, y_train, eval_set=[(X_test, y_test)], verbose=10)

y_pred = model.predict(X_test)
acc = accuracy_score(y_test, y_pred)

print(f"Baseline Accuracy: {acc:.4f}")
print(classification_report(y_test, y_pred, target_names=["Not Survived", "Survived"]))
```

## Hyperparameter Optimization (HPO)

Grid Search with 27 combinations:

| Parameter | Test Values |
|-----------|-------------|
| max_depth | [3, 5, 7] |
| n_estimators | [50, 100, 200] |
| learning_rate | [0.01, 0.1, 0.2] |

```python
import itertools

param_grid = {
    "max_depth": [3, 5, 7],
    "n_estimators": [50, 100, 200],
    "learning_rate": [0.01, 0.1, 0.2],
}

all_params = list(itertools.product(
    param_grid["max_depth"],
    param_grid["n_estimators"],
    param_grid["learning_rate"]
))

results = []
for max_depth, n_estimators, learning_rate in all_params:
    model = xgb.XGBClassifier(
        max_depth=max_depth,
        n_estimators=n_estimators,
        learning_rate=learning_rate,
        eval_metric="logloss",
        random_state=42,
        verbosity=0,
    )
    model.fit(X_train, y_train)
    acc = accuracy_score(y_test, model.predict(X_test))
    results.append({
        "max_depth": max_depth,
        "n_estimators": n_estimators,
        "learning_rate": learning_rate,
        "accuracy": round(acc, 4),
    })
```

## Results

| Model | Accuracy | max_depth | n_estimators | learning_rate |
|-------|----------|-----------|--------------|---------------|
| HPO Best | 84.92% | 3 | 100 | 0.01 |
| Baseline | 83.80% | 5 | 100 | 0.1 |

Save best model:

```python
best_model = xgb.XGBClassifier(
    max_depth=3,
    n_estimators=100,
    learning_rate=0.01,
    eval_metric="logloss",
    random_state=42,
)
best_model.fit(X_train, y_train)
joblib.dump(best_model, "best_model.joblib")
boto3.client("s3").upload_file("best_model.joblib", bucket, "models/best_model.joblib")
print(f"Best model saved: s3://sagemaker-ap-southeast-2-921736623375/models/best_model.joblib")
```
