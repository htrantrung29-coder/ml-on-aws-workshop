---
title: "5.9 Pipeline Automation"
date: 2026-07-31
weight: 9
chapter: false
pre: "<b>5.9 </b>"
---

## Introduction

Due to SageMaker Pipelines quota limits, we build a pipeline using a Python function as a replacement. This pipeline automates the entire workflow from data processing, training to model saving.

## Pipeline Function

```python
import pandas as pd
import xgboost as xgb
from sklearn.metrics import accuracy_score
from sklearn.model_selection import train_test_split
import joblib
import tarfile
import os
import boto3
from config import bucket

def run_pipeline(input_s3_uri, learning_rate=0.01, max_depth=3, n_estimators=100):
    print("=" * 50)
    print("TITANIC ML PIPELINE STARTED")
    print("=" * 50)

    # Step 1: Data Processing
    print("\n[Step 1/4] Data Processing...")
    df = pd.read_csv(input_s3_uri)

    df["Age"].fillna(df["Age"].median(), inplace=True)
    df["Embarked"].fillna(df["Embarked"].mode()[0], inplace=True)
    df.drop(columns=["Cabin"], inplace=True)
    df["FamilySize"] = df["SibSp"] + df["Parch"] + 1
    df["IsAlone"] = (df["FamilySize"] == 1).astype(int)
    df["Title"] = df["Name"].str.extract(r" ([A-Za-z]+)\.", expand=False)
    df["Title"] = df["Title"].replace(
        ["Lady","Countess","Capt","Col","Don","Dr","Major","Rev","Sir","Jonkheer","Dona"],
        "Rare"
    )
    df["Title"] = df["Title"].replace({"Mlle":"Miss","Ms":"Miss","Mme":"Mrs"})
    df["Sex"] = df["Sex"].map({"male": 0, "female": 1})
    df["Embarked"] = df["Embarked"].map({"S": 0, "C": 1, "Q": 2})
    df["Title"] = df["Title"].map({"Mr":0,"Miss":1,"Mrs":2,"Master":3,"Rare":4})

    FEATURES = ["Pclass","Sex","Age","SibSp","Parch","Fare","Embarked","FamilySize","IsAlone","Title"]
    TARGET = "Survived"
    df_final = df[FEATURES + [TARGET]].dropna()

    train_df, test_df = train_test_split(
        df_final, test_size=0.2, random_state=42, stratify=df_final[TARGET]
    )
    print(f"   Train: {train_df.shape} | Test: {test_df.shape}")

    # Step 2: Upload processed data
    print("\n[Step 2/4] Upload processed data...")
    os.makedirs("pipeline/processed", exist_ok=True)
    train_df.to_csv("pipeline/processed/train.csv", index=False)
    test_df.to_csv("pipeline/processed/test.csv", index=False)

    s3 = boto3.client("s3")
    s3.upload_file("pipeline/processed/train.csv", bucket, "pipeline/processed/train.csv")
    s3.upload_file("pipeline/processed/test.csv", bucket, "pipeline/processed/test.csv")
    print(f"   Uploaded to s3://{bucket}/pipeline/processed/")

    # Step 3: Training
    print("\n[Step 3/4] Training XGBoost...")
    X_train = train_df[FEATURES]
    y_train = train_df[TARGET]
    X_test = test_df[FEATURES]
    y_test = test_df[TARGET]

    model = xgb.XGBClassifier(
        max_depth=max_depth,
        n_estimators=n_estimators,
        learning_rate=learning_rate,
        eval_metric="logloss",
        random_state=42,
        verbosity=0,
    )
    model.fit(X_train, y_train)

    acc = accuracy_score(y_test, model.predict(X_test))
    print(f"   Accuracy: {acc:.4f}")

    # Step 4: Save model
    print("\n[Step 4/4] Save model...")
    os.makedirs("pipeline/models", exist_ok=True)
    model.save_model("pipeline/models/xgboost-model")
    with tarfile.open("pipeline/models/model.tar.gz", "w:gz") as tar:
        tar.add("pipeline/models/xgboost-model", arcname="xgboost-model")

    s3.upload_file("pipeline/models/model.tar.gz", bucket, "pipeline/models/model.tar.gz")
    print(f"   Model saved: s3://{bucket}/pipeline/models/model.tar.gz")

    print("\n" + "=" * 50)
    print("PIPELINE COMPLETED!")
    print(f"   Accuracy: {acc:.4f}")
    print("=" * 50)

    return {
        "accuracy": acc,
        "learning_rate": learning_rate,
        "max_depth": max_depth,
        "n_estimators": n_estimators,
        "model_s3": f"s3://{bucket}/pipeline/models/model.tar.gz"
    }
```

## Run Pipeline

```python
result = run_pipeline(
    input_s3_uri=f"s3://sagemaker-ap-southeast-2-921736623375/data/raw/titanic_raw.csv",
    learning_rate=0.01,
    max_depth=3,
    n_estimators=100,
)

print(f"Accuracy: {result['accuracy']:.4f}")
```

## Results

- Pipeline runs end-to-end automatically
- Accuracy: 84.92%
- Model artifact: s3://sagemaker-ap-southeast-2-921736623375/pipeline/models/model.tar.gz
