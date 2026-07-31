---
title: "5.10 Dọn dẹp tài nguyên"
date: 2026-07-31
weight: 10
chapter: false
pre: "<b>5.10 </b>"
---

## Quan trọng

Xóa các resource sau khi demo để **tránh phát sinh chi phí**.

## Bước 1: Xóa Monitoring Schedule

```python
import boto3
from config import region

sm = boto3.client("sagemaker", region_name=region)

try:
    sm.delete_monitoring_schedule(
        MonitoringScheduleName="titanic-monitor-schedule"
    )
    print("Đã xóa monitoring schedule")
except Exception as e:
    print(f"Không tìm thấy monitoring schedule: {e}")
```

## Bước 2: Xóa Endpoint

```python
try:
    sm.delete_endpoint(EndpointName="titanic-survival-endpoint")
    print("Đã xóa endpoint")
except Exception as e:
    print(f"Không tìm thấy endpoint: {e}")

try:
    sm.delete_endpoint_config(EndpointConfigName="titanic-survival-endpoint")
    print("Đã xóa endpoint config")
except Exception as e:
    print(f"Không tìm thấy endpoint config: {e}")
```

## Bước 3: Xóa Lambda & API Gateway

- Vào **Lambda Console** → chọn **titanic-predictor** → **Delete**.
- Vào **API Gateway Console** → chọn **titanic-api** → **Delete**.

## Bước 4: Xóa S3 (tùy chọn)

```bash
aws s3 rm s3://sagemaker-ap-southeast-2-921736623375 --recursive
aws s3 rb s3://sagemaker-ap-southeast-2-921736623375
```

## Chi phí tiết kiệm

| Resource | Chi phí/giờ | Tiết kiệm |
|----------|------------:|----------:|
| SageMaker Endpoint (ml.t2.medium) | $0.065 | $0.065/giờ |
| SageMaker Studio | $0.044 | $0.044/giờ |
| **Tổng** | **~$0.11/giờ** | **~$2.64/ngày** |