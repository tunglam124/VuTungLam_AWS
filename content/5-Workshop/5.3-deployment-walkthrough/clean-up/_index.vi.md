---
title : "Dọn dẹp tài nguyên"
date : "2025-10-10"
weight : 13
chapter : false
pre : " <b> Clean Up </b> "
---
# Dọn Dẹp Tài Nguyên

---

### Bước 1: Xóa CDK stacks

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

📸 *[CHÈN ẢNH: cdk destroy thành công]*

---

### Bước 2: Xóa S3 buckets (CDK giữ lại do RemovalPolicy.RETAIN)

```powershell
aws s3 rb s3://cloudnexusfrontendstack-frontendbucket-<SUFFIX> --force
aws s3 rb s3://cloudnexus-results-<ACCOUNT_ID>-ap-southeast-1 --force
```

---

### Bước 3: Xóa Lambda Layer versions

```powershell
aws lambda list-layer-versions --layer-name CloudNexus-PythonDeps
aws lambda delete-layer-version --layer-name CloudNexus-PythonDeps --version-number 1
aws lambda delete-layer-version --layer-name CloudNexus-PythonDeps --version-number 2
# ... xóa tất cả versions
```

---

### Bước 4: Xóa Secrets Manager

```powershell
aws secretsmanager delete-secret --secret-id cloud-nexus/google-api-key --force-delete-without-recovery
```

---

### Bước 5: Xóa CloudWatch Log Groups

```powershell
aws logs delete-log-group --log-group-name /aws/lambda/CloudNexus-APIHandler
aws logs delete-log-group --log-group-name /aws/lambda/CloudNexus-ScanWorker
aws logs delete-log-group --log-group-name /aws/lambda/CloudNexus-Notifier
```

---

### Bước 6 (tùy chọn): Xóa CDK Bootstrap

```powershell
aws s3 rb s3://cdk-hnb659fds-assets-<ACCOUNT_ID>-ap-southeast-1 --force
aws cloudformation delete-stack --stack-name CDKToolkit
```

---

### Bước 7: Xác nhận

```powershell
aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE UPDATE_COMPLETE
aws lambda list-functions --query "Functions[?starts_with(FunctionName,'CloudNexus')].FunctionName"
aws s3 ls | Select-String "cloudnexus"
aws logs describe-log-groups --log-group-name-prefix "/aws/lambda/CloudNexus"
```

**Kết quả mong đợi:** Không còn tài nguyên CloudNexus nào.
