---
title: "Blog 2"
date: "2026-06-18"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Xây dựng Hệ thống Quản lý Khóa Blockchain An toàn, Có thể Xác minh trên AWS Nitro Enclaves tại Turnkey

<span class="meta-info">Tác giả: Harshvardhan Chunawala và Jack Kearney | ngày: 08 tháng 06, 2026 | in</span> [Security](https://aws.amazon.com/blogs/web3/category/security-identity-compliance/security/), [Blockchain](https://aws.amazon.com/blogs/web3/category/blockchain/), [Architecture](https://aws.amazon.com/blogs/web3/category/architecture/) | [Permalink](https://aws.amazon.com/blogs/web3/building-secure-verifiable-blockchain-key-management-on-aws-nitro-enclaves-at-turnkey/)

Quản lý private key là một trong những thách thức bảo mật lớn nhất trong Web3. Mỗi giao dịch đều cần chữ ký điện tử, và ai sở hữu private key thì kiểm soát tài sản tương ứng. Một lần xâm phạm duy nhất đồng nghĩa với mất mát không thể đảo ngược.

[Turnkey](http://turnkey.com/) đã xây dựng hệ thống quản lý khóa có thể xác minh trên [AWS Nitro Enclaves](https://aws.amazon.com/ec2/nitro/nitro-enclaves/) — cung cấp khả năng tạo khóa cô lập trong enclave, vận hành có attestation, và kiểm soát truy cập dựa trên chính sách, không cần đánh đổi như hạ tầng DIY, custodial opaque, hay MPC phức tạp.

---

## Kiến trúc: Quản lý Khóa Enclave-Native

Nitro Enclaves là môi trường tính toán được tăng cường bảo mật, không có bộ nhớ liên tục, không truy cập tương tác, không kết nối mạng ngoài. Turnkey chạy mọi dịch vụ quan trọng — tạo khóa, ký, và policy engine — bên trong enclaves. **Raw key material không bao giờ lộ ra ngoài ranh giới enclave**, kể cả với hạ tầng của Turnkey.

Private keys chỉ được giải mã bên trong enclave tại thời điểm sử dụng. Ciphertext của khóa được lưu trong database được mã hóa bằng symmetric key dẫn xuất từ **Quorum Key** — master secret chỉ tồn tại bên trong enclave và không bao giờ được xuất ra ngoài.

### Tạo & Lưu trữ Khóa

Turnkey dùng mô hình HD wallet. Signer enclave tạo wallet seed từ entropy an toàn của [Nitro Security Module (NSM)](https://github.com/aws/aws-nitro-enclaves-nsm-api). Các child key pairs được dẫn xuất theo nhu cầu qua BIP-32/BIP-44.

Seed không bao giờ được lưu dạng plaintext — nó được mã hóa bằng Quorum Key và lưu vào database. Khi ký, enclave lấy ciphertext, giải mã hoàn toàn trong ranh giới của nó, dẫn xuất child key, ký, sau đó **loại bỏ raw key material**.

### Các Ứng dụng Enclave

| Enclave | Vai trò |
|---|---|
| **Signer** | Tạo khóa và ký, dùng entropy từ NSM |
| **Policy Engine** | Xác thực và phân quyền qua ngôn ngữ chính sách |
| **Parser** | Trích xuất metadata từ giao dịch chưa ký |
| **Notarizer** | Xác thực dữ liệu tổ chức trước khi enclave khác xử lý |
| **TLS Fetcher** | Enclave duy nhất có kết nối mạng ngoài có kiểm soát (qua vsock) |

Các enclave không tự động tin tưởng lẫn nhau. Mỗi enclave được attest độc lập khi khởi động — các yêu cầu giữa enclave được xác minh qua **Quorum Public Key**. Ngay cả host bị xâm phạm cũng không thể giả mạo enclave.

---

## Attestation & Xác minh Enclave

Khi enclave khởi động, NSM ghi lại các cryptographic measurements (PCR0–PCR3) và ký chúng thành **attestation document** chứa:

- **PCR0** – Hash của Enclave Image File (EIF)
- **PCR1** – Hash của Linux kernel
- **PCR2** – Hash của ứng dụng người dùng
- **PCR3** – Hash của IAM role của Nitro host
- **Certificate** – X.509 cert với public key riêng của enclave
- **cabundle** – Chuỗi chứng chỉ đến root certificate của AWS (hiệu lực đến 2049)

Bất kỳ ai cũng có thể xác minh chứng chỉ enclave đến từ Amazon bằng cách đi theo chuỗi này — chuyển trust từ root key của Amazon đến key riêng của enclave. Chữ ký dùng P-384 (FIPS 186-4).

---

## Triển khai Quorum & Reproducible Builds

Mỗi enclave được cấu hình với **Share Set** — các operator, mỗi người giữ một phần của Quorum Key. Chỉ khi đạt ngưỡng số lượng shares, enclave mới tái tạo khóa và khởi chạy.

Các operator tự xây dựng enclave software và xác minh PCR measurements khớp trước khi gửi key share. **Không một kỹ sư nào** có thể tự ý thay đổi enclave hay tái tạo core secrets.

Nền tảng là [QuorumOS (QOS)](https://github.com/tkhq/qos) — unikernel Linux tối thiểu, bất biến. Mọi artifact được **xây dựng tất định** bằng [StageX](https://stagex.tools/), khởi tạo hoàn toàn từ mã nguồn, bắt đầu từ seed assembly 181 byte đã được tin cậy. Bất kỳ ai cũng có thể tải mã nguồn QOS, build locally, và xác minh hash khớp với PCR measurements của enclave đang chạy.

---

## Turnkey Verified: Boot Proofs Thực tế

Turnkey công bố cryptographic proofs công khai qua [Turnkey Verified](https://docs.turnkey.com/security/turnkey-verified). Hai loại proof tiêu biểu:

**1) Address Derivation Proof** — xác nhận địa chỉ wallet được dẫn xuất tất định bên trong enclave mà không cần private key rời khỏi trust perimeter.

**2) Policy Outcome Proof** — xác nhận Policy Engine đã đánh giá yêu cầu ký theo quy tắc tổ chức hoàn toàn bên trong enclave.

Mỗi proof là JSON payload có chữ ký, có thể xác minh mà không cần tin tưởng các khẳng định vận hành của Turnkey.

---

## Mô hình Đe dọa

Turnkey chỉ coi **enclave applications và Share Sets của chúng là đáng tin cậy**. Mọi thứ khác — host VM, Coordinator, database, thậm chí hạ tầng AWS bên ngoài Nitro — đều được coi là có thể bị xâm phạm. Điều này khả thi nhờ Nitro Enclaves cung cấp:

- **Không lưu trữ liên tục** — bộ nhớ volatile bị xóa khi khởi động lại
- **Không truy cập mạng** — chỉ vsock đến host
- **Entropy và thời gian từ hardware** qua NSM

Ngay cả host bị xâm phạm hoàn toàn cũng không thể trích xuất khóa từ enclave hay sửa đổi mã enclave.

---

## Use Cases Thực tế

- **Embedded consumer wallets** — một wallet mỗi người dùng, quyền sở hữu thực sự (developer không thể tự ý di chuyển tài sản). Policy rules được thực thi bên trong enclave.
- **Quản lý giao dịch AI agent** — giới hạn những gì agent có thể ký (theo tài sản, đối tác, quy mô) mà không lộ private keys cho agent runtime.
- **Thanh toán doanh nghiệp & smart contracts** — quorum-controlled provisioning, attestation-backed audit trail cho tuân thủ.

---

## Kết luận

Turnkey đã vận hành production gần bốn năm, bảo vệ hàng triệu wallet. Sự kết hợp giữa **cô lập hardware** (Nitro Enclaves), **reproducible builds** (QuorumOS + StageX), **quorum-controlled provisioning** và **remote attestation** tạo ra hạ tầng vừa an toàn hơn vừa minh bạch hơn các phương pháp trước đây.

Bắt đầu xây dựng: [Tài liệu Turnkey](https://docs.turnkey.com) | [Tài liệu Nitro Enclaves](https://docs.aws.amazon.com/enclaves/latest/user/nitro-enclave.html)
