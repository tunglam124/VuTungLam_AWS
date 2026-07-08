---
title : "Cập nhật Layer ARN trong CDK"
date : "2025-10-10"
weight : 8
chapter : false
pre : " <b> Step 8 </b> "
---
# Step 8: Cập Nhật Layer ARN trong CDK

---

### Thao tác

Mở file CDK stack:

```powershell
notepad C:\<USER>\<PROJECT_DIR>\cdk\lib\auth-api-stack.ts
```

Tìm dòng:
```typescript
'arn:aws:lambda:ap-southeast-1:<ACCOUNT_ID>:layer:CloudNexus-PythonDeps:1'
```

Cập nhật số version cuối cùng (VD: `:1`, `:2`, `:3`, `:4`) tùy vào lần publish layer.

📸 *[CHÈN ẢNH: Editor hiển thị dòng layer ARN được highlight]*
