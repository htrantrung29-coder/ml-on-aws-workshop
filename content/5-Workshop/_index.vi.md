---
title: "Workshop"
date: 2026-07-31
weight: 5
chapter: true
pre: "<b>5. </b>"
---

# Workshop: Xây dựng hệ thống ML End-to-End trên AWS

Trong phần này, chúng ta sẽ đi qua từng bước xây dựng một hệ thống Machine Learning hoàn chỉnh trên AWS, từ xử lý dữ liệu, huấn luyện mô hình, triển khai API, đến giám sát và tự động hóa pipeline.

## Tổng quan Workshop

| Phần | Nội dung |
|------|---------|
| 5.1 Overview | Giới thiệu và mục tiêu |
| 5.2 Prerequisites | Tài khoản AWS, IAM, công cụ |
| 5.3 Setup | IAM, S3, SageMaker Studio, config.py |
| 5.4 Data Processing | Tải, xử lý và upload dữ liệu |
| 5.5 Training | XGBoost baseline + HPO |
| 5.6 Model Registry | Quản lý version qua JSON |
| 5.7 Deployment | Endpoint + Lambda + API Gateway |
| 5.8 Monitoring | CloudWatch Alarms + Model Monitor |
| 5.9 Pipeline | Tự động hóa end-to-end |
| 5.10 Cleanup | Xóa resource để tránh phát sinh chi phí |

## Kết quả chính

- ✅ Baseline Accuracy: **83.80%**
- ✅ Best Accuracy (HPO): **84.92%**
- ✅ REST API với Lambda + API Gateway
- ✅ CloudWatch Alarms + Model Monitor
- ✅ End-to-end Pipeline Automation
