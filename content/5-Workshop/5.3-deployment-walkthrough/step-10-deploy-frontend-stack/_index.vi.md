---
title : "Deploy Frontend Stack"
date : "2025-10-10"
weight : 10
chapter : false
pre : " <b> Step 10 </b> "
---
# Step 10: Deploy Frontend Stack

---

### Mô tả

Tạo S3 bucket và upload frontend (React) lên static website hosting.

### Thao tác

```powershell
cdk deploy CloudNexusFrontendStack --require-approval never
```

### Expected output

```
✅  CloudNexusFrontendStack
Outputs:
  CloudNexusFrontendStack.WebsiteURL = http://cloudnexusfrontendstack-<SUFFIX>.s3-website-ap-southeast-1.amazonaws.com
```

📸 *[CHÈN ẢNH: cdk deploy FrontendStack]*

### Cấu hình S3

```typescript
// frontend-stack.ts
this.frontendBucket = new Bucket(this, 'FrontendBucket', {
  publicReadAccess: true,
  blockPublicAccess: BlockPublicAccess.BLOCK_ACLS,
  websiteIndexDocument: 'index.html',
  websiteErrorDocument: 'index.html',
  removalPolicy: RemovalPolicy.RETAIN,
  versioned: true,
})
```
