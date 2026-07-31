---
title: "Tuần 8: Tự động hóa Pipeline"
date: 2026-07-31
weight: 8
chapter: false
pre: "<b>1.8 </b>"
---

#### Công việc đã làm
- Xây dựng pipeline dạng **Python function** (thay vì SageMaker Pipelines do quota) với 4 bước:
  1. **Data Processing**: Đọc raw data, xử lý, chia train/test.
  2. **Upload processed data**: Lưu train.csv và test.csv lên S3 (pipeline/processed/).
  3. **Training**: Huấn luyện XGBoost với tham số tối ưu (depth=3, n=100, lr=0.01).
  4. **Save model**: Đóng gói và upload model lên S3 (pipeline/models/).
- Gọi pipeline function và kiểm tra kết quả.

#### Kết quả đạt được
- ✅ Pipeline chạy tự động hoàn chỉnh.
- ✅ Accuracy đạt **84.92%** (khớp với HPO best).
- ✅ Model artifact lưu tại pipeline/models/model.tar.gz.
- ✅ Toàn bộ quy trình từ raw data → model → S3 được tự động hóa.
