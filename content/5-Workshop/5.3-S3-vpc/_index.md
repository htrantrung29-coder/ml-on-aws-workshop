---
title: "5.3 Environment Setup"
date: 2026-07-31
weight: 3
chapter: false
pre: "<b>5.3 </b>"
---

## Step 1: Create IAM Role

1. Go to **IAM Console** $\rightarrow$ **Roles** $\rightarrow$ **Create role**.
2. Choose **AWS service** $\rightarrow$ **SageMaker** $\rightarrow$ **SageMaker - Execution**.
3. Attach policies: `AmazonSageMakerFullAccess`, `AmazonS3FullAccess`, `CloudWatchFullAccess`.
4. Name: `SageMakerExecutionRole`.
5. Click **Create role**.

---

## Step 2: Create S3 Bucket

1. Go to **S3 Console** $\rightarrow$ **Create bucket**.
2. Fill in:
   - **Bucket name:** `sagemaker-ap-southeast-2-921736623375`
   - **Region:** `ap-southeast-2`
3. Create folders: `data/`, `models/`, `outputs/`, `monitoring/`, `registry/`, `pipeline/`.

---

## Step 3: Launch SageMaker Studio

1. Go to **SageMaker Console** $\rightarrow$ **Studio**.
2. Click **Set up for single user (Quick setup)**.
3. Select **Execution role** as `SageMakerExecutionRole`.
4. Click **Submit** and wait 3-5 minutes.

---

## Step 4: Create config.py

In JupyterLab, create file `config.py`:

```python
import boto3
import sagemaker

session = sagemaker.Session()
role = sagemaker.get_execution_role()
region = boto3.Session().region_name
bucket = "sagemaker-ap-southeast-2-921736623375"

print(f"Region : {region}")
print(f"Role : {role}")
print(f"Bucket : {bucket}")
```
Step 5: Verify Setup
Run the following cell to check the connection:

```
from config import session, role, region, bucket

print(f"Region : {region}")
print(f"Role : {role}")
print(f"Bucket : {bucket}")
```
Expected output:
```
Region : ap-southeast-2
Role : arn:aws:iam::921736623375:role/SageMakerExecutionRole
Bucket : sagemaker-ap-southeast-2-921736623375
