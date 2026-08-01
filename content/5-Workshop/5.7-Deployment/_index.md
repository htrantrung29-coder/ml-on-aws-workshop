---
title: "5.7 Endpoint & API Deployment"
date: 2026-07-31
weight: 7
chapter: false
pre: "<b>5.7 </b>"
---

## Architecture

```text
Client
|
v
API Gateway (POST /predict)
|
v
AWS Lambda (titanic-predictor)
|
v
SageMaker Endpoint (titanic-survival-endpoint)
|
v
Prediction Result
```

## Step 1: Package Model

```python
import joblib
import tarfile
import boto3
from config import bucket

model = joblib.load("models/best_model.joblib")
model.save_model("xgboost-model")

with tarfile.open("model.tar.gz", "w:gz") as tar:
    tar.add("xgboost-model")

s3 = boto3.client("s3")
s3.upload_file("model.tar.gz", bucket, "models/model.tar.gz")
print(f"Uploaded: s3://sagemaker-ap-southeast-2-921736623375/models/model.tar.gz")
```

## Step 2: Deploy Endpoint

```python
from sagemaker.xgboost.model import XGBoostModel
from sagemaker.model_monitor import DataCaptureConfig
from config import role, session, bucket

data_capture = DataCaptureConfig(
    enable_capture=True,
    sampling_percentage=100,
    destination_s3_uri=f"s3://{bucket}/monitoring/captured-data/",
)

xgb_model = XGBoostModel(
    model_data=f"s3://{bucket}/models/model.tar.gz",
    role=role,
    framework_version="1.7-1",
    sagemaker_session=session,
)

predictor = xgb_model.deploy(
    initial_instance_count=1,
    instance_type="ml.t2.medium",
    endpoint_name="titanic-survival-endpoint",
    data_capture_config=data_capture,
)
print(f"Endpoint: titanic-survival-endpoint")
```

## Step 3: Create Lambda Function

```python
# Lambda Function code
import json
import boto3

runtime = boto3.client("sagemaker-runtime", region_name="ap-southeast-2")
ENDPOINT_NAME = "titanic-survival-endpoint"

def lambda_handler(event, context):
    try:
        body = json.loads(event["body"])
        features = body["features"]
        csv_input = ",".join(str(x) for x in features)

        response = runtime.invoke_endpoint(
            EndpointName=ENDPOINT_NAME,
            ContentType="text/csv",
            Body=csv_input,
        )

        prob = float(response["Body"].read().decode("utf-8"))
        prediction = 1 if prob > 0.5 else 0

        return {
            "statusCode": 200,
            "headers": {"Content-Type": "application/json"},
            "body": json.dumps({
                "prediction": prediction,
                "probability": round(prob, 4),
                "label": "Survived" if prediction == 1 else "Did not survive",
            })
        }
    except Exception as e:
        return {
            "statusCode": 500,
            "body": json.dumps({"error": str(e)})
        }
```

## Step 4: Create API Gateway

Go to API Gateway Console -> Create API -> REST API.

- API name: titanic-api.
- Create resource /predict with method POST.
- Integrate with Lambda function titanic-predictor.
- Deploy API with stage prod.

## Step 5: Test API

```python
import requests

url = "https://41zys98x41.execute-api.ap-southeast-2.amazonaws.com/prod/predict"

test_cases = [
    {"desc": "Male, 3rd class, 22t", "features": [3,0,22,1,0,7.25,0,2,0,0]},
    {"desc": "Female, 1st class, 38t", "features": [1,1,38,1,0,71.28,1,2,0,2]},
    {"desc": "Female, 3rd class, 26t", "features": [3,1,26,0,0,7.92,0,1,1,1]},
]

for case in test_cases:
    response = requests.post(url, json={"features": case["features"]})
    print(f"{case['desc']}: {response.json()}")
```

## Results

| Passenger | Pclass | Sex | Age | Prediction |
|-----------|--------|-----|-----|------------|
| Male, 3rd class, 22t | 3 | Male | 22 | Not survive (18.8%) |
| Female, 1st class, 38t | 1 | Female | 38 | Survive (73.9%) |
| Female, 3rd class, 26t | 3 | Female | 26 | Survive (50.1%) |
