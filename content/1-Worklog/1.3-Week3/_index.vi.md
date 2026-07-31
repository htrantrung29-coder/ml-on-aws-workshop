---
title: "Tuần 3: Huấn luyện mô hình (Training) – Local mode"
date: 2026-07-31
weight: 3
chapter: false
pre: "<b>1.3 </b>"
---

#### Công việc đã làm
- Viết script train.py cho XGBoost, hỗ trợ truyền hyperparameters qua argparse.
- Do quota SageMaker Training Job (ml.m5.large = 0), thực hiện huấn luyện **trực tiếp trong notebook**.
- Huấn luyện baseline với:
  - max_depth = 5
  - n_estimators = 100
  - learning_rate = 0.1
- Đánh giá mô hình trên tập test.
- Log experiment vào SageMaker Experiments (titanic-training).
- Lưu model.joblib lên S3 (models/).

#### Kết quả đạt được
- ✅ Baseline Accuracy: **83.80%**.
- ✅ Precision (Không sống/Sống sót): 0.85 / 0.82.
- ✅ Recall: 0.90 / 0.74.
- ✅ Model artifact lên S3.
