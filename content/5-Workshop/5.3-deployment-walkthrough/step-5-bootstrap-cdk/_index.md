---
title : "Bootstrap CDK"
date : "2025-10-10"
weight : 5
chapter : false
pre : " <b> Step 5 </b> "
---
# Step 5: Bootstrap CDK

---

### Purpose

Creates S3 bucket `cdk-hnb659fds-assets-<ACCOUNT>-<REGION>` to store templates and assets during deployment.

### Commands

```powershell
cd cdk
cdk bootstrap aws://<ACCOUNT_ID>/ap-southeast-1
```

### Expected Output

```
 ✅  Environment aws://<ACCOUNT_ID>/ap-southeast-1 bootstrapped.
```

📸 *[SCREENSHOT: cdk bootstrap success]*
