---
title : "Điều kiện tiên quyết"
date : "2025-10-10"
weight : 0
chapter : false
pre : " <b> Step 0 </b> "
---
# Step 0: Điều Kiện Tiên Quyết

---

### Công cụ cần cài đặt

| Công cụ | Yêu cầu | Cài đặt |
|---------|---------|---------|
| AWS Account | Active | [Đăng ký AWS](https://aws.amazon.com) |
| Region | `ap-southeast-1` | Chọn trong AWS Console |
| AWS CLI | v2.x | `winget install Amazon.AWSCLI` |
| Node.js | v18+ | `winget install OpenJS.NodeJS.LTS` |
| Python | 3.12 | `winget install Python.Python.3.12` |
| npm | v9+ | (kèm Node.js) |
| AWS CDK | v2.170+ | `npm install -g aws-cdk` |
| Git | Latest | `winget install Git.Git` |
| Google API Key | Gemini free | [Lấy tại đây](https://aistudio.google.com/app/apikey) |

### Kiểm tra cài đặt

```powershell
aws --version
node --version
npm --version
cdk --version
python --version
```

📸 *[CHÈN ẢNH: Terminal hiển thị version các công cụ]*

### Quyền IAM cần thiết

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": [
      "cloudformation:*", "s3:*", "iam:*", "lambda:*",
      "apigateway:*", "cognito-idp:*", "dynamodb:*",
      "sqs:*", "sns:*", "states:*", "secretsmanager:*",
      "logs:*", "ssm:GetParameter", "ecr:*"
    ],
    "Resource": "*"
  }]
}
```

### Chi phí dự kiến

> Tất cả service trong bài đều nằm trong AWS Free Tier hoặc chi phí rất thấp (< $1/tháng nếu không sử dụng nhiều).
