---
title: "Week 9: Rebuild from Scratch with New Account"
date: 2026-07-31
weight: 9
chapter: false
pre: "<b>1.9 </b>"
---

#### Reason
- The old AWS account was lost (forgotten password / locked), unable to access for finalizing the report and demo.
- Decided to create a new account and redo all steps from scratch, focusing on **not using high-quota services** (Processing Job, Training Job, Pipelines) to ensure successful execution.

#### Tasks Done
- Registered a new AWS account (free tier).
- Repeated setup steps from Week 1:
  - Created IAM Role with necessary policies.
  - Created a new S3 Bucket with folders data/, models/, outputs/.
  - Launched SageMaker Studio and JupyterLab.
  - Recreated config.py with the new bucket info.
- Re-ran all notebooks from Week 2 → 8, adjusted code to work entirely in **local mode** (no SageMaker Processing, Training, or Pipelines).
- Verified results and ensured metrics matched the previous run:
  - Baseline accuracy: 83.80%
  - Best accuracy: 84.92%
  - Endpoint working, API returns correct predictions.
- Updated report files on GitHub with new account info (bucket name, region, endpoint URL).

#### Results
- ✅ New account works stably.
- ✅ All steps completed successfully without quota errors.
- ✅ Accuracy and API test results perfectly match the first run.
- ✅ Report updated and ready for demo.
