---
title : "Deploy API Stack"
date : "2025-10-10"
weight : 9
chapter : false
pre : " <b> Step 9 </b> "
---
# Step 9: Deploy API Stack

---

### Description

Creates API Gateway, Lambda (FastAPI), Cognito User Pool.

### Commands

```powershell
cd C:\<USER>\<PROJECT_DIR>\cdk
cdk deploy CloudNexusAuthApiStack --require-approval never
```

### Expected Output

```
✅  CloudNexusAuthApiStack
Outputs:
  CloudNexusAuthApiStack.APIEndpoint = https://<API_ID>.execute-api.ap-southeast-1.amazonaws.com/prod/
  CloudNexusAuthApiStack.UserPoolId = ap-southeast-1_XXXXX
  CloudNexusAuthApiStack.ClientId = xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

📸 *[SCREENSHOT: cdk deploy AuthApiStack outputs]*

### Resources Created

| Resource | AWS Service | Purpose |
|----------|-------------|---------|
| `CloudNexus-APIHandler` | Lambda | FastAPI backend |
| `CloudNexus-PythonDeps` | Layer | Python dependencies |
| `CloudNexusAPI` | API Gateway | REST endpoint |
| `CloudNexusUserPool` | Cognito | User pool |
| `cloud-nexus/google-api-key` | Secrets Manager | API key storage |
