---
title: "5.6 Model Registry"
date: 2026-07-31
weight: 6
chapter: false
pre: "<b>5.6 </b>"
---

## Giới thiệu

Do quota SageMaker Model Registry bị giới hạn, chúng ta quản lý phiên bản mô hình bằng file JSON thủ công.

## Tạo file model_registry.json

```json
{
  "model_group": "titanic-survival-models",
  "versions": [
    {
      "version": 1,
      "status": "approved",
      "model_name": "HPO Best",
      "accuracy": 0.8492,
      "max_depth": 3,
      "n_estimators": 100,
      "learning_rate": 0.01,
      "s3_path": "s3://sagemaker-ap-southeast-2-921736623375/models/best_model.joblib",
      "created_at": "2026-07-31"
    },
    {
      "version": 2,
      "status": "rejected",
      "model_name": "Baseline",
      "accuracy": 0.8380,
      "max_depth": 5,
      "n_estimators": 100,
      "learning_rate": 0.1,
      "s3_path": "s3://sagemaker-ap-southeast-2-921736623375/models/model.joblib",
      "created_at": "2026-07-30"
    }
  ]
}
```

## Upload lên S3

```python
import json
import boto3
from config import bucket

registry_data = {
    "model_group": "titanic-survival-models",
    "versions": [
        {
            "version": 1,
            "status": "approved",
            "model_name": "HPO Best",
            "accuracy": 0.8492,
            "max_depth": 3,
            "n_estimators": 100,
            "learning_rate": 0.01,
            "s3_path": f"s3://{bucket}/models/best_model.joblib",
            "created_at": "2026-07-31"
        },
        {
            "version": 2,
            "status": "rejected",
            "model_name": "Baseline",
            "accuracy": 0.8380,
            "max_depth": 5,
            "n_estimators": 100,
            "learning_rate": 0.1,
            "s3_path": f"s3://{bucket}/models/model.joblib",
            "created_at": "2026-07-30"
        }
    ]
}

with open("model_registry.json", "w") as f:
    json.dump(registry_data, f, indent=2)

s3 = boto3.client("s3")
s3.upload_file("model_registry.json", bucket, "registry/model_registry.json")
print(f"Uploaded: s3://{bucket}/registry/model_registry.json")
```

## Kết quả

| Version | Model | Accuracy | Status |
|---------|-------|----------|--------|
| v1 | HPO Best | 84.92% | Approved |
| v2 | Baseline | 83.80% | Rejected |
