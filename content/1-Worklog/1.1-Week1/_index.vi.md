---
title: "Tuần 1: Setup môi trường AWS"
date: 2026-07-31
weight: 1
chapter: false
pre: "<b>1.1 </b>"
---

#### Công việc đã làm
- Tìm hiểu tổng quan ML workflow và các dịch vụ AWS ML.
- Tạo IAM Role (`SageMakerExecutionRole`) với các policy: `AmazonSageMakerFullAccess`, `AmazonS3FullAccess`, `CloudWatchFullAccess`.
- Tạo S3 Bucket tại region `ap-southeast-2` và tạo 3 thư mục: `data/`, `models/`, `outputs/`.
- Khởi tạo SageMaker Studio Domain và JupyterLab.
- Tạo file `config.py` để quản lý session, role, region và bucket dùng chung.

#### Kết quả đạt được
- ✅ IAM Role hoạt động.
- ✅ S3 Bucket: `sagemaker-ap-southeast-2-921736623375`.
- ✅ SageMaker Studio sẵn sàng.
- ✅ File `config.py` kết nối thành công.
