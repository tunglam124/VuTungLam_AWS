---
title: "Worklog Tuần 12"
date: "2026-07-06"
weight: 12
chapter: false
pre: " <b> 1.12 </b> "
---

# **WEEK 12 WORKLOG**

### **Mục tiêu tuần 12**

* Triển khai **frontend** lên AWS qua S3 static hosting và CloudFront CDN.
* Hoàn thiện **tích hợp frontend-backend** và đảm bảo CORS hoạt động end-to-end.
* Tích hợp các **dịch vụ AI** và kiểm tra toàn bộ luồng chức năng của ứng dụng.

---

### **Các công việc cần triển khai trong tuần này**

| Day | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Ba) | - Xây dựng stack `CloudNexus-Secrets` và tạo Secrets Manager lưu GOOGLE_API_KEY<br>- Xây dựng stack `CloudNexus-Backend` với Lambda dùng FastAPI qua Mangum, API Gateway HTTP API và IAM roles<br>- Cấu hình Lambda Layer chứa Python dependencies: fastapi, mangum, google-genai<br>- Deploy lần đầu cả hai stack lên AWS<br>- Khởi tạo cấu trúc frontend với Vite + React + ReactFlow + Zustand + TailwindCSS<br>- Cấu hình build script triển khai frontend lên S3 bucket<br>- Deploy S3 bucket và thiết lập CloudFront distribution phục vụ frontend | 06/06/2026 | 06/06/2026 | |
| 2 (Thứ Tư) | - Fix lỗi CORS preflight OPTIONS từ CloudFront qua API Gateway bị trả 400 Bad Request<br>- Loại bỏ CORS config khỏi API Gateway để tránh double-handling với FastAPI CORSMiddleware<br>- Bổ sung handler `@app.options` trong FastAPI xử lý preflight<br>- Cập nhật `allow_origins` trong CORSMiddleware bao gồm CloudFront URL và localhost<br>- Thêm Lambda Layer mới chứa đầy đủ dependencies<br>- Rebuild và redeploy Lambda function | 07/06/2026 | 07/06/2026 | |
| 3 (Thứ Năm) | - Cấu hình `VITE_API_URL` trong `.env.production` trỏ đến API Gateway endpoint production<br>- Thiết lập build configuration cho Vite ở production mode<br>- Deploy lại frontend bundle đã build lên S3 và thực hiện invalidation cache CloudFront<br>- Kiểm tra kết nối frontend từ CloudFront tới backend API | 08/06/2026 | 08/06/2026 | |
| 4 (Thứ Sáu) | - Hoàn thiện FastAPI backend bằng endpoint `GET /` trả metadata API<br>- Verify tất cả endpoint: `/api/health`, `/api/ai/generate`, `/api/topology/validate`, `/api/simulation/scan`<br>- Kiểm tra CORS headers trên tất cả endpoint từ CloudFront origin<br>- Test đầu cuối luồng AI generate topology từ frontend | 09/06/2026 | 09/06/2026 | |
| 5 (Thứ Bảy) | - Tích hợp và kiểm tra toàn bộ luồng: AI generate topology, topology validation, simulation scan, simulation run, simulation with defense<br>- Test thực tế từ giao diện frontend trên CloudFront để đảm bảo tất cả chức năng ổn định<br>- Fix endpoint `/api/simulation/with-defense` trả đầy đủ `attack_steps` và `defense_mechanisms`<br>- Tối ưu tên Lambda function và CloudFormation outputs | 10/06/2026 | 10/06/2026 | |

---

### **Kết quả đạt được tuần 12**

* **Backend** đã triển khai hoàn chỉnh trên AWS Lambda với FastAPI, chạy thông qua Mangum adapter.
* **API Gateway HTTP API** đã hoạt động, expose đầy đủ endpoint để frontend truy cập qua CloudFront.
* **Secrets Manager** lưu trữ `GOOGLE_API_KEY` an toàn, Lambda đọc thông qua IAM grant read.
* **Frontend** đã deploy lên S3 và phục vụ qua **CloudFront CDN**.
* **CORS** đã được xử lý đúng qua FastAPI **CORSMiddleware**, cho phép request từ CloudFront origin.
* **Lambda Layer** chứa `fastapi`, `mangum`, `google-genai` đảm bảo Lambda có đầy đủ dependencies.
* Toàn bộ luồng **end-to-end** từ frontend đến backend hoạt động ổn định: AI generate topology, topology validation, simulation scan, simulation run, simulation with defense.
* **Infrastructure** được quản lý hoàn toàn qua **AWS CDK** và có thể redeploy bất kỳ lúc nào.
