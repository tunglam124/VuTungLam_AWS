---
title : "Architecture & Technical Design"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---
# 5.2. Architecture & Technical Design (2.0 pts)

---

### Architecture Diagram

*(Diagram image to be inserted)*

---

### Service Selection

| Service | Rationale | Cost |
|---------|----------|------|
| **S3** | Static web hosting, no server, CDK integration | ~$0.01/month |
| **API Gateway** | Managed REST API, auto-scaling, Lambda integration | $0 (1M req/month free) |
| **Lambda** | Serverless, pay-per-request, ARM64 cheaper than x86 | $0 (1M req + 400K GBs free) |
| **Cognito** | Managed user pool, social login support | $0 (50k MAU free) |
| **DynamoDB** | NoSQL key-value, no management, auto-scale | $0 (25GB free) |
| **SQS** | Queue between API and Step Functions, absorbs spikes | $0 (1M req free) |
| **SNS** | Push notification when severe attack detected | $0 (1M pub free) |
| **Step Functions** | Orchestrate simulation workflow | $0 (4k state transitions free) |
| **Secrets Manager** | Securely store API key, auto-rotate | ~$0.40/month |

---

### Security & IAM

**Principles:**
1. **Principle of Least Privilege:** Each Lambda has minimum permissions (e.g., API handler cannot write SQS)
2. **No hard-coded keys:** Google API key stored in Secrets Manager or Lambda env
3. **S3 private by default:** Bucket only public for static web hosting
4. **IAM Role:** Lambda receives role automatically via CDK, no access keys

**Example IAM Policy (API Handler):**
```json
{
  "Effect": "Allow",
  "Action": [
    "secretsmanager:GetSecretValue",
    "dynamodb:PutItem",
    "dynamodb:GetItem",
    "sqs:SendMessage",
    "sns:Publish"
  ],
  "Resource": "arn:aws:...:CloudNexus-*"
}
```

---

### Scalability & Operations

| Aspect | Implementation |
|--------|---------------|
| **Scale** | Lambda auto-scales per request, SQS buffers spikes |
| **Event-driven** | SQS → Step Functions → DynamoDB stores results |
| **Async processing** | Scan request via SQS, does not block client |
| **Logging** | CloudWatch Logs for Lambda |
| **Monitoring** | CloudWatch Alarm on Lambda error rate, SQS depth |
| **Alert** | SNS → Email when severe attack path detected |
