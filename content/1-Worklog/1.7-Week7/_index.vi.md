---
title: "Tuần 7: Giám sát hệ thống (Monitoring)"
date: 2026-07-31
weight: 7
chapter: false
pre: "<b>1.7 </b>"
---

#### Công việc đã làm
- Tạo 2 CloudWatch Alarms:
  - `titanic-endpoint-errors`: cảnh báo khi có lỗi 5XX.
  - `titanic-endpoint-latency`: cảnh báo khi latency > 1 giây.
- Gửi 20 requests đến Endpoint để tạo metrics và data capture.
- Tạo Model Monitor baseline sử dụng `ml.t3.xlarge` từ file `train.csv` (sinh ra `statistics.json` và `constraints.json`).
- Tạo Monitoring Schedule (`titanic-monitor-schedule`) chạy mỗi giờ để phát hiện data drift.

#### Kết quả đạt được
- ✅ CloudWatch Alarms ở trạng thái `OK`.
- ✅ Baseline files lưu tại `monitoring/baseline/`.
- ✅ Data Capture hoạt động, lưu request/payload tại `monitoring/captured-data/`.
- ✅ Monitoring Schedule được tạo thành công.
