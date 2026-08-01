---
title: "Đề xuất dự án"
date: 2026-07-31
weight: 2
chapter: false
pre: "<b>2. </b>"
---

# Machine Learning on AWS

## 1. Tổng quan

Xây dựng hệ thống Machine Learning end-to-end trên AWS sử dụng Amazon SageMaker làm nền tảng chính, với bài toán dự đoán khả năng sống sót trên tàu Titanic làm use-case thực nghiệm.

## 2. Mục tiêu

### Mục tiêu kỹ thuật

- Xây dựng data pipeline tự động với SageMaker Processing Jobs.
- Huấn luyện và tối ưu model XGBoost đạt Accuracy ≥ 83%.
- Triển khai REST API production-ready với latency < 1 giây.
- Thiết lập monitoring tự động phát hiện data drift.

### Mục tiêu học tập

- Nắm vững AWS Machine Learning Ecosystem.
- Hiểu quy trình Machine Learning end-to-end trên AWS.
- Thực hành các kỹ thuật MLOps.

---

## 3. Vấn đề cần giải quyết

| Vấn đề | Giải pháp |
|--------|-----------|
| Deploy ML model phức tạp | Amazon SageMaker Endpoint |
| Không có version control model | SageMaker Model Registry |
| Khó tái lập kết quả | SageMaker Experiments |
| Không giám sát sau triển khai | CloudWatch + Model Monitor |
| Pipeline thủ công | SageMaker Pipelines |

---

## 4. Kiến trúc giải pháp

![Kiến trúc hệ thống](/images/architecture-diagram.png)

---

## 5. Timeline

| Tuần | Nội dung | Deliverable |
|------|----------|-------------|
| 1 | Setup môi trường | IAM, S3, SageMaker Studio |
| 2 | Data Processing | train.csv, test.csv |
| 3 | Model Training | model.joblib |
| 4 | Hyperparameter Tuning | best_model.joblib |
| 5 | Model Registry | 2 Model Versions |
| 6 | Deploy & API | REST Endpoint |
| 7 | Monitoring | CloudWatch Alarms |
| 8 | Pipeline Automation | SageMaker Pipeline |

---

## 6. Ngân sách ước tính

| Dịch vụ | Đơn giá | Thời gian | Chi phí |
|----------|---------|-----------|----------|
| SageMaker Studio | \$0.044/giờ | 8 tuần × 4 giờ | ~\$14 |
| SageMaker Endpoint | \$0.065/giờ | 2 tuần × 8 giờ | ~\$10 |
| Amazon S3 | \$0.023/GB | 1 GB | ~\$0.02 |
| Lambda + API Gateway | Free Tier | - | \$0 |
| **Tổng** | | | **~\$24** |

---

## 7. Rủi ro và giải pháp

| Rủi ro | Mức độ | Giải pháp |
|--------|---------|-----------|
| AWS Service Quota bị giới hạn | Cao | Huấn luyện cục bộ và mô phỏng kết quả |
| Chi phí vượt ngân sách | Thấp | Xóa Endpoint sau khi hoàn thành |
| Accuracy chưa đạt yêu cầu | Thấp | Sử dụng Hyperparameter Optimization |
| Endpoint gặp lỗi | Trung bình | CloudWatch Alarm + Retry |
| Data Drift | Trung bình | SageMaker Model Monitor |
