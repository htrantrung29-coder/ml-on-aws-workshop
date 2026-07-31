---
title: "Đề xuất dự án"
date: 2026-07-31
weight: 2
chapter: true
pre: "<b>2. </b>"
---

# Đề xuất dự án: Machine Learning on AWS

## 1. Tổng quan
Xây dựng hệ thống Machine Learning end-to-end trên AWS với bài toán dự đoán khả năng sống sót trên tàu Titanic.

## 2. Mục tiêu
- Xây dựng data pipeline tự động.
- Huấn luyện và tối ưu model XGBoost đạt Accuracy ≥ 83%.
- Triển khai REST API production-ready.
- Thiết lập monitoring tự động phát hiện data drift.

## 3. Vấn đề cần giải quyết
| Vấn đề | Giải pháp |
|--------|----------|
| Deploy ML model phức tạp | SageMaker Endpoint |
| Không có version control model | SageMaker Model Registry |
| Khó reproduce kết quả | SageMaker Experiments |
| Không monitor sau deploy | CloudWatch + Model Monitor |
| Pipeline thủ công | SageMaker Pipelines |

## 4. Kiến trúc giải pháp
![Architecture](/images/architecture.png)

## 5. Timeline (8 tuần)
| Tuần | Nội dung | Deliverable |
|------|---------|-------------|
| 1 | Setup môi trường | IAM, S3, Studio |
| 2 | Data Processing | train.csv, test.csv |
| 3 | Model Training | model.joblib |
| 4 | HPO | best_model.joblib |
| 5 | Model Registry | 2 versions |
| 6 | Deploy + API | REST endpoint |
| 7 | Monitoring | Alarms + Schedule |
| 8 | Pipelines | End-to-end automation |

## 6. Ngân sách
| Service | Chi phí |
|---------|---------|
| SageMaker Endpoint | ~$0.065/h |
| S3 Storage | ~$0.023/GB |
| Lambda + API GW | Free tier |

## 7. Rủi ro & Giải pháp
| Rủi ro | Giải pháp |
|--------|----------|
| Quota bị giới hạn | Train local + document |
| Chi phí vượt budget | Xóa endpoint sau demo |
| Endpoint bị lỗi | CloudWatch alarm + retry |
| Data drift | Model Monitor schedule |
