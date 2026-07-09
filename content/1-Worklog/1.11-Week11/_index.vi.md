---
title: "WEEK 11 WORKLOG"
date: "2026-06-22"
weight: 11
chapter: false
pre: " <b> 1.11 </b> "
---

# **WEEK 11 WORKLOG**

### **Mục tiêu Tuần 11**

* Xây dựng **hạ tầng serverless** cho Cloud Nexus sử dụng **AWS CDK (TypeScript)**.
* Phát triển **CDK stacks**: Simulation Stack (SQS, DynamoDB, S3, Step Functions, SNS) và Auth Stack (Cognito).
* Tạo **Lambda functions** bằng Python 3.12 ARM64 với FastAPI qua Mangum adapter.
* Cấu hình **API Gateway HTTP API** và IAM roles cho Lambda execution.
* Thiết lập **Secrets Manager** để lưu trữ Google API key an toàn.
* Xây dựng **CI/CD pipeline** với các lệnh CDK synth, deploy và destroy.

---

### **Công việc thực hiện trong tuần**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | Thiết lập CDK project với TypeScript: khởi tạo cdk app, cấu hình TypeScript config, định nghĩa CloudNexusStack; tìm hiểu Python 3.12 ARM64 Lambda compatibility. | 22/06/2026 | 22/06/2026 | |
| 2 (Thứ Ba) | Xây dựng **Simulation Stack**: tạo SQS queue (đệm scan requests), DynamoDB table (lưu topology + kết quả), S3 bucket (artifacts), Step Functions state machine (điều phối), SNS topic (cảnh báo). | 23/06/2026 | 23/06/2026 | |
| 3 (Thứ Tư) | Xây dựng **Auth Stack** với Cognito User Pool; xây dựng **Secrets Stack**: tạo Secrets Manager secret cho GOOGLE_API_KEY; tìm hiểu Lambda Layer structure cho Python dependencies. | 24/06/2026 | 24/06/2026 | |
| 4 (Thứ Năm) | Tạo **Lambda Layer** cho Python 3.12 ARM64: đóng gói fastapi, mangum, google-genai, pydantic vào cấu trúc layer chuẩn; phát triển Lambda function với FastAPI app + Mangum handler. | 25/06/2026 | 25/06/2026 | |
| 5 (Thứ Sáu) | Lắp ráp **API Stack**: cấu hình API Gateway HTTP API, IAM roles, Cognito authorizer; tích hợp tất cả output (bucket names, queue URLs, table ARNs) qua CDK context; chạy `cdk synth` và `cdk deploy` lần đầu. | 26/06/2026 | 26/06/2026 | |

---

### **Kết quả đạt được Tuần 11**

* Khởi tạo thành công **AWS CDK (TypeScript)** project với `cdk init app --language typescript`, cấu hình `tsconfig.json` và `cdk.json` cho dự án Cloud Nexus.
* Xây dựng **Simulation Stack** (`CloudNexusSimulationStack`) bao gồm:
  * **SQS** standard queue làm bộ đệm cho simulation requests.
  * **DynamoDB** table với partition key `PK` (lưu topology/kết quả).
  * **S3** bucket chứa topology JSON artifacts.
  * **Step Functions** state machine điều phối simulation đa bước.
  * **SNS** topic cho thông báo cảnh báo bảo mật.
* Xây dựng **Secrets Stack** dùng `aws-cdk-lib/aws-secretsmanager` tạo secret `GOOGLE_API_KEY` với auto-rotation.
* Xây dựng **Cognito Auth Stack**: User Pool với đăng nhập email/password, App Client cho frontend.
* Phát triển **Python 3.12 ARM64 Lambda Layer**: tạo cấu trúc `/python/lib/python3.12/site-packages/` chứa `fastapi==0.115.0`, `mangum==0.17.0`, `google-genai==1.0.0`, `pydantic==2.9.0`. Cấu hình Lambda với `architecture: Architecture.ARM_64` và `runtime: Runtime.PYTHON_3_12`.
* Implement **FastAPI application** với Mangum handler: định nghĩa routes (`/api/health`, `/api/ai/generate`, `/api/topology/validate`, `/api/simulation/scan`, `/api/simulation/run`, `/api/simulation/run-with-defense`), tích hợp CORS middleware.
* Xây dựng **API Stack** (`CloudNexusApiStack`) với:
  * **API Gateway HTTP API** tích hợp Lambda.
  * **Cognito User Pool Authorizer** cho các endpoint bảo vệ.
  * **IAM roles** cấp quyền Lambda đọc Secrets Manager và toàn quyền truy cập SQS, DynamoDB, SNS, Step Functions.
* Chạy thành công `cdk synth` (sinh CloudFormation template) và `cdk deploy --all` để triển khai tất cả stacks lên AWS.
* Xác minh tất cả stack outputs (API Gateway URL, S3 bucket name, SQS queue URL, DynamoDB table name, Cognito User Pool ID) để cấu hình frontend.
