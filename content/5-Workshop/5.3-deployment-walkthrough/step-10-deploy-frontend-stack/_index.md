---
title : "Deploy Frontend Stack"
date : "2025-10-10"
weight : 10
chapter : false
pre : " <b> Step 10 </b> "
---
# Step 10: Deploy Frontend Stack

---

### Description

Creates S3 bucket and uploads frontend (React) to static website hosting.

### Commands

```powershell
cdk deploy CloudNexusFrontendStack --require-approval never
```

### Expected Output

```
✅  CloudNexusFrontendStack
Outputs:
  CloudNexusFrontendStack.WebsiteURL = http://cloudnexusfrontendstack-<SUFFIX>.s3-website-ap-southeast-1.amazonaws.com
```

📸 *[SCREENSHOT: cdk deploy FrontendStack]*

### S3 Configuration

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
