---
title: "Tuần 5: Quản lý phiên bản mô hình (Model Versioning)"
date: 2026-07-31
weight: 5
chapter: false
pre: "<b>1.5 </b>"
---

#### Công việc đã làm
- Do quota SageMaker Model Registry bị giới hạn (ResourceLimitExceeded), thực hiện quản lý phiên bản thủ công.
- Tạo file `registry/model_registry.json` lưu metadata:
  - Version 1 (HPO Best): accuracy 84.92%, approved.
  - Version 2 (Baseline): accuracy 83.80%, rejected.
- Metadata bao gồm: accuracy, hyperparameters, S3 path, timestamp.
- Upload file JSON lên S3 (`registry/`).

#### Kết quả đạt được
- ✅ Có 2 phiên bản model được ghi nhận rõ ràng.
- ✅ Metadata đầy đủ.
- ✅ Sẵn sàng cho quy trình deploy.
