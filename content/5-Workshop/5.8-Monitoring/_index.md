---
title: "5.8 Monitoring"
date: 2026-07-31
weight: 8
chapter: false
pre: "<b>5.8 </b>"
---

## CloudWatch Alarms

Create 2 alarms to monitor the endpoint:

```python
import boto3
from config import region

cw_client = boto3.client("cloudwatch", region_name=region)
endpoint_name = "titanic-survival-endpoint"

# Alarm 1: 5XX Errors
cw_client.put_metric_alarm(
    AlarmName="titanic-endpoint-errors",
    AlarmDescription="Alert when endpoint has 5XX errors",
    MetricName="Invocation5XXErrors",
    Namespace="AWS/SageMaker",
    Statistic="Sum",
    Dimensions=[
        {"Name": "EndpointName", "Value": endpoint_name},
        {"Name": "VariantName", "Value": "AllTraffic"}
    ],
    Period=300,
    EvaluationPeriods=1,
    Threshold=1,
    ComparisonOperator="GreaterThanOrEqualToThreshold",
    TreatMissingData="notBreaching",
)
print("Alarm: titanic-endpoint-errors")

# Alarm 2: Latency
cw_client.put_metric_alarm(
    AlarmName="titanic-endpoint-latency",
    AlarmDescription="Alert when latency > 1s",
    MetricName="ModelLatency",
    Namespace="AWS/SageMaker",
    Statistic="Average",
    Dimensions=[
        {"Name": "EndpointName", "Value": endpoint_name},
        {"Name": "VariantName", "Value": "AllTraffic"}
    ],
    Period=300,
    EvaluationPeriods=1,
    Threshold=1000000,
    ComparisonOperator="GreaterThanOrEqualToThreshold",
    TreatMissingData="notBreaching",
)
print("Alarm: titanic-endpoint-latency")
```

## Send traffic to generate metrics

```python
import time
import boto3
from config import region

runtime = boto3.client("sagemaker-runtime", region_name=region)
endpoint_name = "titanic-survival-endpoint"

passengers = [
    [3,0,22,1,0,7.25,0,2,0,0],
    [1,1,38,1,0,71.28,1,2,0,2],
    [3,1,26,0,0,7.92,0,1,1,1],
]

print("Sending 20 requests...")
for i in range(20):
    p = passengers[i % len(passengers)]
    response = runtime.invoke_endpoint(
        EndpointName=endpoint_name,
        ContentType="text/csv",
        Body=",".join(str(x) for x in p),
    )
    prob = float(response["Body"].read().decode("utf-8"))
    print(f"[{i+1:2d}/20] {prob:.4f}")
    time.sleep(0.5)
print("Sent 20 requests!")
```

## SageMaker Model Monitor

```python
from sagemaker.model_monitor import DefaultModelMonitor
from sagemaker.model_monitor.dataset_format import DatasetFormat
from config import role, session, bucket

monitor = DefaultModelMonitor(
    role=role,
    instance_count=1,
    instance_type="ml.t3.xlarge",
    volume_size_in_gb=20,
    max_runtime_in_seconds=3600,
    sagemaker_session=session,
)

monitor.suggest_baseline(
    baseline_dataset=f"s3://sagemaker-ap-southeast-2-921736623375/data/processed/train.csv",
    dataset_format=DatasetFormat.csv(header=True),
    output_s3_uri=f"s3://sagemaker-ap-southeast-2-921736623375/monitoring/baseline/",
    wait=True,
)
print("Baseline created!")

# Create Monitoring Schedule
from sagemaker.model_monitor import CronExpressionGenerator

monitor.create_monitoring_schedule(
    monitor_schedule_name="titanic-monitor-schedule",
    endpoint_input=endpoint_name,
    output_s3_uri=f"s3://sagemaker-ap-southeast-2-921736623375/monitoring/reports/",
    statistics=f"s3://sagemaker-ap-southeast-2-921736623375/monitoring/baseline/statistics.json",
    constraints=f"s3://sagemaker-ap-southeast-2-921736623375/monitoring/baseline/constraints.json",
    schedule_cron_expression=CronExpressionGenerator.hourly(),
)
print("Monitoring Schedule created!")
```

## Results

- CloudWatch Alarms: OK
- Baseline files: `statistics.json`, `constraints.json`
- Monitoring Schedule: runs hourly
- Data Capture: 100% requests captured