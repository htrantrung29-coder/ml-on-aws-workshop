---
title: "Self Evaluation"
date: 2026-07-31
weight: 6
chapter: true
pre: "<b>6. </b>"
---

# Self Evaluation

Below is my self-evaluation during the internship and the Machine Learning on AWS project. The criteria are assessed based on task completion, adaptability, and contribution to the overall project.

## Evaluation Table

| Criteria | Rating | Comments |
|----------|--------|----------|
| **Knowledge** | **Good** | Solid understanding of core AWS services like SageMaker, S3, Lambda, and API Gateway. Understands end-to-end ML workflow. Needs to explore advanced MLOps practices and SageMaker Feature Store further. |
| **Learning Ability** | **Excellent** | Self-studied AWS documentation, debugged technical issues (quota, health check, container). Quickly adapted to resource constraints and found appropriate workarounds. |
| **Proactiveness** | **Good** | Proactively researched new services and proposed solutions when encountering problems. Occasionally needed guidance for complex IAM and networking issues. |
| **Discipline** | **Excellent** | Completed the 8-week schedule on time, maintained detailed worklog and reports. Demonstrated a serious work ethic with clear planning. |
| **Communication** | **Good** | Reported progress regularly, asked clear and coherent questions when facing issues. Able to synthesize and present results logically. |
| **Teamwork** | **Average** | Since this was an individual project, teamwork skills weren't fully demonstrated. However, assisted peers facing similar AWS setup challenges. |
| **Problem Solving** | **Excellent** | Encountered various real-world errors (quota, endpoint health check, Model Registry limit) and resolved them with appropriate solutions or workarounds. Skilled at log analysis and root cause identification. |
| **Contribution to Project** | **Good** | Completed all 8 weeks as required. Built an end-to-end ML system with 84.92% accuracy. Produced a detailed report with complete code and instructions for replication. |

## Challenges and Solutions

### 1. SageMaker Quota Limits
**Problem:** The student account had quota limits for Training Jobs, Processing Jobs, Model Registry, and Pipelines.

**Solution:**
- Ran training and processing directly in JupyterLab (local mode).
- Managed model versions manually using JSON files instead of Model Registry.
- Built a Python function as a pipeline replacement instead of SageMaker Pipelines.

**Lesson:** Always check quotas before starting and have a Plan B for limitations.

### 2. Endpoint Health Check Failure
**Problem:** The SKLearn container didn't have the `xgboost` library pre-installed, causing endpoint health check failure.

**Solution:** Switched to the official AWS XGBoost container instead of the SKLearn container.

**Lesson:** Always check CloudWatch logs and choose the correct container for your framework.

### 3. Lost Old AWS Account
**Problem:** Lost access to the previous AWS account, unable to finalize the report and demo.

**Solution:** Created a new account and re-ran all steps from scratch, adjusting code to avoid high-quota services.

**Lesson:** Always back up code and documentation. Use IAM users instead of the root user.

## Future Development Directions

- 🔜 Experiment with larger datasets (> 100K rows) to evaluate scalability.
- 🔜 Integrate CI/CD with GitHub Actions for automated model deployment on changes.
- 🔜 Implement A/B testing with multiple model variants on the same endpoint.
- 🔜 Explore SageMaker Feature Store for centralized feature management.
- 🔜 Deploy multi-region for high availability and lower latency.
