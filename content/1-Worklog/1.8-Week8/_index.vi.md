---
title: "WEEK 8 WORKLOG"
date: "2026-06-01"
weight: 1
chapter: false
pre: " <b> 1.8 </b> "
---

# **WEEK 8 WORKLOG**

### **Mục tiêu Tuần 8**

* Xây dựng quy trình CI/CD hoàn chỉnh cho dự án **Cloud Nexus** sử dụng **AWS CodePipeline**, **CodeBuild** và **CodeDeploy**.
* Docker hóa frontend React và backend FastAPI để triển khai nhất quán.
* Sử dụng **Terraform** để quản lý hạ tầng CI/CD dưới dạng Infrastructure as Code (IaC).
* Tích hợp bước kiểm tra tự động (automated testing) vào pipeline.
* Tìm hiểu về AWS CodeCommit làm nguồn source code cho pipeline.

---

### **Công việc thực hiện trong tuần**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | Viết Dockerfile cho frontend (React + Vite) và backend (FastAPI + Uvicorn); tạo docker-compose.yml để chạy đa container. | 01/06/2026 | 01/06/2026 | |
| 2 (Thứ Ba) | Thiết lập AWS CodeCommit repository chứa mã nguồn Cloud Nexus; cấu hình IAM roles cho pipeline. | 02/06/2026 | 02/06/2026 | |
| 3 (Thứ Tư) | Xây dựng CI pipeline với AWS CodeBuild: tự động build Docker images, chạy unit test cho backend FastAPI. | 03/06/2026 | 03/06/2026 | |
| 4 (Thứ Năm) | Thiết lập CD pipeline với AWS CodeDeploy: triển khai Docker containers lên EC2; cấu hình AppSpec và scripts. | 04/06/2026 | 04/06/2026 | |
| 5 (Thứ Sáu) | Dùng Terraform để định nghĩa toàn bộ hạ tầng CI/CD (VPC, ECR repositories, CodePipeline, CodeBuild projects, CodeDeploy groups). | 05/06/2026 | 05/06/2026 | |

---

### **Kết quả đạt được Tuần 8**

* Viết thành công **Dockerfile** cho frontend (React + Vite đa stage) và backend (FastAPI + Uvicorn), cùng **docker-compose.yml** để orchestrate đa container.
* Thiết lập **AWS CodeCommit** repository và cấu hình IAM roles với quyền tối thiểu (Least Privilege) cho pipeline.
* Xây dựng **CI pipeline** với AWS CodeBuild:
    * Build Docker images cho frontend và backend.
    * Chạy unit test cho backend FastAPI (Pydantic models validation).
    * Push images lên Amazon ECR.
* Thiết lập **CD pipeline** với AWS CodeDeploy:
    * Triển khai Docker containers lên EC2 instances.
    * Cấu hình AppSpec.yml với các hooks (BeforeInstall, ApplicationStart, ValidateService).
    * Viết deployment scripts để pull images từ ECR và start containers.
* Dùng **Terraform** (HCL) định nghĩa toàn bộ hạ tầng CI/CD:
    * Sử dụng variables và .tfvars để quản lý cấu hình linh hoạt.
    * Tạo VPC, subnets, ECR repositories, CodePipeline, CodeBuild projects, CodeDeploy application và deployment groups.
    * Chạy thành công `terraform init`, `plan`, và `apply` để triển khai.
* Hiểu rõ quy trình **CI/CD** và áp dụng vào dự án thực tế Cloud Nexus.
