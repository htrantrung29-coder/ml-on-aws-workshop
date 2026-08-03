---
title: "5.1 Project Overview"
date: 2026-07-31
weight: 1
chapter: false
pre: "<b>5.1 </b>"
---

## Introduction

This workshop guides you through building an end-to-end Machine Learning system on AWS using Amazon SageMaker, XGBoost, AWS Lambda, API Gateway, and Amazon CloudWatch.

## Problem Statement

Predict the survival probability of passengers on the Titanic based on features such as:
- Pclass (ticket class)
- Sex
- Age
- Number of siblings/spouses (SibSp)
- Number of parents/children (Parch)
- Fare
- Port of embarkation (Embarked)

## Objectives

- Build an automated data pipeline.
- Train and optimize an XGBoost model.
- Deploy a REST API for real-time predictions.
- Set up monitoring and alerting.
- Automate the entire workflow via pipeline.

## System Architecture

Below is the overall architecture diagram of the system:

![System Architecture](https://htrantrung29-coder.github.io/ml-on-aws-workshop/images/architecture-diagram.png)


*The diagram illustrates the data flow from S3 → Processing → Training → Endpoint → API Gateway → Client, along with monitoring and governance components.*

## Key Components

| Component | Role |
|-----------|------|
| Amazon S3 (sagemaker-ap-southeast-2-921736623375) | Stores raw data, processed data, and model artifacts |
| SageMaker Studio | JupyterLab development environment |
| SageMaker Processing | Data processing and transformation (local mode in this workshop) |
| SageMaker Training | XGBoost model training (local mode) |
| SageMaker Endpoint | Real-time inference (titanic-survival-endpoint) |
| AWS Lambda | Wrapper to call endpoint, handle request/response |
| API Gateway | REST API endpoint /predict (https://41zys98x41.execute-api.ap-southeast-2.amazonaws.com/prod/predict) |
| CloudWatch | Logs, metrics, and alarms |
| SageMaker Model Registry | Model version management (manual) |
| IAM | Access management |

## Results

| Metric | Value |
|--------|-------|
| Baseline Accuracy | 83.80% |
| Best Accuracy (HPO) | 84.92% |
| Improvement | +1.12% |
| Endpoint Latency | < 200ms |
| API Availability | 99.9% |
