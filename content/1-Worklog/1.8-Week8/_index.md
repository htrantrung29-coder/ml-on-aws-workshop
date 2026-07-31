---
title: "Week 8: Pipeline Automation"
date: 2026-07-31
weight: 8
chapter: false
pre: "<b>1.8 </b>"
---

#### Tasks Done
- Built a pipeline as a **Python function** (instead of SageMaker Pipelines due to quota) with 4 steps:
  1. **Data Processing**: Load raw data, process, train/test split.
  2. **Upload processed data**: Save `train.csv` and `test.csv` to S3 (`pipeline/processed/`).
  3. **Training**: Train XGBoost with optimal parameters (`depth=3`, `n=100`, `lr=0.01`).
  4. **Save model**: Package and upload model to S3 (`pipeline/models/`).
- Invoked the pipeline function and verified results.

#### Results
- ✅ Pipeline runs end-to-end automatically.
- ✅ Accuracy achieved **84.92%** (matches HPO best).
- ✅ Model artifact saved at `pipeline/models/model.tar.gz`.
- ✅ Entire workflow from raw data → model → S3 is automated.
