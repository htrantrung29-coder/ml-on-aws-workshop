---
title: "5.10 Clean Up"
date: 2026-07-31
weight: 10
chapter: false
pre: "<b>5.10 </b>"
---

## Important

Delete resources after the demo to avoid unexpected costs.

## Step 1: Delete Monitoring Schedule

```python
import boto3
from config import region

sm = boto3.client("sagemaker", region_name=region)

try:
    sm.delete_monitoring_schedule(
        MonitoringScheduleName="titanic-monitor-schedule"
    )
    print("Deleted monitoring schedule")
except Exception as e:
    print(f"Monitoring schedule not found: {e}")
```

## Step 2: Delete Endpoint

```python
try:
    sm.delete_endpoint(EndpointName="titanic-survival-endpoint")
    print("Deleted endpoint")
except Exception as e:
    print(f"Endpoint not found: {e}")

try:
    sm.delete_endpoint_config(EndpointConfigName="titanic-survival-endpoint")
    print("Deleted endpoint config")
except Exception as e:
    print(f"Endpoint config not found: {e}")
```

## Step 3: Delete Lambda & API Gateway

- Go to Lambda Console → select titanic-predictor → Delete.
- Go to API Gateway Console → select titanic-api → Delete.

## Step 4: Delete S3 (Optional)

```bash
aws s3 rm s3://sagemaker-ap-southeast-2-921736623375 --recursive
aws s3 rb s3://sagemaker-ap-southeast-2-921736623375
```

## Cost Savings

| Resource | Cost/hour | Savings |
|----------|----------:|---------:|
| SageMaker Endpoint (ml.t2.medium) | $0.065 | $0.065/hour |
| SageMaker Studio | $0.044 | $0.044/hour |
| Total | ~$0.11/hour | ~$2.64/day |
