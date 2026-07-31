---
title: "Proposal"
date: 2026-07-31
weight: 2
chapter: false
pre: "<b>2. </b>"
---

# Project Proposal: Machine Learning on AWS

## 1. Overview

Building an end-to-end Machine Learning system on AWS using Amazon SageMaker as the main platform, with the Titanic survival prediction problem as the experimental use case.

## 2. Objectives

### Technical Objectives
- Build an automated data pipeline with SageMaker Processing Jobs.
- Train and optimize an XGBoost model to achieve Accuracy ≥ 83%.
- Deploy a production-ready REST API with latency < 1 second.
- Set up automated monitoring to detect data drift.

### Learning Objectives
- Master the AWS ML ecosystem.
- Understand end-to-end ML workflow on the cloud.
- Practice MLOps best practices.

## 3. Problem Statement

| Problem | Solution |
|---------|----------|
| Complex ML model deployment | SageMaker Endpoint |
| No model version control | SageMaker Model Registry |
| Hard to reproduce results | SageMaker Experiments |
| No monitoring after deployment | CloudWatch + Model Monitor |
| Manual pipeline | SageMaker Pipelines |

## 4. Solution Architecture

```text
┌─────────────────────────────────────────────┐
│ DATA LAYER                                  │
│ S3 (raw) → Processing → S3 (processed)      │
└─────────────────┬───────────────────────────┘
                  ↓
┌─────────────────────────────────────────────┐
│ TRAINING LAYER                              │
│ Training → Experiments → HPO → Registry     │
└─────────────────┬───────────────────────────┘
                  ↓
┌─────────────────────────────────────────────┐
│ INFERENCE LAYER                             │
│ Endpoint → Lambda → API Gateway → Client    │
└─────────────────┬───────────────────────────┘
                  ↓
┌─────────────────────────────────────────────┐
│ MONITORING LAYER                            │
│ CloudWatch Alarms + SageMaker Model Monitor │
└─────────────────────────────────────────────┘
```

## 5. Timeline

| Week | Content | Deliverable |
|------|---------|-------------|
| 1 | Environment Setup | IAM, S3, Studio |
| 2 | Data Processing | train.csv, test.csv |
| 3 | Model Training | model.joblib |
| 4 | HPO | best_model.joblib |
| 5 | Model Registry | 2 versions |
| 6 | Deploy + API | REST endpoint |
| 7 | Monitoring | Alarms + Schedule |
| 8 | Pipelines | TitanicMLPipeline |

## 6. Estimated Budget

| Service | Unit Price | Duration | Cost |
|---------|------------|----------|------|
| SageMaker Studio | $0.044/hour | 8 weeks × 4h/week | ~$14 |
| SageMaker Endpoint | $0.065/hour | 2 weeks × 8h | ~$10 |
| S3 Storage | $0.023/GB | 1 GB | ~$0.02 |
| Lambda + API GW | Free tier | — | $0 |
| **Total** | | | **~$24** |

## 7. Risks & Mitigation

| Risk | Level | Mitigation |
|------|-------|------------|
| Quota limits | High | Train locally + document workaround |
| Cost overrun | Low | Delete endpoint after demo |
| Low model accuracy | Low | HPO for optimization |
| Endpoint failure | Medium | CloudWatch alarm + retry |
| Data drift | Medium | Model Monitor schedule |
