---
title: "Week 6: Endpoint & API Deployment"
date: 2026-07-31
weight: 6
chapter: false
pre: "<b>1.6 </b>"
---

#### Tasks Done
- Wrote `inference.py` (with `model_fn`, `input_fn`, `predict_fn`, `output_fn`).
- Wrote `requirements.txt` (xgboost).
- Converted model to XGBoost native, packaged as `model.tar.gz`, uploaded to S3 (`models/`).
- Deployed SageMaker Endpoint with `ml.t2.medium` instance, enabled Data Capture.
- Created Lambda Function `titanic-predictor` (Python 3.12) to wrap Endpoint.
- Created API Gateway `titanic-api` with `POST /predict` method, integrated with Lambda.
- Tested API with 3 passenger scenarios.

#### Results
- ✅ Endpoint `titanic-survival-endpoint` in `InService` state.
- ✅ Lambda Function working.
- ✅ API Gateway returns correct JSON.
- ✅ Test results:
  - Male, 3rd class (22yo) → Did not survive (0.188).
  - Female, 1st class (38yo) → Survived (0.739).
  - Female, 3rd class (26yo) → Survived (0.500).
