---
title: "Week 2: Data Processing – Local mode"
date: 2026-07-31
weight: 2
chapter: false
pre: "<b>1.2 </b>"
---

#### Tasks Done
- Loaded Titanic dataset (891 passengers, 12 features) from GitHub.
- Analyzed missing values: Age (177), Cabin (687), Embarked (2).
- Due to SageMaker Processing Job quota limits, performed data processing **directly in the notebook**.
- Processing steps:
  - Filled missing values: Age (median), Embarked (mode).
  - Dropped Cabin column.
  - Feature Engineering: created FamilySize, IsAlone, extracted Title from name.
  - Encoding: Sex (0/1), Embarked (S/C/Q → 0/1/2), Title (Mr/Miss/Mrs/Master/Rare → 0-4).
  - Selected 10 features and target Survived.
  - Train/Test split 80/20 (stratified).
- Saved train.csv and test.csv, uploaded to S3 (data/processed/).

#### Results
- ✅ Train: 712 rows, 11 columns; Test: 179 rows, 11 columns.
- ✅ 0 missing values.
- ✅ Uploaded to S3 successfully.
