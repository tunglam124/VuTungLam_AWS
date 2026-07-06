---
title: "FCAJ Community Day – Conference Call"
date: "2026-05-23"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Summary Report: FCAJ Community Day – Conference Call

## Event Objectives

- **Hạ tầng và Chi phí:** Chuyển đổi mô hình thanh toán CloudFront sang giá cố định (Flat-rate) và tối ưu hóa hiệu suất mạng
- **Phát triển Sản phẩm AI:** Hành trình 36 giờ xây dựng công cụ tạo UI thông minh (UTMorpho)
- **Độ tin cậy của AI:** Giải mã tính không định hình của LLM và các chiến lược giảm thiểu sai số
- **Kỹ thuật Ngữ cảnh:** Tầm quan trọng của việc cung cấp dữ liệu đầu vào chất lượng hơn là số lượng
- **Tự động hóa và Chấm điểm Tín dụng:** Ứng dụng hệ thống đa tác vụ (Multi-Agent) để xử lý dữ liệu phức tạp và tự động hóa quy trình kinh doanh

---

## Agenda Overview

| | |
|---|---|
| **Thời gian** | 9:00 AM – 12:00 PM, Thứ Bảy, 23/05/2026 |
| **Địa điểm** | AWS Vietnam Office |

---

## Key Highlights

### 1. Welcome & Introduction (8:30 – 9:00 AM)

- Check-in và networking
- Giới thiệu mục tiêu, nội dung trọng tâm

### 2. Context Is Everything: Making AI Actually Work for You (9:00 – 09:30 AM)

#### Bản chất của Context

Context không chỉ là thông tin bổ sung — nó là "thông tin giúp AI hiểu được nhiệm vụ đằng sau nhiệm vụ". Bốn yếu tố cốt lõi:

| Yếu tố | Mô tả |
|---|---|
| **Goal (Mục tiêu)** | Kết quả cuối cùng bạn thực sự mong muốn |
| **Situation (Tình huống)** | Bạn là ai, thời hạn hoàn thành |
| **Constraints (Ràng buộc)** | Tech stack, phong cách, ngân sách, định dạng |
| **Evidence (Bằng chứng)** | Mã nguồn, tài liệu, ví dụ, yêu cầu cụ thể |

#### Tại sao AI thất bại khi thiếu context?

- AI không thể đọc suy nghĩ — nó cần bạn nói rõ mục tiêu
- Phản hồi chung chung hoặc sai hướng do input kém
- Quá rườm rà hoặc vi phạm ràng buộc vì không được thiết lập giới hạn từ đầu

#### Ba sai lầm phổ biến

1. **"Internet Puller"** — Sao chép toàn bộ bài báo, PDF, ảnh chụp màn hình vào chat. Hệ quả: AI bị xao nhãng, giảm độ chính xác, tăng chi phí token
2. **Nói điều AI đã biết** — Cung cấp thông tin hiển nhiên. Thay vào đó, hãy nói điều quan trọng tiếp theo
3. **Thiếu mục tiêu và ràng buộc** — Lệnh mơ hồ "Xây dựng cho tôi một website" nhận câu trả lời mơ hồ

#### Sự tiến hóa của hệ thống context

| Giai đoạn | Mô tả |
|---|---|
| **Prompt** | Câu hỏi đơn lẻ, không trạng thái |
| **Context** | Kết hợp tài liệu bổ trợ |
| **Memory** | Cá nhân hóa theo thời gian ("bộ não AI thứ hai") |

#### Framework cung cấp context tốt

1. Xác định mục tiêu: AI nên giúp bạn đạt được điều gì?
2. Lọc thông tin liên quan: Chỉ cung cấp dữ liệu thực sự cần thiết
3. Thiết lập ràng buộc: Công nghệ, thời gian, phong cách
4. Tiêu chí thành công: Một câu trả lời tốt trông như thế nào?

> Context không phải thông tin bổ sung — context chính là trải nghiệm sản phẩm. Context Engineering đang trở thành kỹ năng cốt lõi.

---

### 3. Broadening the Cloud Horizon (09:30 AM – 12:00 PM)

#### Tự động hóa quy trình kinh doanh với Amazon Quick Suite

- **Giải pháp Agentic AI:** Amazon Quick Suite giúp đơn giản hóa và tăng tốc từ dữ liệu đến hành động
- **Hệ sinh thái dữ liệu:** Kết nối 40+ nguồn dữ liệu, database, kho dữ liệu, kết hợp Bedrock models và web search
- **Tự động hóa:** Tạo biên bản họp (MoM), gửi email, lên lịch họp tự động

#### Amazon CloudFront: Từ Edge đến Origin

- **Flat-rate pricing** (ra mắt 11/2025) — dự đoán chi phí hàng tháng, tránh hóa đơn tăng đột biến
- **Tối ưu hóa chi phí:** Miễn phí truyền dữ liệu từ origin AWS đến CloudFront; giảm tải CPU cho EC2
- **Bảo mật & Hiệu năng:**
  - 700+ PoPs toàn cầu giảm độ trễ
  - TLS 1.3, mTLS, chống DDoS tại Edge
  - HTTP/3 (QUIC) tải tài nguyên song song nhanh hơn

#### UTMorpho: Xây dựng sản phẩm tại LotusHacks

Hành trình 36 giờ xây dựng công cụ tạo UI bằng AI với khả năng chỉnh sửa trực tiếp:

- **Ý tưởng:** Giải quyết vấn đề các công cụ AI UI hiện tại tạo mô hình tĩnh, không thể chỉnh sửa trực tiếp. Mỗi lần re-prompt làm thay đổi toàn bộ thiết kế
- **Tính năng chính:** Chỉnh sửa trực tiếp trên canvas (WYSIWYG), giữ nguyên thành phần không liên quan, tối ưu token consumption
- **Bài học:** Sự thất vọng thực tế tạo ý tưởng thực tế — sự ăn ý của nhóm quan trọng hơn kỹ năng cá nhân

#### Tính phi định hình của LLM

Tại sao temperature = 0 vẫn không đảm bảo đầu ra giống hệt nhau 100%?

- **Nguyên nhân kỹ thuật:** Phép toán floating-point trên GPU không có tính kết hợp, thứ tự thực thi song song không cố định
- **Nguyên nhân thương mại:** Inference batching của API provider làm thay đổi tính toán mỗi request
- **Chiến lược:** Majority voting, JSON mode, thiết kế hệ thống chấp nhận biến thiên

#### Multi-Agent cho chấm điểm tín dụng Startup

Case study tại VPBank: sử dụng nhiều AI Agent để đánh giá hồ sơ vay vốn startup.

- **Thách thức:** Hệ thống ngân hàng truyền thống thất bại với dữ liệu startup (thiếu lịch sử tài chính 3 năm, không có tài sản thế chấp)
- **Mô hình Multi-Agent:** Financial Analyst, Market Analyst, Team Evaluator, Risk Assessor — cùng phản biện và đưa ra kết quả đồng thuận
- **ROI:**
  - Giảm thời gian xử lý: 2-3 tuần → 2-4 giờ
  - Giảm 95% chi phí mỗi quyết định tín dụng
  - Tăng gấp đôi tỷ lệ phê duyệt nhờ đánh giá đa chiều

---

### 4. Networking & Lucky Draw

- 10 lượt rút thăm trúng thưởng dành riêng cho khách mời tại tầng 36
- Giao lưu với cộng đồng sinh viên và kỹ sư AWS
- Thảo luận về lộ trình thi chứng chỉ Cloud, dự án Serverless và GenAI

---

## Key Takeaways

### AI Implementation
Context là chìa khóa quyết định để biến mô hình ngôn ngữ thông thường thành trợ lý AI đáng tin cậy trong doanh nghiệp.

### Career Orientation
Ngành công nghệ đang dịch chuyển — cơ hội lớn cho nhân sự đa năng, biết viết code, có tư duy tích hợp AI và quản trị luồng dữ liệu.

### Community & Networking
Tiếp xúc với chuyên gia trong hệ sinh thái AWS giúp thu hẹp khoảng cách giữa lý thuyết học thuật và bài toán kiến trúc hạ tầng thực tiễn.

---

## Event Photos

{{< figure src="/images/bfb2481eacf02dae74e1.jpg" title="FCAJ Community Day" alt="Event photo" >}}

---

> Buổi FCAJ Community Day mang lại góc nhìn thực tiễn về ứng dụng AI trong doanh nghiệp — từ Context Engineering, CloudFront optimization, Multi-Agent credit scoring đến xây dựng sản phẩm AI trong 36 giờ. Đây là cầu nối quý giá giữa lý thuyết hàn lâm và thực tế triển khai.
