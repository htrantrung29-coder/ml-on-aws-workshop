---
title: "Tuần 9: Làm lại dự án với account mới (không dùng quota)"
date: 2026-07-31
weight: 9
chapter: false
pre: "<b>1.9 </b>"
---

#### Lý do
- Tài khoản AWS cũ bị mất quyền truy cập, không thể tiếp tục.
- Quyết định tạo account mới và làm lại toàn bộ dự án từ đầu.
- Thách thức: account mới vẫn là tài khoản sinh viên, không có quota cho SageMaker Training Job và Model Registry.

#### Công việc đã làm
- Tạo account AWS mới, thiết lập IAM, S3 bucket, SageMaker Studio.
- Clone lại toàn bộ code từ repo GitHub (config.py, preprocessing.py, train.py, inference.py, notebooks).
- Điều chỉnh code để **không sử dụng bất kỳ service nào yêu cầu quota cao**:
  - **Processing Job** → thay bằng xử lý dữ liệu local trong notebook.
  - **Training Job** → thay bằng huấn luyện local (vẫn dùng XGBoost).
  - **Model Registry** → thay bằng lưu metadata JSON trên S3.
  - **SageMaker Pipelines** → thay bằng Python function tự động hóa.
- Vẫn giữ nguyên các service có quota mặc định: Endpoint (`ml.t2.medium`), CloudWatch, Lambda, API Gateway.
- Chạy lại toàn bộ pipeline từ Week 1 đến Week 8 và xác nhận kết quả tương đương.

#### Kết quả đạt được
- ✅ Toàn bộ dự án được tái tạo thành công trên account mới.
- ✅ Accuracy vẫn đạt **84.92%**.
- ✅ Endpoint `titanic-survival-endpoint` hoạt động.
- ✅ API Gateway và Lambda vận hành bình thường.
- ✅ Tất cả artifacts được lưu trên S3.
- ✅ Quy trình không phụ thuộc vào quota đặc biệt, có thể tái sử dụng cho bất kỳ account sinh viên nào.

#### Bài học rút ra
- Luôn backup code và tài liệu lên GitHub để có thể khôi phục nhanh chóng.
- Khi bị giới hạn quota, cần linh hoạt chuyển sang các phương án thay thế (local execution, lưu metadata JSON, ...).
- Việc làm lại từ đầu giúp hiểu sâu hơn từng bước và tối ưu hóa quy trình.
