---
title : "Deploy API Stack"
date : "2025-10-10"
weight : 9
chapter : false
pre : " <b> Step 9 </b> "
---
# Step 9: Deploy API Stack

---

### Mô tả

Tạo API Gateway, Lambda (FastAPI), Cognito User Pool.

### Thao tác

```powershell
cd C:\<USER>\<PROJECT_DIR>\cdk
cdk deploy CloudNexusAuthApiStack --require-approval never
```

### Expected output

```
✅  CloudNexusAuthApiStack
Outputs:
  CloudNexusAuthApiStack.APIEndpoint = https://<API_ID>.execute-api.ap-southeast-1.amazonaws.com/prod/
  CloudNexusAuthApiStack.UserPoolId = ap-southeast-1_XXXXX
  CloudNexusAuthApiStack.ClientId = xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

📸 *[CHÈN ẢNH: cdk deploy AuthApiStack outputs]*

### Tài nguyên tạo ra

| Resource | AWS Service | Mục đích |
|----------|-------------|---------|
| `CloudNexus-APIHandler` | Lambda | FastAPI backend |
| `CloudNexus-PythonDeps` | Layer | Python deps |
| `CloudNexusAPI` | API Gateway | REST endpoint |
| `CloudNexusUserPool` | Cognito | User pool |
| `cloud-nexus/google-api-key` | Secrets Manager | API key |
