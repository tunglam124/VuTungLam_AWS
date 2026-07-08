---
title : "Deploy Simulation Stack"
date : "2025-10-10"
weight : 6
chapter : false
pre : " <b> Step 6 </b> "
---
# Step 6: Deploy Simulation Stack

---

### Mô tả

Tạo các service phụ trợ: SQS, DynamoDB, S3, Step Functions, SNS.

### Thao tác

```powershell
cdk deploy CloudNexusSimulationStack --require-approval never
```

### Expected output

```
✅  CloudNexusSimulationStack
Outputs:
  CloudNexusSimulationStack.ResultBucketName = cloudnexus-results-<ACCOUNT_ID>-ap-southeast-1
  CloudNexusSimulationStack.StateMachineArn = arn:aws:states:ap-southeast-1:<ACCOUNT_ID>:stateMachine:CloudNexus-SimOrchestrator
  CloudNexusSimulationStack.AlertTopicArn = arn:aws:sns:ap-southeast-1:<ACCOUNT_ID>:CloudNexus-Alerts
```

📸 *[CHÈN ẢNH: Kết quả cdk deploy SimulationStack]*

### Tài nguyên tạo ra

| Resource | AWS Service | Mục đích |
|----------|-------------|---------|
| `CloudNexus-ScanQueue` | SQS | Hàng đợi scan job |
| `CloudNexus-ResultsTable` | DynamoDB | Lưu kết quả |
| `CloudNexus-ResultBucket` | S3 | File kết quả lớn |
| `CloudNexus-SimOrchestrator` | Step Functions | Điều phối luồng |
| `CloudNexus-Alerts` | SNS | Thông báo alert |
