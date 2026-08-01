---
title: "5.1 Tổng quan dự án"
date: 2026-07-31
weight: 1
chapter: false
pre: "<b>5.1 </b>"
---

## Giới thiệu

Workshop này hướng dẫn xây dựng một hệ thống Machine Learning end-to-end trên AWS sử dụng Amazon SageMaker, XGBoost, AWS Lambda, API Gateway và Amazon CloudWatch.

## Bài toán

Dự đoán khả năng sống sót của hành khách trên tàu Titanic dựa trên các đặc điểm như:
- Pclass (hạng vé)
- Giới tính
- Tuổi
- Số lượng anh chị em / vợ chồng (SibSp)
- Số lượng bố mẹ / con cái (Parch)
- Giá vé (Fare)
- Cảng lên tàu (Embarked)

## Mục tiêu

- Xây dựng data pipeline tự động xử lý dữ liệu.
- Huấn luyện và tối ưu mô hình XGBoost.
- Triển khai REST API cho dự đoán real-time.
- Thiết lập monitoring và alerting.
- Tự động hóa toàn bộ workflow bằng pipeline.

## Kiến trúc hệ thống

Dưới đây là sơ đồ kiến trúc tổng quan của hệ thống:

![Kiến trúc hệ thống](/images/architecture-diagram.png)

*Sơ đồ mô tả luồng dữ liệu từ S3 → Processing → Training → Endpoint → API Gateway → Client, cùng với các thành phần monitoring và governance.*

## Các thành phần chính

| Thành phần | Vai trò |
|------------|---------|
| Amazon S3 (sagemaker-ap-southeast-2-921736623375) | Lưu trữ dữ liệu thô, dữ liệu đã xử lý, và model artifacts |
| SageMaker Studio | Môi trường phát triển JupyterLab |
| SageMaker Processing | Xử lý và biến đổi dữ liệu (local mode trong workshop này) |
| SageMaker Training | Huấn luyện mô hình XGBoost (local mode) |
| SageMaker Endpoint | Real-time inference (titanic-survival-endpoint) |
| AWS Lambda | Wrapper gọi endpoint, xử lý request/response |
| API Gateway | REST API endpoint /predict (https://41zys98x41.execute-api.ap-southeast-2.amazonaws.com/prod/predict) |
| CloudWatch | Logs, metrics, và alarms |
| SageMaker Model Registry | Quản lý phiên bản mô hình (thủ công) |
| IAM | Quản lý quyền truy cập |

## Kết quả đạt được

| Metric | Giá trị |
|--------|---------|
| Baseline Accuracy | 83.80% |
| Best Accuracy (HPO) | 84.92% |
| Cải thiện | +1.12% |
| Endpoint Latency | < 200ms |
| API Availability | 99.9% |
