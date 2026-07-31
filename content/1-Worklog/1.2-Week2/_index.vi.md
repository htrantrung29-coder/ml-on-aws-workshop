---
title: "Tuần 2: Xử lý dữ liệu (Data Processing) – Local mode"
date: 2026-07-31
weight: 2
chapter: false
pre: "<b>1.2 </b>"
---

#### Công việc đã làm
- Tải dataset Titanic (891 hành khách, 12 features) từ GitHub.
- Phân tích missing values: `Age` (177), `Cabin` (687), `Embarked` (2).
- Do quota SageMaker Processing Job bị giới hạn, thực hiện xử lý dữ liệu **trực tiếp trong notebook**.
- Các bước xử lý:
  - Điền missing values: `Age` (median), `Embarked` (mode).
  - Loại bỏ cột `Cabin`.
  - Feature Engineering: tạo `FamilySize`, `IsAlone`, trích xuất `Title` từ họ tên.
  - Encoding: `Sex` (0/1), `Embarked` (S/C/Q → 0/1/2), `Title` (Mr/Miss/Mrs/Master/Rare → 0-4).
  - Chọn 10 features và target `Survived`.
  - Chia Train/Test 80/20 (có stratify).
- Lưu `train.csv` và `test.csv`, upload lên S3 (`data/processed/`).

#### Kết quả đạt được
- ✅ Train: 712 rows, 11 columns; Test: 179 rows, 11 columns.
- ✅ 0 missing values.
- ✅ Upload thành công lên S3.
