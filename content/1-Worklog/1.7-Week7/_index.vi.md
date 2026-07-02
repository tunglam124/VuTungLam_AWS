---
title: "WEEK 7 WORKLOG"
date: "2025-11-10"
weight: 1
chapter: false
pre: " <b> 1.7 </b> "
---

# **WEEK 7 WORKLOG**

### **Mục tiêu Tuần 7**

* Khởi tạo dự án **Cloud Nexus** — nền tảng Threat Modeling sử dụng React + Vite + Tailwind CSS.
* Thiết lập backend **FastAPI** (Python) tích hợp **Google Gemini AI** cho các tính năng sinh topology và mô phỏng tấn công.
* Định nghĩa các loại node mạng (Server, Database, Firewall, IPS, IDS, Router, Cloud, IoT, Attacker, Workstation) cho React Flow canvas.
* Tìm hiểu về kiến trúc Serverless với AWS Lambda và API Gateway để hỗ trợ triển khai backend.
* Sử dụng CloudFormation để tự động hóa triển khai hạ tầng cho dự án.

---

### **Công việc thực hiện trong tuần**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | Khởi tạo dự án Cloud Nexus: cài đặt Vite + React 18 + Tailwind CSS + React Flow; tạo cấu trúc thư mục frontend. | 20/10/2025 | 20/10/2025 | https://github.com/thawngs18/DEMO.git |
| 2 (Thứ Ba) | Thiết lập backend FastAPI: tạo main.py với các endpoint /api/ai/generate, /api/topology/validate, /api/simulation/scan, /api/simulation/run. | 21/10/2025 | 21/10/2025 | |
| 3 (Thứ Tư) | Tích hợp Google Gemini AI: viết ai_service.py với system prompts (GENERATION_PROMPT, VALIDATION_PROMPT, SIMULATION_PROMPT, SCAN_PROMPT); cấu hình Gemini client. | 22/10/2025 | 22/10/2025 | |
| 4 (Thứ Năm) | Định nghĩa node definitions: tạo 10 loại node (Server, Database, Firewall, IPS, IDS, Router, Cloud, IoT, Workstation, Attacker) với icon Lucide React và màu sắc tương ứng. | 23/10/2025 | 23/10/2025 | |
| 5 (Thứ Sáu) | Tìm hiểu AWS Lambda + API Gateway cho Serverless backend; viết CloudFormation template triển khai hạ tầng cho Cloud Nexus. | 24/10/2025 | 24/10/2025 | |

---

### **Kết quả đạt được Tuần 7**

* Khởi tạo thành công dự án **Cloud Nexus** với cấu trúc frontend (React 18 + Vite + Tailwind CSS + React Flow) và backend (FastAPI).
* Thiết lập **FastAPI** với các API endpoints: generate topology, validate, scan, và run simulation — sử dụng CORS middleware cho phép frontend localhost:5173 kết nối.
* Tích hợp thành công **Google Gemini AI** (gemini-2.0-flash) với system prompts chuyên biệt cho từng tác vụ bảo mật:
    * GENERATION_PROMPT: Sinh network topology từ mô tả văn bản.
    * VALIDATION_PROMPT: Kiểm tra lỗ hổng kiến trúc dựa trên Zero Trust.
    * SIMULATION_PROMPT: Mô phỏng đường tấn công step-by-step.
    * SCAN_PROMPT: Phân tích bề mặt tấn công và đề xuất kịch bản.
* Định nghĩa hoàn chỉnh **10 loại node** cho React Flow canvas với icon và màu sắc riêng: Server (cyan), Database (cyan), Firewall (green), IPS (green), IDS (green), Router (cyan), Cloud (cyan), IoT (cyan), Workstation (cyan), Attacker (red).
* Tìm hiểu về **AWS Lambda** và **API Gateway** cho kiến trúc Serverless, viết CloudFormation template để tự động hóa triển khai.
