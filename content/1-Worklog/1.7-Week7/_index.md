---
title: "Week 7: System Monitoring"
date: 2026-07-31
weight: 7
chapter: false
pre: "<b>1.7 </b>"
---

#### Tasks Done
- Created 2 CloudWatch Alarms:
  - `titanic-endpoint-errors`: alerts on 5XX errors.
  - `titanic-endpoint-latency`: alerts when latency > 1 second.
- Sent 20 requests to Endpoint to generate metrics and data capture.
- Created Model Monitor baseline using `ml.t3.xlarge` from `train.csv` (generated `statistics.json` and `constraints.json`).
- Created Monitoring Schedule (`titanic-monitor-schedule`) running hourly to detect data drift.

#### Results
- ✅ CloudWatch Alarms in `OK` state.
- ✅ Baseline files saved at `monitoring/baseline/`.
- ✅ Data Capture active, storing request/payload at `monitoring/captured-data/`.
- ✅ Monitoring Schedule created successfully.
