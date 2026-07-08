---
title : "Kiến trúc & Thiết kế Kỹ thuật"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---
# 5.2. Kiến Trúc & Thiết Kế Kỹ Thuật (2.0 điểm)

---

### Sơ Đồ Kiến Trúc

*(Hình diagram sẽ được chèn sau)*

---

### Lựa Chọn Dịch Vụ

| Service | Lý do chọn | Chi phí |
|---------|-----------|---------|
| **S3** | Host static web, không cần server, tích hợp sẵn CDK | ~$0.01/tháng |
| **API Gateway** | REST API managed, tự động scale, tích hợp Lambda | $0 (1tr req/tháng free) |
| **Lambda** | Serverless, trả tiền theo request, ARM64 rẻ hơn x86 | $0 (1tr req + 400K GBs free) |
| **Cognito** | User pool managed, social login support | $0 (50k MAU free) |
| **DynamoDB** | NoSQL key-value, không cần quản lý, auto-scale | $0 (25GB free) |
| **SQS** | Queue giữa API và Step Functions, giảm tải đột biến | $0 (1tr req free) |
| **SNS** | Push notification khi phát hiện attack nghiêm trọng | $0 (1tr pub free) |
| **Step Functions** | Orchestrate simulation workflow | $0 (4k state transitions free) |
| **Secrets Manager** | Lưu API key an toàn, tự động rotate | ~$0.40/tháng |

---

### Bảo Mật & IAM

**Nguyên tắc:**
1. **Principle of Least Privilege:** Mỗi Lambda chỉ có quyền tối thiểu (VD: API handler không được write SQS)
2. **Không hard-code key:** Google API key lưu trong Secrets Manager hoặc Lambda env
3. **S3 private (mặc định):** Bucket chỉ public cho static web hosting
4. **IAM Role:** Lambda nhận role tự động qua CDK, không dùng access key

**Ví dụ IAM Policy (API Handler):**
```json
{
  "Effect": "Allow",
  "Action": [
    "secretsmanager:GetSecretValue",
    "dynamodb:PutItem",
    "dynamodb:GetItem",
    "sqs:SendMessage",
    "sns:Publish"
  ],
  "Resource": "arn:aws:...:CloudNexus-*"
}
```

---

### Khả Năng Mở Rộng & Vận Hành

| Khía cạnh | Cách triển khai |
|-----------|----------------|
| **Scale** | Lambda auto-scale theo request, SQS buffer khi đột biến |
| **Event-driven** | SQS → Step Functions → DynamoDB lưu kết quả |
| **Async processing** | Request scan qua SQS, không block client |
| **Logging** | CloudWatch Logs cho Lambda |
| **Monitoring** | CloudWatch Alarm trên Lambda error rate, SQS depth |
| **Alert** | SNS → Email khi phát hiện attack path nghiêm trọng |
