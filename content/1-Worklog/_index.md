---
title: "Week 9: Rebuild Project with New Account (No Quota)"
date: 2026-07-31
weight: 9
chapter: false
pre: "<b>1.9 </b>"
---

#### Reason
- The old AWS account lost access, preventing continuation.
- Decision to create a new account and rebuild the entire project from scratch.
- Challenge: the new account is still a student account, with no quota for SageMaker Training Job and Model Registry.

#### Tasks Done
- Created a new AWS account, set up IAM, S3 bucket, SageMaker Studio.
- Cloned all code from GitHub repo (`config.py`, `preprocessing.py`, `train.py`, `inference.py`, notebooks).
- Modified code to **avoid using any high-quota services**:
  - **Processing Job** → replaced with local data processing in notebook.
  - **Training Job** → replaced with local training (XGBoost still used).
  - **Model Registry** → replaced with JSON metadata stored on S3.
  - **SageMaker Pipelines** → replaced with Python automation function.
- Retained services with default quotas: Endpoint (`ml.t2.medium`), CloudWatch, Lambda, API Gateway.
- Re-ran the entire pipeline from Week 1 to Week 8 and verified equivalent results.

#### Results
- ✅ Entire project recreated successfully on new account.
- ✅ Accuracy still reached **84.92%**.
- ✅ Endpoint `titanic-survival-endpoint` is live.
- ✅ API Gateway and Lambda work normally.
- ✅ All artifacts saved on S3.
- ✅ Workflow no longer depends on special quotas, reusable for any student account.

#### Lessons Learned
- Always back up code and documentation to GitHub for quick recovery.
- When quota is limited, be flexible with alternative solutions (local execution, JSON metadata, etc.).
- Rebuilding from scratch deepens understanding of each step and helps optimize the process.
