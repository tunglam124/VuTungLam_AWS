---
title: "WEEK 4 WORKLOG"
date: "2026-05-20"
weight: 1
chapter: false
pre: " <b> 1.4 </b> "
---

# **WEEK 4 WORKLOG**

### **Week 4 Objectives**

* Lên ý tưởng và thiết kế kiến trúc hệ thống Phản ứng Sự cố Bảo mật IAM tự động trên AWS theo mô hình Zero Trust.
* Thiết lập hạ tầng giám sát và cảnh báo bảo mật thời gian thực (CloudTrail, SNS).
* Xây dựng luồng xử lý tự động hóa sử dụng kiến trúc hướng sự kiện (EventBridge, AWS Lambda).
* Nắm vững quy trình xử lý sự cố (Incident Response) và áp dụng nguyên tắc đặc quyền tối thiểu (Least Privilege) bằng việc tối ưu cấu hình trong Free Tier.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | **Thiết lập Sandbox & Giám sát: Tạo môi trường kiểm thử IAM an toàn và cấu hình AWS CloudTrail để ghi log toàn bộ Management events. | 29/09/2025 | 29/09/2025 | |
| 2 (Thứ Ba) | **Thiết lập luồng cảnh báo: Cấu hình kênh thông báo Amazon SNS và xử lý kiến trúc đồng bộ Region về us-east-1.| 30/09/2025 | 30/09/2025 | |
| 3 (Thứ Tư) | **Xây dựng bộ lọc sự kiện: Phân tích log và viết mã JSON Event Pattern trên Amazon EventBridge để bắt hành vi leo thang đặc quyền. | 01/10/2025 | 01/10/2025 | |
| 4 (Thứ Năm) | **Phát triển mã nguồn tự động hóa: Viết script Python cho AWS Lambda để bóc tách JSON, tước quyền tự động và gửi cảnh báo. | 02/10/2025 | 02/10/2025 | |
| 5 (Thứ Sáu) | **Tích hợp & Kiểm thử: Nối EventBridge với Lambda, tiến hành Live Test gán quyền Admin trái phép, gỡ lỗi qua CloudWatch. | 03/10/2025 | 03/10/2025 | |

---

### **Week 4 Achievements**

* Thứ Hai (Day 1): * Khởi tạo thành công môi trường kiểm thử workshop-test-user (IAM Sandbox).
    * Thiết lập IAM Role IAM-Security-Lambda-Role tuân thủ nguyên tắc đặc quyền tối thiểu.
    * Kích hoạt hệ thống camera giám sát CloudTrail (IAM-Security-Trail), lưu vết API vào S3 Bucket với mã hóa SSE-S3 nhằm tối ưu hoàn toàn chi phí.
* Thứ Ba (Day 2): * Triển khai hệ thống cảnh báo khẩn cấp thông qua Amazon SNS Topic (Security-Alert-Topic).
    * Phát hiện và xử lý thành công bài toán "lệch pha" Region của hệ thống, thực hiện đồng bộ toàn bộ tài nguyên (SNS, S3) về vùng N. Virginia (us-east-1) để bắt được các sự kiện IAM Global.
* Thứ Tư (Day 3): * Hoàn thành thiết kế kiến trúc hệ thống hướng sự kiện (Event-Driven Security).
    * Thiết lập thành công EventBridge Rule với Custom JSON Pattern, lọc chính xác 100% lệnh AttachUserPolicy liên quan đến AdministratorAccess.
* Thứ Năm (Day 4): * Phát triển hoàn thiện mã nguồn Python sử dụng thư viện Boto3 trên AWS Lambda.
    * Code bóc tách thành công dữ liệu vi phạm, xác định kẻ tấn công và thực thi API iam:DetachUserPolicy thành công. Tích hợp gửi email cảnh báo tự động.
* Thứ Sáu (Day 5): * Tích hợp hoàn chỉnh chuỗi pipeline: CloudTrail -> EventBridge -> Lambda -> SNS.
    * Thực hiện Live Test giả lập sự cố thành công: Hệ thống tự động nhận diện và thu hồi quyền AdministratorAccess trái phép trong chưa tới 3 giây.
    * Khắc phục triệt để lỗi không khởi tạo được Log Group trên CloudWatch do cấu hình sai vùng, đảm bảo luồng theo dõi vận hành trơn tru.
