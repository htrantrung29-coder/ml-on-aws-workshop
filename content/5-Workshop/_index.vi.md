---
title: "Tự đánh giá"
date: 2026-07-31
weight: 6
chapter: true
pre: "<b>6. </b>"
---

# Tự đánh giá

Dưới đây là bảng tự đánh giá của tôi về quá trình thực tập và thực hiện dự án Machine Learning trên AWS. Các tiêu chí được đánh giá dựa trên mức độ hoàn thành công việc, khả năng thích ứng và đóng góp cho dự án chung.

## Bảng đánh giá

| Tiêu chí | Đánh giá | Nhận xét |
|----------|---------|---------|
| **Kiến thức** | **Khá** | Nắm vững các dịch vụ AWS cốt lõi như SageMaker, S3, Lambda, API Gateway. Hiểu được end-to-end ML workflow. Cần tìm hiểu thêm về SageMaker Feature Store và các advanced MLOps practices. |
| **Khả năng học hỏi** | **Tốt** | Tự nghiên cứu tài liệu AWS, debug các lỗi kỹ thuật (quota, health check, container). Nhanh chóng thích nghi khi gặp giới hạn tài nguyên và tìm được workaround phù hợp. |
| **Tính chủ động** | **Khá** | Chủ động tìm hiểu các service mới, đề xuất giải pháp khi gặp sự cố. Tuy nhiên, đôi khi cần hỗ trợ thêm để xử lý các vấn đề phức tạp về IAM và networking. |
| **Kỷ luật** | **Tốt** | Hoàn thành đúng tiến độ 8 tuần, ghi chép worklog và báo cáo đầy đủ. Duy trì tác phong làm việc nghiêm túc, có kế hoạch rõ ràng. |
| **Giao tiếp** | **Khá** | Báo cáo tiến độ đều đặn, đặt câu hỏi rõ ràng và mạch lạc khi gặp vấn đề. Có khả năng tổng hợp và trình bày kết quả một cách logic. |
| **Teamwork** | **Trung bình** | Vì đây là dự án cá nhân, khả năng làm việc nhóm chưa được thể hiện nhiều. Tuy nhiên, đã hỗ trợ các bạn đồng trang lứa khi gặp vấn đề tương tự về AWS setup. |
| **Giải quyết vấn đề** | **Tốt** | Gặp nhiều lỗi thực tế (quota, endpoint health check, Model Registry limit) nhưng đều tìm được cách giải quyết hoặc workaround hợp lý. Biết cách phân tích log và tìm nguyên nhân gốc rễ. |
| **Đóng góp cho dự án** | **Khá** | Hoàn thành 8 tuần đúng yêu cầu. Xây dựng được hệ thống ML end-to-end với accuracy 84.92%. Viết báo cáo chi tiết, có đầy đủ code và hướng dẫn để người khác có thể làm theo. |

## Khó khăn gặp phải và cách giải quyết

### 1. Quota SageMaker bị giới hạn
**Vấn đề:** Tài khoản sinh viên bị giới hạn quota cho Training Job, Processing Job, Model Registry và Pipelines.

**Giải pháp:** 
- Chạy training và processing trực tiếp trong JupyterLab (local mode).
- Quản lý phiên bản model thủ công bằng file JSON thay vì Model Registry.
- Xây dựng pipeline dạng Python function thay vì SageMaker Pipelines.

**Bài học:** Luôn kiểm tra quota trước khi bắt đầu và có plan B khi gặp giới hạn.

### 2. Endpoint Health Check Failure
**Vấn đề:** Container SKLearn không có sẵn thư viện `xgboost`, dẫn đến endpoint bị lỗi health check.

**Giải pháp:** Chuyển sang dùng XGBoost container chính thức của AWS thay vì SKLearn container.

**Bài học:** Luôn kiểm tra CloudWatch logs và chọn đúng container cho framework tương ứng.

### 3. Mất account AWS cũ
**Vấn đề:** Mất quyền truy cập vào account cũ, không thể tiếp tục hoàn thiện báo cáo và demo.

**Giải pháp:** Tạo account mới và làm lại toàn bộ các bước từ đầu, điều chỉnh code để không sử dụng các dịch vụ yêu cầu quota cao.

**Bài học:** Luôn sao lưu code và tài liệu, sử dụng IAM user thay vì root user.

## Hướng phát triển trong tương lai

- 🔜 Thử nghiệm với dataset lớn hơn (> 100K rows) để đánh giá khả năng mở rộng.
- 🔜 Tích hợp CI/CD với GitHub Actions để tự động deploy model khi có thay đổi.
- 🔜 Thực hiện A/B testing với nhiều model variants khác nhau trên cùng endpoint.
- 🔜 Khám phá SageMaker Feature Store để quản lý features tập trung.
- 🔜 Deploy multi-region để tăng độ sẵn sàng và giảm latency.
