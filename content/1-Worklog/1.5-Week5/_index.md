---
title: "Week 5: Model Versioning"
date: 2026-07-31
weight: 5
chapter: false
pre: "<b>1.5 </b>"
---

#### Tasks Done
- Due to SageMaker Model Registry quota limit (ResourceLimitExceeded), implemented manual versioning.
- Created `registry/model_registry.json` with metadata:
  - Version 1 (HPO Best): accuracy 84.92%, approved.
  - Version 2 (Baseline): accuracy 83.80%, rejected.
- Metadata includes: accuracy, hyperparameters, S3 path, timestamp.
- Uploaded JSON file to S3 (`registry/`).

#### Results
- ✅ 2 model versions clearly documented.
- ✅ Full metadata available.
- ✅ Ready for deployment workflow.
