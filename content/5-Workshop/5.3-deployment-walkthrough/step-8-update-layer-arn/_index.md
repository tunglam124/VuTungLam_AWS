---
title : "Update Layer ARN in CDK"
date : "2025-10-10"
weight : 8
chapter : false
pre : " <b> Step 8 </b> "
---
# Step 8: Update Layer ARN in CDK

---

### Commands

Open the CDK stack file:

```powershell
notepad C:\<USER>\<PROJECT_DIR>\cdk\lib\auth-api-stack.ts
```

Find this line:
```typescript
'arn:aws:lambda:ap-southeast-1:<ACCOUNT_ID>:layer:CloudNexus-PythonDeps:1'
```

Update the version number at the end (e.g., `:1`, `:2`, `:3`, `:4`) depending on how many times you published the layer.

📸 *[SCREENSHOT: Editor showing highlighted layer ARN line]*
