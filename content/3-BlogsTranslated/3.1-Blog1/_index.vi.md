---
title: "Blog 1"
date: "2026-06-09"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Well-Architected Best Practices cho Bảo mật Chuỗi Cung ứng Phần mềm

<span class="meta-info">Tác giả: Trevor Schiavone và Desiree Brunner | ngày: 26 tháng 05, 2026 | in</span> [Security, Identity, & Compliance](https://aws.amazon.com/blogs/security/category/security-identity-compliance/), [Best Practices](https://aws.amazon.com/blogs/security/category/post-types/best-practices/) | [Permalink](https://aws.amazon.com/blogs/security/well-architected-best-practices-for-software-supply-chain-security/)

Các cuộc tấn công chuỗi cung ứng gần đây — Shai-Hulud, Chalk/Debug, tea.xyz token farming, và axios — cho thấy một thực tế đáng lo ngại: một tài khoản maintainer bị xâm phạm có thể phát tán mã độc đến hàng nghìn môi trường tiêu dùng cùng lúc. Các cuộc tấn công khai thác hai mặt trận — thông tin đăng nhập maintainer bị đánh cắp để phát hành gói độc hại, và môi trường tiêu dùng tải và thực thi các gói đó.

Bài viết này trình bày các best practices dành cho **người tiêu dùng gói phần mềm**, dựa trên [AWS Well-Architected Framework — Security Pillar](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html).

---

## 1. Sử dụng Thông tin Đăng nhập Tạm thời & Nguyên tắc Đặc quyền Tối thiểu

Worm Shai-Hulud quét môi trường phát triển và CI/CD pipelines để tìm kiếm secrets — npm tokens, GitHub tokens, IAM access keys. Thông tin đăng nhập dài hạn bị lộ tạo điều kiện cho tin tặc phát tán malware và truy cập tài nguyên đám mây.

**Thực hành chính:**

- **Sử dụng thông tin tạm thời** — `aws login` cho phát triển local, IAM Identity Center cho CLI credentials ngắn hạn, OIDC federation (GitHub Actions, GitLab CI) cho CI/CD pipelines. Thông tin tạm thời tự động hết hạn, giới hạn cửa sổ phơi nhiễm. [SEC02-BP02](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_identities_unique.html)
- **Đặc quyền tối thiểu** — chỉ gán quyền tối thiểu cần thiết; sử dụng quyền cao tạm thời khi cần. [SEC03-BP02](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_permissions_least_privileges.html)
- **Kiểm toán và luân chuyển thông tin dài hạn** — nếu bắt buộc phải dùng, lưu trữ trong AWS Secrets Manager với tự động luân chuyển và ghi nhật ký kiểm toán. [SEC02-BP05](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_identities_audit.html)

Sử dụng Amazon GuardDuty và AWS CloudTrail để phát hiện hoạt động IAM bất thường.

---

## 2. Triển khai Phòng thủ Theo Chiều sâu

Ngay cả với thông tin tạm thời và đặc quyền tối thiểu, một tài khoản bị xâm phạm vẫn có thể phát hành gói độc hại. Phòng thủ theo chiều sâu tạo nhiều lớp bảo vệ ngăn chặn sự lan rộng sau khi bị xâm phạm.

### Ký Artifact với AWS Signer

[AWS Signer](https://docs.aws.amazon.com/signer/latest/developerguide/Welcome.html) cung cấp ký điện tử cho gói và container image bằng HSM đạt chuẩn FIPS 140-3 Level 3. Mô hình ủy quyền ký tách biệt trách nhiệm — thông tin developer không có quyền ký; chỉ CI/CD pipeline roles mới có.

**Quy trình ký container image** (với Amazon ECR managed signing mới):
1. Developer/CI/CD tạo image và push lên Amazon ECR
2. Amazon ECR tự động kích hoạt ký qua Signer
3. Signer xác minh quyền và ký image digest
4. Chữ ký được lưu cùng image theo định dạng OCI artifact
5. Admission controllers (Kyverno cho EKS, lifecycle hooks cho ECS) xác minh chữ ký trước khi deploy

**Lợi ích so với tự xây dựng:** quản lý hoàn toàn, tự động, quản trị tập trung, tích hợp sẵn EKS/ECS, đạt chuẩn FIPS 140-3 Level 3.

### Tập trung Quản lý Phụ thuộc

Sử dụng [AWS CodeArtifact](https://aws.amazon.com/codeartifact/) để lưu trữ và quản lý gói phần mềm. Package group configuration xác định danh sách nguồn upstream được phép — kiểm soát trực tiếp chống tấn công typosquatting. Tập trung hóa cho phép cố định phiên bản và nhanh chóng loại bỏ gói độc hại trên toàn bộ danh mục. [SEC11-BP05](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_appsec_centralize_services_for_packages_and_dependencies.html)

Với npm packages, **provenance attestation** (npm 9.5+) liên kết gói đã xuất bản với repository và CI/CD workflow nguồn thông qua Sigstore — xác minh gói không bị can thiệp giữa bước build và xuất bản.

### Quét Phụ thuộc Xuyên suốt SDLC

- **Trong phát triển** — Kiro phân tích thành phần phần mềm trong code review
- **Trong repository và pipeline** — Amazon Inspector quét code, dependency, và IaC
- **Cho container images** — Amazon Inspector quét ECR images liên tục và tích hợp CI/CD

Công cụ quét CVE truyền thống bỏ sót zero-day trong chuỗi cung ứng. AWS phát hiện qua **phân tích hành vi quy mô lớn** — tín hiệu cross-account từ MadPot và dữ liệu ứng phó sự cố từ hàng triệu khách hàng. Kết quả được đóng góp vào OpenSSF Malicious Packages Repository (MAL-ID). Với chiến dịch tea.xyz, thời gian trung bình từ phát hiện đến xác nhận chính thức là ~30 phút.

**SBOMs** (SPDX/CycloneDX) cho phép đánh giá nhanh phạm vi ảnh hưởng — xác định ứng dụng nào chứa gói độc và ưu tiên xử lý.

### Thiết lập Ghi nhật ký và Giám sát

Sử dụng CloudTrail, GuardDuty, Security Hub, và AWS Config. Các sự kiện CloudTrail cần theo dõi:

- `sts:AssumeRole` từ IP hoặc region bất thường
- `secretsmanager:GetSecretValue` từ nguồn không quen thuộc
- `ecr:PutImage` từ máy developer (bỏ qua CI/CD pipeline)
- `lambda:UpdateFunctionCode` ngoài khung thời gian deploy thông thường
- `iam:CreateAccessKey` kèm hoạt động API ngay sau đó

Kết hợp Amazon EventBridge rules để tự động phản hồi khi Amazon Inspector phát hiện gói độc hoặc mẫu truy cập bất thường. [SEC04: Detection](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/detection.html)

---

## Kết luận

Các cuộc tấn công chuỗi cung ứng gần đây phản ánh nỗ lực không ngừng của tin tặc nhắm vào package registries, CI/CD pipelines, và thông tin đăng nhập developer. Các biện pháp được mô tả hoạt động cùng nhau:

- **Thông tin tạm thời** giới hạn giá trị của token bị đánh cắp
- **Quản lý phụ thuộc tập trung** giảm diện tích tấn công ở cấp registry
- **Ký artifact** đảm bảo artifact không được ký không thể vào production
- **Quét liên tục** phát hiện gói độc từ sớm
- **Ghi nhật ký và giám sát** cho phép phát hiện và điều tra nhanh chóng

Mỗi lớp thu hẹp cơ hội cho tin tặc. Well-Architected Framework cung cấp bản thiết kế — việc triển khai tùy thuộc vào bạn.
