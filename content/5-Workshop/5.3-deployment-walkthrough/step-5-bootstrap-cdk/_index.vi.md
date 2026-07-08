---
title : "Bootstrap CDK"
date : "2025-10-10"
weight : 5
chapter : false
pre : " <b> Step 5 </b> "
---
# Step 5: Bootstrap CDK

---

### Mục đích

Tạo S3 bucket `cdk-hnb659fds-assets-<ACCOUNT>-<REGION>` để lưu template và assets khi deploy.

### Thao tác

```powershell
cd cdk
cdk bootstrap aws://<ACCOUNT_ID>/ap-southeast-1
```

### Expected output

```
 ✅  Environment aws://<ACCOUNT_ID>/ap-southeast-1 bootstrapped.
```

📸 *[CHÈN ẢNH: cdk bootstrap thành công]*
