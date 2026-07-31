---
title: "5.4 Xử lý dữ liệu"
date: 2026-07-31
weight: 4
chapter: false
pre: "<b>5.4 </b>"
---

## Dataset

Sử dụng dataset Titanic từ Kaggle:
- 891 hành khách
- 12 features
- Target: `Survived` (0/1)

## Bước 1: Tải và khám phá dữ liệu

```python
import pandas as pd
import boto3
from config import bucket

url = "https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv"
df = pd.read_csv(url)

print(f"Shape: {df.shape}")
print(f"Missing values:\n{df.isnull().sum()}")
print(f"5 dòng đầu:\n{df.head()}")
```
Bước 2: Upload dữ liệu thô lên S3
```python
df.to_csv("titanic_raw.csv", index=False)
s3 = boto3.client("s3")
s3.upload_file("titanic_raw.csv", bucket, "data/raw/titanic_raw.csv")
print(f"Uploaded: s3://sagemaker-ap-southeast-2-921736623375/data/raw/titanic_raw.csv")
```
Bước 3: Xử lý dữ liệu
```python
# 1. Xử lý missing values
df["Age"].fillna(df["Age"].median(), inplace=True)
df["Embarked"].fillna(df["Embarked"].mode()[0], inplace=True)
df.drop(columns=["Cabin"], inplace=True)

# 2. Feature Engineering
df["FamilySize"] = df["SibSp"] + df["Parch"] + 1
df["IsAlone"] = (df["FamilySize"] == 1).astype(int)
df["Title"] = df["Name"].str.extract(r" ([A-Za-z]+)\.", expand=False)
df["Title"] = df["Title"].replace(
    ["Lady","Countess","Capt","Col","Don","Dr","Major","Rev","Sir","Jonkheer","Dona"],
    "Rare"
)
df["Title"] = df["Title"].replace({"Mlle":"Miss","Ms":"Miss","Mme":"Mrs"})

# 3. Encoding
df["Sex"] = df["Sex"].map({"male": 0, "female": 1})
df["Embarked"] = df["Embarked"].map({"S": 0, "C": 1, "Q": 2})
df["Title"] = df["Title"].map({"Mr":0,"Miss":1,"Mrs":2,"Master":3,"Rare":4})

# 4. Chọn features và split
FEATURES = ["Pclass","Sex","Age","SibSp","Parch","Fare","Embarked","FamilySize","IsAlone","Title"]
TARGET = "Survived"
df_final = df[FEATURES + [TARGET]].dropna()

from sklearn.model_selection import train_test_split
train_df, test_df = train_test_split(
    df_final, test_size=0.2, random_state=42, stratify=df_final[TARGET]
)

print(f"Train: {train_df.shape} | Test: {test_df.shape}")
```
Bước 4: Lưu và upload lên S3
```python
import os
os.makedirs("data/processed", exist_ok=True)
train_df.to_csv("data/processed/train.csv", index=False)
test_df.to_csv("data/processed/test.csv", index=False)

s3.upload_file("data/processed/train.csv", bucket, "data/processed/train.csv")
s3.upload_file("data/processed/test.csv", bucket, "data/processed/test.csv")
print(f"Uploaded: s3://sagemaker-ap-southeast-2-921736623375/data/processed/")
```
Kết quả
Train: 712 rows, 11 columns

Test: 179 rows, 11 columns

0 missing values
