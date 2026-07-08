---
title : "Deploy Simulation Stack"
date : "2025-10-10"
weight : 6
chapter : false
pre : " <b> Step 6 </b> "
---
# Step 6: Deploy Simulation Stack

---

### Description

Creates supporting services: SQS, DynamoDB, S3, Step Functions, SNS.

### Commands

```powershell
cdk deploy CloudNexusSimulationStack --require-approval never
```

### Expected Output

```
✅  CloudNexusSimulationStack
Outputs:
  CloudNexusSimulationStack.ResultBucketName = cloudnexus-results-<ACCOUNT_ID>-ap-southeast-1
  CloudNexusSimulationStack.StateMachineArn = arn:aws:states:ap-southeast-1:<ACCOUNT_ID>:stateMachine:CloudNexus-SimOrchestrator
  CloudNexusSimulationStack.AlertTopicArn = arn:aws:sns:ap-southeast-1:<ACCOUNT_ID>:CloudNexus-Alerts
```

📸 *[SCREENSHOT: cdk deploy SimulationStack output]*

### Resources Created

| Resource | AWS Service | Purpose |
|----------|-------------|---------|
| `CloudNexus-ScanQueue` | SQS | Scan job queue |
| `CloudNexus-ResultsTable` | DynamoDB | Store results |
| `CloudNexus-ResultBucket` | S3 | Large result files |
| `CloudNexus-SimOrchestrator` | Step Functions | Workflow orchestration |
| `CloudNexus-Alerts` | SNS | Alert notifications |
