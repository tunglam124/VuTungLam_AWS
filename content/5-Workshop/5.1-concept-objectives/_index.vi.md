---
title : "Ý tưởng & Mục tiêu"
date : "2025-10-10"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---
# 5.1. Ý Tưởng & Mục Tiêu (1.0 điểm)

---

### Bối Cảnh & Bài Toán

**Cloud Nexus** là nền tảng mô phỏng và phân tích bảo mật mạng (Threat Modeling Platform) dành cho các chuyên gia an ninh mạng và kiến trúc sư hạ tầng. Hệ thống cho phép người dùng vẽ sơ đồ mạng (network topology), sau đó sử dụng AI (Google Gemini) để tự động phát hiện lỗ hổng, mô phỏng đường đi tấn công, và đề xuất biện pháp phòng thủ.

**Khách hàng mục tiêu:**
- Chuyên gia bảo mật (Security Analysts)
- Kiến trúc sư hạ tầng (Cloud Architects)
- Sinh viên học về an ninh mạng (Cybersecurity Students)

**Vấn đề giải quyết:**
| Vấn đề | Giải pháp |
|--------|----------|
| Phát hiện lỗ hổng mạng thủ công tốn thời gian | AI tự động quét topology |
| Khó hình dung đường đi tấn công | Mô phỏng trực quan trên ReactFlow |
| Thiết lập môi trường test phức tạp | Serverless trên AWS, không cần quản lý server |
| Không có công cụ đánh giá phòng thủ | So sánh attack path trước/sau khi thêm defense |

---

### Mục Tiêu Cụ Thể

| Tiêu chí | Mô tả |
|----------|-------|
| **Output** | REST API endpoints + Web Dashboard (React) |
| **AI Integration** | Google Gemini tạo topology, phân tích lỗ hổng, mô phỏng tấn công |
| **Alert** | SNS notification khi phát hiện tấn công nghiêm trọng |
| **Serverless** | Toàn bộ backend trên Lambda + API Gateway |
| **Infra as Code** | AWS CDK — deploy / destroy bằng 1 lệnh |

**Tiêu chí đánh giá thành công:**
1. Web dashboard load được từ S3 static hosting
2. API Gateway trả về `{"status":"ok"}` tại `/api/health`
3. Lambda gọi được Google Gemini và trả về topology JSON hợp lệ
4. Toàn bộ hạ tầng deploy bằng `cdk deploy` và xóa bằng `cdk destroy`

---

### Phù Hợp Chương Trình FCAJ / AWS

- **Serverless-first:** Lambda, API Gateway, DynamoDB, SQS, SNS, Step Functions
- **Infrastructure as Code:** AWS CDK (TypeScript)
- **Bảo mật:** IAM Role, Secrets Manager, Cognito, Principle of Least Privilege
- **Chi phí thấp:** Free tier cho các service cốt lõi
