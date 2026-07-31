---
title: "Week 3: Model Training – Local mode"
date: 2026-07-31
weight: 3
chapter: false
pre: "<b>1.3 </b>"
---

#### Tasks Done
- Wrote train.py for XGBoost with argparse for hyperparameters.
- Due to SageMaker Training Job quota (ml.m5.large = 0), trained directly in the notebook.
- Baseline training with:
  - max_depth = 5
  - n_estimators = 100
  - learning_rate = 0.1
- Evaluated model on test set.
- Logged experiment to SageMaker Experiments (titanic-training).
- Saved model.joblib to S3 (models/).

#### Results
- ✅ Baseline Accuracy: 83.80%.
- ✅ Precision (Not survived/Survived): 0.85 / 0.82.
- ✅ Recall: 0.90 / 0.74.
- ✅ Model artifact on S3.
