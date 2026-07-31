---
title: "Tuần 9: Làm lại từ đầu với tài khoản mới"
date: 2026-07-31
weight: 9
chapter: false
pre: "<b>1.9 </b>"
---

#### Lý do
- Tài khoản AWS cũ bị mất (quên mật khẩu / bị khóa), không thể truy cập để hoàn thiện báo cáo và demo.
- Quyết định tạo một tài khoản mới và làm lại toàn bộ các bước từ đầu, tập trung vào việc **không sử dụng các dịch vụ yêu cầu quota cao** (Processing Job, Training Job, Pipelines) để đảm bảo có thể chạy thành công.

#### Công việc đã làm
- Đăng ký tài khoản AWS mới (free tier).
- Lặp lại các bước setup từ Tuần 1:
  - Tạo IAM Role với các policy cần thiết.
  - Tạo S3 Bucket mới, tạo các thư mục `data/`, `models/`, `outputs/`.
  - Khởi tạo SageMaker Studio và JupyterLab.
  - Tạo lại file `config.py` với thông tin bucket mới.
- Chạy lại toàn bộ các notebook từ Tuần 2 → 8, điều chỉnh code để hoạt động hoàn toàn trong **local mode** (không dùng Processing Job, Training Job, Pipelines của SageMaker).
- Kiểm tra lại kết quả và đảm bảo các số liệu khớp với lần chạy trước:
  - Baseline accuracy: 83.80%
  - Best accuracy: 84.92%
  - Endpoint hoạt động, API trả về đúng dự đoán.
- Cập nhật lại các file báo cáo trên GitHub với thông tin account mới (bucket name, region, endpoint URL).

#### Kết quả đạt được
- ✅ Tài khoản mới hoạt động ổn định.
- ✅ Tất cả các bước đều được thực hiện thành công mà không gặp lỗi quota.
- ✅ Các số liệu accuracy và kết quả test API hoàn toàn khớp với lần chạy đầu.
- ✅ Báo cáo được cập nhật và sẵn sàng cho demo.
