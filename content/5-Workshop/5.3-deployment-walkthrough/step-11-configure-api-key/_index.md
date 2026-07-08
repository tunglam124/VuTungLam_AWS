---
title : "Configure Google API Key"
date : "2025-10-10"
weight : 11
chapter : false
pre : " <b> Step 11 </b> "
---
# Step 11: Configure Google API Key

---

Lambda needs Google API key to call Gemini. Two approaches:

### Method 1: Environment Variable (fast)

```powershell
aws lambda update-function-configuration --function-name CloudNexus-APIHandler `
  --environment "Variables={
    GOOGLE_API_KEY=<YOUR_GOOGLE_API_KEY>,
    SCAN_QUEUE_URL=https://sqs.ap-southeast-1.amazonaws.com/<ACCOUNT_ID>/CloudNexus-ScanQueue,
    GEMINI_MODEL=gemini-2.0-flash
  }"
```

### Method 2: Secrets Manager (more secure)

```powershell
aws secretsmanager put-secret-value `
  --secret-id cloud-nexus/google-api-key `
  --secret-string "<YOUR_GOOGLE_API_KEY>"
```

### Code to Read Key

```python
# ai_service.py
_api_key = os.environ.get('GOOGLE_API_KEY')
if not _api_key:
    secrets_client = boto3.client('secretsmanager')
    resp = secrets_client.get_secret_value(SecretId='cloud-nexus/google-api-key')
    _api_key = resp['SecretString']
```
