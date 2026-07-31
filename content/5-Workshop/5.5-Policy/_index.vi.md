---
title: "5.5 Huấn luyện mô hình"
date: 2026-07-31
weight: 5
chapter: false
pre: "<b>5.5 </b>"
---

# 5.5 Huấn luyện mô hình

## Baseline Model

Mô hình ban đầu sử dụng **XGBoost** với các siêu tham số mặc định như sau:

| Tham số | Giá trị |
|----------|----------|
| `max_depth` | 5 |
| `n_estimators` | 100 |
| `learning_rate` | 0.1 |
| `eval_metric` | `logloss` |

## Huấn luyện Baseline Model

```python
import xgboost as xgb
from sklearn.metrics import accuracy_score, classification_report
import joblib
import boto3
from config import bucket
import pandas as pd

# Load dataset
train_df = pd.read_csv(
    "s3://sagemaker-ap-southeast-2-921736623375/data/processed/train.csv"
)
test_df = pd.read_csv(
    "s3://sagemaker-ap-southeast-2-921736623375/data/processed/test.csv"
)

FEATURES = [
    "Pclass",
    "Sex",
    "Age",
    "SibSp",
    "Parch",
    "Fare",
    "Embarked",
    "FamilySize",
    "IsAlone",
    "Title",
]

TARGET = "Survived"

X_train = train_df[FEATURES]
y_train = train_df[TARGET]

X_test = test_df[FEATURES]
y_test = test_df[TARGET]

# Baseline model
model = xgb.XGBClassifier(
    max_depth=5,
    n_estimators=100,
    learning_rate=0.1,
    eval_metric="logloss",
    random_state=42,
)

model.fit(
    X_train,
    y_train,
    eval_set=[(X_test, y_test)],
    verbose=10,
)

# Evaluation
y_pred = model.predict(X_test)
acc = accuracy_score(y_test, y_pred)

print(f"Baseline Accuracy: {acc:.4f}")
print(
    classification_report(
        y_test,
        y_pred,
        target_names=["Không sống", "Sống sót"],
    )
)
```

---

# Hyperparameter Optimization (HPO)

Để cải thiện hiệu năng của mô hình, tiến hành **Grid Search** trên 27 tổ hợp siêu tham số.

## Không gian tìm kiếm

| Tham số | Giá trị thử nghiệm |
|----------|--------------------|
| `max_depth` | `[3, 5, 7]` |
| `n_estimators` | `[50, 100, 200]` |
| `learning_rate` | `[0.01, 0.1, 0.2]` |

Tổng số tổ hợp:

\[
3 \times 3 \times 3 = 27
\]

## Code Grid Search

```python
import itertools
import xgboost as xgb
from sklearn.metrics import accuracy_score

param_grid = {
    "max_depth": [3, 5, 7],
    "n_estimators": [50, 100, 200],
    "learning_rate": [0.01, 0.1, 0.2],
}

all_params = list(
    itertools.product(
        param_grid["max_depth"],
        param_grid["n_estimators"],
        param_grid["learning_rate"],
    )
)

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

    acc = accuracy_score(
        y_test,
        model.predict(X_test),
    )

    results.append(
        {
            "max_depth": max_depth,
            "n_estimators": n_estimators,
            "learning_rate": learning_rate,
            "accuracy": round(acc, 4),
        }
    )
```

---

# Kết quả

Sau khi thử nghiệm 27 tổ hợp siêu tham số, mô hình có kết quả tốt nhất như sau:

| Model | Accuracy | max_depth | n_estimators | learning_rate |
|--------|----------|-----------|--------------|----------------|
| **HPO Best** | **84.92%** | 3 | 100 | 0.01 |
| Baseline | 83.80% | 5 | 100 | 0.10 |

So với mô hình Baseline, việc tối ưu siêu tham số giúp tăng độ chính xác từ **83.80%** lên **84.92%**, tương ứng tăng khoảng **1.12%**.

---

# Lưu mô hình tốt nhất

Sau khi xác định được bộ siêu tham số tối ưu, mô hình được huấn luyện lại trên tập huấn luyện và lưu dưới dạng `joblib`, sau đó tải lên Amazon S3.

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

boto3.client("s3").upload_file(
    "best_model.joblib",
    bucket,
    "models/best_model.joblib",
)

print(
    "Best model saved: "
    "s3://sagemaker-ap-southeast-2-921736623375/models/best_model.joblib"
)
```

Sau bước này, mô hình tối ưu được lưu tại:

```text
s3://sagemaker-ap-southeast-2-921736623375/models/best_model.joblib
```

và sẵn sàng được sử dụng cho các bước triển khai (deployment) hoặc suy luận (inference).
