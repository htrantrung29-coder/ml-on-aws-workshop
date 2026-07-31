---
title: "Tuần 6: Triển khai Endpoint & API"
date: 2026-07-31
weight: 6
chapter: false
pre: "<b>1.6 </b>"
---

#### Công việc đã làm
- Viết `inference.py` (các hàm `model_fn`, `input_fn`, `predict_fn`, `output_fn`).
- Viết `requirements.txt` (xgboost).
- Chuyển model sang XGBoost native, đóng gói thành `model.tar.gz` và upload lên S3 (`models/`).
- Triển khai SageMaker Endpoint với instance `ml.t2.medium`, bật Data Capture.
- Tạo Lambda Function `titanic-predictor` (Python 3.12) wrapper gọi Endpoint.
- Tạo API Gateway `titanic-api` với method `POST /predict`, tích hợp Lambda.
- Test API với 3 kịch bản hành khách.

#### Kết quả đạt được
- ✅ Endpoint `titanic-survival-endpoint` ở trạng thái `InService`.
- ✅ Lambda Function hoạt động.
- ✅ API Gateway trả về JSON chính xác.
- ✅ Kết quả test:
  - Nam, hạng 3 (22t) → Không sống (0.188).
  - Nữ, hạng 1 (38t) → Sống (0.739).
  - Nữ, hạng 3 (26t) → Sống (0.500).
