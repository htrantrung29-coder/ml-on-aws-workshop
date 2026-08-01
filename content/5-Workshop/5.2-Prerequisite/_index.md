---
title: "5.2 Prerequisites"
date: 2026-07-31
weight: 2
chapter: false
pre: "<b>5.2 </b>"
---

## AWS Account

- AWS account (Free Tier or student account is acceptable).
- Region: ap-southeast-2 (Sydney).

## Minimum IAM Permissions

Create an IAM Role with the following policies:

| Policy | Purpose |
|--------|---------|
| AmazonSageMakerFullAccess | Full SageMaker access |
| AmazonS3FullAccess | Read/write S3 |
| CloudWatchFullAccess | Write logs and metrics |
| AWSLambdaFullAccess | Create and manage Lambda |
| AmazonAPIGatewayAdministrator | Manage API Gateway |

## Required Knowledge

- Basic Python (pandas, numpy, joblib).
- Basic understanding of Machine Learning.
- Familiarity with AWS Console.

## Tools Required

| Tool | Version | Purpose |
|------|---------|---------|
| AWS CLI | v2 | Interact with AWS from command line |
| Python | 3.12+ | Run code and notebooks |
| Git | Latest | Source code management |

## S3 Folder Structure

Create the following folders in S3 bucket sagemaker-ap-southeast-2-921736623375:
- data/raw/ : raw data
- data/processed/ : processed data
- models/ : model artifacts
- outputs/ : job outputs
- monitoring/baseline/ : baseline files
- monitoring/captured-data/ : data capture
- registry/ : model registry metadata
- pipeline/ : pipeline artifacts

## Quota Considerations

Due to student account quota limits, this workshop uses local mode (running in notebook) instead of SageMaker Processing Jobs and Training Jobs. The results remain equivalent.
