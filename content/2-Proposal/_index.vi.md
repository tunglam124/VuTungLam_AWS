---
title: "Bản Đề Xuất"
date: "2026-07-04
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# Cloud Nexus — Đề xuất dự án (Proposal)

---

## 1. Tổng quan dự án

**Cloud Nexus** là nền tảng mô phỏng và phân tích bảo mật mạng (Threat Modeling Platform) dành cho chuyên gia an ninh mạng và kiến trúc sư hạ tầng. Hệ thống cho phép người dùng thiết kế sơ đồ mạng trực quan, sau đó sử dụng AI (Google Gemini) để tự động phát hiện lỗ hổng, mô phỏng đường đi tấn công, và đề xuất biện pháp phòng thủ.

| Thành phần | Công nghệ |
|-----------|-----------|
| Frontend | React + Vite + ReactFlow + Tailwind CSS |
| Backend | FastAPI trên AWS Lambda + API Gateway |
| AI | Google Gemini API (Gemini 2.0 Flash) |
| Hạ tầng | AWS CDK (TypeScript), Python 3.12 ARM64 |
| AWS Services | S3, API Gateway, Lambda, Cognito, DynamoDB, SQS, SNS, Step Functions, Secrets Manager |

---

## 2. Mục tiêu

### Mục tiêu tổng quát
Xây dựng một nền tảng serverless trên AWS giúp tự động hóa quy trình đánh giá bảo mật mạng, từ vẽ topology đến phát hiện lỗ hổng và mô phỏng tấn công.

### Mục tiêu cụ thể
- **Output:** REST API endpoints + Web Dashboard (React)
- **AI Integration:** Google Gemini tạo topology, phân tích lỗ hổng, mô phỏng tấn công
- **Alert:** SNS notification khi phát hiện tấn công nghiêm trọng
- **Serverless:** Toàn bộ backend trên Lambda + API Gateway
- **Infra as Code:** AWS CDK — deploy / destroy bằng 1 lệnh

### Tiêu chí thành công
1. Web dashboard load được từ S3 static hosting
2. API Gateway trả về `{"status":"ok"}` tại `/api/health`
3. Lambda gọi được Google Gemini và trả về topology JSON hợp lệ
4. Toàn bộ hạ tầng deploy bằng `cdk deploy` và xóa bằng `cdk destroy`

---

## 3. Vấn đề cần giải quyết

| Vấn đề | Giải pháp |
|--------|----------|
| Phát hiện lỗ hổng mạng thủ công tốn thời gian | AI tự động quét topology |
| Khó hình dung đường đi tấn công | Mô phỏng trực quan trên ReactFlow |
| Thiết lập môi trường test phức tạp | Serverless trên AWS, không cần quản lý server |
| Không có công cụ đánh giá phòng thủ | So sánh attack path trước/sau khi thêm defense |

### Khách hàng mục tiêu
- Chuyên gia bảo mật (Security Analysts)
- Kiến trúc sư hạ tầng (Cloud Architects)
- Sinh viên học về an ninh mạng (Cybersecurity Students)

---

![Architecture Diagram](/images/1783482999271_7294040460361473390_g172388743919642419_7e7bc145b9dbf0b86747b4370039c64b.jpg)

---

## 4. Timeline (01/06 → 04/07)

| Giai đoạn | Nội dung | Thời gian |
|-----------|----------|-----------|
| **Khởi động** | Thiết lập môi trường, IAM policy, AWS CLI | 01/06 → 04/06 |
| **Frontend** | Xây dựng UI với React + ReactFlow | 05/06 → 09/06 |
| **Backend** | FastAPI + AI service + Gemini integration | 10/06 → 14/06 |
| **Infrastructure** | AWS CDK stacks (Simulation, API, Frontend, Auth) | 15/06 → 19/06 |
| **Triển khai** | Build Lambda Layer, deploy stacks | 20/06 → 23/06 |
| **Tích hợp** | Kết nối frontend-backend, cấu hình API key | 24/06 → 27/06 |
| **Kiểm thử** | Kiểm tra toàn bộ hệ thống, fix bug | 28/06 → 30/06 |
| **Hoàn thiện** | Báo cáo, tài liệu, dọn dẹp tài nguyên | 01/07 → 04/07 |

---

## 5. Ngân sách

### Chi phí AWS (ước tính hàng tháng)

| Service | Chi phí |
|---------|---------|
| S3 Static Hosting | ~$0.01 |
| API Gateway | $0 (free tier) |
| Lambda | $0 (free tier) |
| Cognito | $0 (free tier) |
| DynamoDB | $0 (free tier) |
| SQS | $0 (free tier) |
| SNS | $0 (free tier) |
| Step Functions | $0 (free tier) |
| Secrets Manager | ~$0.40 |
| **Tổng** | **~$0.41/tháng** |

### Chi phí Google Gemini API
- Gemini 2.0 Flash: free tier với rate limit thấp
- Chi phí phát sinh chỉ khi vượt free tier

### Tổng kết
Dự án nằm hoàn toàn trong AWS Free Tier + Google Gemini Free Tier, hầu như không phát sinh chi phí vận hành.

---

## 6. Rủi ro

| Rủi ro | Mô tả | Mức độ | Giảm thiểu |
|--------|-------|--------|------------|
| **API Key lộ** | Google API key bị commit lên Git | Cao | Secrets Manager + .gitignore |
| **Chi phí ngoài ý muốn** | Lambda bị gọi liên tục / tấn công | Trung bình | CloudWatch Alarm, budget alert |
| **AI response lỗi** | Gemini trả về JSON không hợp lệ | Trung bình | Retry logic (2 lần), fallback |
| **Lambda timeout** | AI response quá chậm (>30s) | Thấp | Tăng timeout, dùng async SQS |
| **CDK deploy lỗi** | Khác biệt version AWS CDK | Thấp | Pin version, kiểm tra trước khi deploy |
| **CORS** | Trình duyệt chặn request cross-origin | Thấp | CORS middleware đã cấu hình sẵn |
| **Dữ liệu bị mất** | DynamoDB bị xóa nhầm | Trung bình | Backup, Point-in-Time Recovery |

---

*Tài liệu đề xuất dự án — Cloud Nexus*
