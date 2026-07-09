---
title: "WEEK 9 WORKLOG"
date: "2026-06-15"
weight: 1
chapter: false
pre: " <b> 1.9 </b> "
---

# **WEEK 9 WORKLOG**

### **Mục tiêu Tuần 9**

* Hoàn thiện **AI Simulation Engine** cho Cloud Nexus: xây dựng system prompts chuyên sâu cho Gemini AI.
* Phát triển các API endpoints mô phỏng tấn công: scan topology, run simulation, run-with-defense.
* Xử lý logic normalize node/edge từ phản hồi AI và ánh xạ kiểu thiết bị mạng.
* Tích hợp **Prometheus** và **Grafana** để giám sát hiệu năng backend FastAPI.
* Tìm hiểu **AWS CodeDeploy** nâng cao và debugging deployment scripts.

---

### **Công việc thực hiện trong tuần**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | Phát triển AI Simulation Engine: viết SIMULATION_PROMPT với hướng dẫn chi tiết về attack path tracing, Zero Trust logic, action mô tả kỹ thuật tấn công (nmap, CVE exploit, brute-force). | 08/06/2026 | 08/06/2026 | |
| 2 (Thứ Ba) | Xây dựng API endpoint /api/simulation/run và /api/simulation/run-with-defense; xử lý SimulationRequest/SimulationResponse models; implement normalize_node để map flat/nested JSON từ AI. | 09/06/2026 | 09/06/2026 | |
| 3 (Thứ Tư) | Phát triển SCAN_PROMPT và VALIDATION_PROMPT: phân tích bề mặt tấn công, kiểm tra lỗ hổng theo Zero Trust, sinh kịch bản tấn công (SQL Injection, Lateral Movement, DDoS IoT Botnet). | 10/06/2026 | 10/06/2026 | |
| 4 (Thứ Năm) | Debug và tối ưu AI service: xử lý JSON parse errors, retry logic cho truncated responses, type_mapping cho các thiết bị mạng (internet→cloud, pc→workstation, db→database). | 11/06/2026 | 11/06/2026 | |
| 5 (Thứ Sáu) | Thiết lập Prometheus + Grafana cho monitoring: cấu hình metrics endpoint cho FastAPI, tạo dashboard giám sát CPU, memory, request latency; tìm hiểu cAdvisor cho container metrics. | 12/06/2026 | 12/06/2026 | |

---

### **Kết quả đạt được Tuần 9**

* Hoàn thiện **AI Simulation Engine** với system prompts chuyên sâu:
    * SIMULATION_PROMPT: Hướng dẫn Gemini mô phỏng tấn công ethical hacking step-by-step với kỹ thuật thực tế (nmap -sV scan, exploit CVE, SSH brute-force, data exfiltration qua DNS tunneling).
    * SIMULATION_WITH_DEFENSE_PROMPT: Mô phỏng lại với defenses, xác định blocking point tại security node đầu tiên.
    * SCAN_PROMPT: Phân tích bề mặt tấn công và sinh kịch bản (SQL Injection, Lateral Movement, DDoS IoT Botnet).
* Xây dựng **API endpoints** đầy đủ:
    * POST /api/simulation/scan — quét topology tìm lỗ hổng.
    * POST /api/simulation/run — chạy mô phỏng tấn công.
    * POST /api/simulation/run-with-defense — chạy lại với biện pháp phòng thủ.
* Implement **normalize_node** function xử lý 2 định dạng JSON (flat và nested) từ AI response, cùng **type_mapping** để map tên thiết bị thông dụng (internet→cloud, pc→workstation, db→database, fw→firewall).
* Debug thành công các vấn đề: JSON parse errors do response bị truncate (implement retry logic), xử lý thiếu id/position trong node data.
* Thiết lập hệ thống **monitoring** với **Prometheus** (thu thập metrics) và **Grafana** (trực quan hóa dashboard):
    * Cấu hình metrics endpoint cho FastAPI backend.
    * Tạo dashboard giám sát CPU usage, memory usage, request latency, error rates.
    * Tìm hiểu cAdvisor cho monitoring Docker containers.
