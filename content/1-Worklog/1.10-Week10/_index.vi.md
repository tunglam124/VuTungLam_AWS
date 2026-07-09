---
title: "WEEK 10 WORKLOG"
date: "2026-06-22"
weight: 10
chapter: false
pre: " <b> 1.10 </b> "
---

# **WEEK 10 WORKLOG**

### **Mục tiêu Tuần 10**

* Hoàn thiện **React Flow canvas** cho Cloud Nexus với custom nodes và edges.
* Phát triển các UI components: GlassPanel, HUD, FloatingCommandBar, Terminal, ScanningSpinner, ResultModal.
* Xây dựng **useAI** hook kết nối frontend với backend API (generate, scan, simulate).
* Triển khai ứng dụng Cloud Nexus lên AWS (ECS Fargate hoặc EC2).
* Tìm hiểu về **Kubernetes** và **Minikube** để quản lý container orchestration.
* Thiết lập **Velero** backup cho Kubernetes cluster.

---

### **Công việc thực hiện trong tuần**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | Phát triển React Flow canvas: tạo CustomNode (10 loại node với icon + màu) và CustomEdge (smoothstep + animated); implement smartHandles và edgeRouting. | 22/06/2026 | 22/06/2026 | |
| 2 (Thứ Ba) | Xây dựng UI components: GlassPanel (hiệu ứng kính mờ), TopHUD (thanh trạng thái trên cùng), FloatingCommandBar (thanh lệnh terminal), HackerOverlay, ResultModal. | 23/06/2026 | 23/06/2026 | |
| 3 (Thứ Tư) | Phát triển useAI hook: kết nối frontend với backend API (generate, scan, simulate); xử lý async/await, error handling, logging ra terminal; implement useStore (Zustand) cho state management. | 24/06/2026 | 24/06/2026 | |
| 4 (Thứ Năm) | Triển khai Cloud Nexus lên AWS: cấu hình ECS Fargate cluster cho containers frontend & backend; thiết lập Application Load Balancer và Auto Scaling. | 25/06/2026 | 25/06/2026 | |
| 5 (Thứ Sáu) | Tìm hiểu Kubernetes: cài đặt Minikube, viết deployment.yaml cho Cloud Nexus, deploy ứng dụng; thiết lập Velero backup cho cluster resources. | 26/06/2026 | 26/06/2026 | |

---

### **Kết quả đạt được Tuần 10**

* Hoàn thiện **React Flow canvas** với khả năng kéo-thả 10 loại node, custom edges dạng smoothstep có animated, và thuật toán smartHandles để tự động chọn vị trí kết nối tối ưu.
* Xây dựng bộ **UI components** hoàn chỉnh với phong cách hacker/cyber:
    * **GlassPanel**: Component nền kính mờ dùng cho tất cả panel (Scenarios, Edit, AttackPath).
    * **TopHUD**: Thanh trạng thái hiển thị chế độ (view/edit), số node, số edge.
    * **FloatingCommandBar**: Thanh lệnh dạng terminal cho phép gõ "generate", "scan", "simulate", "help", "clear".
    * **HackerOverlay**: Overlay với hiệu ứng Matrix-style cho attack simulation.
    * **ResultModal**: Modal hiển thị kết quả AI (topology generated, scan complete, simulation result).
    * **ScanningSpinner**: Spinner animation trong lúc scan/simulate.
* Phát triển **useAI hook** kết nối frontend với 4 API endpoints:
    * Gọi /api/ai/generate để sinh topology từ text prompt.
    * Gọi /api/simulation/scan để quét lỗ hổng.
    * Gọi /api/simulation/run để chạy mô phỏng.
    * Xử lý async/await, error handling, logging real-time ra TerminalLine component.
* Sử dụng **Zustand** (useStore) cho state management toàn cục: nodes, edges, scenarios, logs, mode, scanning/simulating status.
* Triển khai Cloud Nexus lên **AWS ECS Fargate**:
    * Tạo ECS cluster với Fargate launch type cho frontend (port 5173) và backend (port 8000).
    * Thiết lập Application Load Balancer để routing traffic.
    * Cấu hình Auto Scaling dựa trên CPU utilization.
* Tìm hiểu **Kubernetes**: cài đặt Minikube, tạo deployment.yaml cho Cloud Nexus, deploy thành công bằng `kubectl apply`. Hiểu về Pod, Node, Cluster.
* Thiết lập **Velero**: cài đặt bằng Helm, thực hành backup (`velero backup create`) và restore (`velero restore create`) cho cluster resources.
