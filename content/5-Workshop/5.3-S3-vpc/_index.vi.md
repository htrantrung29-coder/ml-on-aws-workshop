---
title: "5.3 Setup môi trường"
date: 2026-07-31
weight: 3
chapter: false
pre: "<b>5.3 </b>"
---

## Bước 1: Tạo IAM Role

1. Truy cập **IAM Console** → **Roles** → **Create role**.
2. Chọn **AWS service** → **SageMaker** → **SageMaker - Execution**.
3. Attach các policy: `AmazonSageMakerFullAccess`, `AmazonS3FullAccess`, `CloudWatchFullAccess`.
4. Đặt tên role: `SageMakerExecutionRole`.
5. Click **Create role**.

## Bước 2: Tạo S3 Bucket

1. Truy cập **S3 Console** → **Create bucket**.
2. Điền thông tin:
   - Bucket name: `sagemaker-ap-southeast-2-921736623375`
   - Region: `ap-southeast-2`
3. Tạo các thư mục: `data/`, `models/`, `outputs/`, `monitoring/`, `registry/`, `pipeline/`.

## Bước 3: Khởi tạo SageMaker Studio

1. Truy cập **SageMaker Console** → **Studio**.
2. Click **Set up for single user (Quick setup)**.
3. Chọn **Execution role** là `SageMakerExecutionRole`.
4. Click **Submit** và đợi 3-5 phút.

## Bước 4: Tạo config.py

Trong JupyterLab, tạo file `config.py`:
import boto3
import sagemaker

session = sagemaker.Session()
role = sagemaker.get_execution_role()
region = boto3.Session().region_name
bucket = "sagemaker-ap-southeast-2-921736623375"

print(f"Region : {region}")
print(f"Role : {role}")
print(f"Bucket : {bucket}")

Bước 5: Verify Setup
Chạy cell sau để kiểm tra kết nối:
python
from config import session, role, region, bucket

print(f"Region : {region}")
print(f"Role : {role}")
print(f"Bucket : {bucket}")
Kết quả mong đợi:

text
Region : ap-southeast-2
Role : arn:aws:iam::921736623375:role/SageMakerExecutionRole
Bucket : sagemaker-ap-southeast-2-921736623375
text

---
