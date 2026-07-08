---
title : "Clean Up Resources"
date : "2025-10-10"
weight : 13
chapter : false
pre : " <b> Clean Up </b> "
---
# Clean Up Resources

---

### Step 1: Delete CDK stacks

```powershell
cd C:\<USER>\<PROJECT_DIR>\cdk
cdk destroy --all --force
```

**Expected:**
```
 ✅  CloudNexusFrontendStack: destroyed
 ✅  CloudNexusAuthApiStack: destroyed
 ✅  CloudNexusSimulationStack: destroyed
```

📸 *[SCREENSHOT: cdk destroy success]*

---

### Step 2: Delete S3 buckets (retained by CDK due to RemovalPolicy.RETAIN)

```powershell
aws s3 rb s3://cloudnexusfrontendstack-frontendbucket-<SUFFIX> --force
aws s3 rb s3://cloudnexus-results-<ACCOUNT_ID>-ap-southeast-1 --force
```

---

### Step 3: Delete Lambda Layer versions

```powershell
aws lambda list-layer-versions --layer-name CloudNexus-PythonDeps
aws lambda delete-layer-version --layer-name CloudNexus-PythonDeps --version-number 1
aws lambda delete-layer-version --layer-name CloudNexus-PythonDeps --version-number 2
```

---

### Step 4: Delete Secrets Manager

```powershell
aws secretsmanager delete-secret --secret-id cloud-nexus/google-api-key --force-delete-without-recovery
```

---

### Step 5: Delete CloudWatch Log Groups

```powershell
aws logs delete-log-group --log-group-name /aws/lambda/CloudNexus-APIHandler
aws logs delete-log-group --log-group-name /aws/lambda/CloudNexus-ScanWorker
aws logs delete-log-group --log-group-name /aws/lambda/CloudNexus-Notifier
```

---

### Step 6 (optional): Delete CDK Bootstrap

```powershell
aws s3 rb s3://cdk-hnb659fds-assets-<ACCOUNT_ID>-ap-southeast-1 --force
aws cloudformation delete-stack --stack-name CDKToolkit
```

---

### Step 7: Verify

```powershell
aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE UPDATE_COMPLETE
aws lambda list-functions --query "Functions[?starts_with(FunctionName,'CloudNexus')].FunctionName"
aws s3 ls | Select-String "cloudnexus"
aws logs describe-log-groups --log-group-name-prefix "/aws/lambda/CloudNexus"
```

**Expected result:** No CloudNexus resources remain.
