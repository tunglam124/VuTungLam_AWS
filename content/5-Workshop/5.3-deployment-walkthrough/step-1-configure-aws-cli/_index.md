---
title : "Configure AWS CLI"
date : "2025-10-10"
weight : 1
chapter : false
pre : " <b> Step 1 </b> "
---
# Step 1: Configure AWS CLI

---

### Commands

```powershell
aws configure
# AWS Access Key ID: ********
# AWS Secret Access Key: ********
# Default region name: ap-southeast-1
# Default output format: json

aws sts get-caller-identity
```

### Expected Output

```json
{
  "UserId": "AIDA...",
  "Account": "<ACCOUNT_ID>",
  "Arn": "arn:aws:iam::<ACCOUNT_ID>:user/..."
}
```

📸 *[SCREENSHOT: aws sts get-caller-identity output showing Account ID]*
