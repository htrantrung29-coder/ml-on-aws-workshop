---
title: "Week 4: Hyperparameter Optimization (HPO)"
date: 2026-07-31
weight: 4
chapter: false
pre: "<b>1.4 </b>"
---

#### Tasks Done
- Designed Grid Search with 27 combinations (3×3×3) for:
  - max_depth: [3, 5, 7]
  - n_estimators: [50, 100, 200]
  - learning_rate: [0.01, 0.1, 0.2]
- Ran 27 training iterations in the notebook, compared accuracy.
- Identified best parameters:
  - max_depth = 3
  - n_estimators = 100
  - learning_rate = 0.01
- Retrained with best params, achieved **84.92%** accuracy.
- Saved best_model.joblib to S3 (models/).
- Logged HPO results to SageMaker Experiments (titanic-hpo).

#### Results
- ✅ Best Accuracy: **84.92%** (+1.12% improvement over baseline).
- ✅ Optimal hyperparameters selected.
