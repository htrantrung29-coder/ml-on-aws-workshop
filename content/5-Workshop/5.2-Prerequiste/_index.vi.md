---
title: "5.2 Điều kiện tiên quyết"
date: 2026-07-31
weight: 2
chapter: false
pre: "<b>5.2 </b>"
---

## Tài khoản AWS

- Tài khoản AWS (có thể sử dụng Free Tier hoặc tài khoản sinh viên).
- Region: `ap-southeast-2` (Sydney).

## Quyền IAM tối thiểu

Tạo IAM Role với các policy sau:

| Policy | Mục đích |
|--------|---------|
| `AmazonSageMakerFullAccess` | Quyền đầy đủ trên SageMaker |
| `AmazonS3FullAccess` | Đọc/ghi trên S3 |
| `CloudWatchFullAccess` | Ghi logs và metrics |
| `AWSLambdaFullAccess` | Tạo và quản lý Lambda |
| `AmazonAPIGatewayAdministrator` | Quản lý API Gateway |

## Kiến thức cần có

- Python cơ bản (pandas, numpy, joblib).
- Hiểu biết cơ bản về Machine Learning.
- Quen thuộc với AWS Console.

## Công cụ cần cài đặt

| Công cụ | Phiên bản | Mục đích |
|---------|-----------|----------|
| AWS CLI | v2 | Tương tác với AWS từ command line |
| Python | 3.12+ | Chạy code và notebook |
| Git | Latest | Quản lý source code |

## Cấu trúc thư mục

Tạo cấu trúc thư mục sau trong S3 bucket `sagemaker-ap-southeast-2-921736623375`:
s3://sagemaker-ap-southeast-2-921736623375/
├── data/
│ ├── raw/ # Dữ liệu thô
│ └── processed/ # Dữ liệu đã xử lý
├── models/ # Model artifacts
├── outputs/ # Output từ các job
├── monitoring/ # Baseline và reports
│ ├── baseline/
│ └── captured-data/
├── registry/ # Model registry metadata
└── pipeline/ # Pipeline artifacts

## Lưu ý về quota

Do tài khoản sinh viên thường bị giới hạn quota, workshop này sử dụng **local mode** (chạy trong notebook) thay vì SageMaker Processing Jobs và Training Jobs. Các bước vẫn đảm bảo tính tương đương về kết quả.
