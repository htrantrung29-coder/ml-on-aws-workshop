---
title: "Tuần 4: Tối ưu siêu tham số (HPO)"
date: 2026-07-31
weight: 4
chapter: false
pre: "<b>1.4 </b>"
---

#### Công việc đã làm
- Thiết kế Grid Search với 27 combinations (3×3×3) cho các tham số:
  - max_depth: [3, 5, 7]
  - n_estimators: [50, 100, 200]
  - learning_rate: [0.01, 0.1, 0.2]
- Chạy tuần tự 27 lần huấn luyện trong notebook, so sánh accuracy.
- Xác định bộ tham số tốt nhất:
  - max_depth = 3
  - n_estimators = 100
  - learning_rate = 0.01
- Huấn luyện lại với best params, đạt accuracy **84.92%**.
- Lưu best_model.joblib lên S3 (models/).
- Log kết quả HPO vào SageMaker Experiments (titanic-hpo).

#### Kết quả đạt được
- ✅ Best Accuracy: **84.92%** (cải thiện +1.12% so với baseline).
- ✅ Đã so sánh và chọn được bộ tham số tối ưu.
