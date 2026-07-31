---
title: "5. Workshop"
date: 2026-07-31
weight: 5
chapter: false
pre: "<b>5. </b>"
---

# Machine Learning on AWS với SageMaker

## Tổng quan

Workshop này hướng dẫn xây dựng hệ thống ML end-to-end trên AWS,
từ xử lý dữ liệu đến triển khai REST API production.

## Kiến trúc hệ thống

![Architecture](/images/5-Workshop/5.1-Workshop-overview/architecture.png)

## Các bước thực hiện

| Bước | Nội dung | Service |
|------|---------|---------|
| 1 | Setup môi trường | IAM, S3, SageMaker Studio |
| 2 | Xử lý dữ liệu | SageMaker Processing |
| 3 | Huấn luyện & HPO | XGBoost, Experiments |
| 4 | Model Registry | SageMaker Registry |
| 5 | Deploy & API | Endpoint, Lambda, API GW |
| 6 | Monitoring | CloudWatch, Model Monitor |
| 7 | Pipeline | SageMaker Pipelines |
| 8 | Cleanup | Xóa tài nguyên |
