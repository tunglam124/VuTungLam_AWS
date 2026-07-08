---
title : "Đóng góp cá nhân"
date : "2025-10-10"
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---
# 5.5. Đóng góp cá nhân (0.5 điểm)

---

### Mức Độ Tự Làm

Project được xây dựng từ đầu, không copy mẫu có sẵn:
- Tự thiết kế kiến trúc serverless phù hợp bài toán threat modeling
- Code CDK stack hoàn chỉnh (3 stacks riêng biệt)
- Viết Lambda handler (FastAPI + Mangum)
- Tích hợp Google Gemini API (prompt engineering cho bảo mật mạng)
- Build Lambda Layer cho ARM64 Python 3.12

---

### Tùy Biến

| Tính năng | Mô tả |
|-----------|-------|
| **FastAPI + Mangum** | FastAPI thay vì plain handler (validation, OpenAPI docs) |
| **Lambda Layer ARM64** | Build cho ARM64 — rẻ hơn 20% so với x86 |
| **Gemini Prompt Engineering** | 5 prompt: generation, validation, simulation, scan, defense |
| **Normalize node types** | Map user label → chuẩn hóa (web_server → server) |
| **Cross-stack references** | SQS, DynamoDB truyền qua CDK export/import |

---

### Khó Khăn & Giải Quyết

| Khó khăn | Giải pháp |
|----------|----------|
| **`ImportModuleError: No module named 'google'`** | Layer zip thiếu prefix `python/` — rebuild |
| **`_pydantic_core.cpython-313-aarch64...`** | Download nhầm Python 3.13, cần `--python-version 3.12` |
| **`_cffi_backend` missing** | Extract wheel bỏ sót `.so` — extract toàn bộ |
| **CloudFront Access Denied** | Account chưa verify — fallback S3 |
| **API key hết quota free tier** | Chờ reset hoặc nâng cấp paid tier |

---

### Suy ngẫm

> "Qua project này, tôi hiểu rõ hơn về cách Lambda hoạt động với native extensions, tầm quan trọng của việc matching Python version và architecture khi build layer, và cách CDK giúp quản lý hạ tầng AWS dễ dàng như code."

---

### Hướng Phát Triển

1. **CloudFront** — HTTPS, custom domain, WAF (cần AWS Support)
2. **Real-time WebSocket** — API Gateway WebSocket
3. **Multi-region** — Disaster recovery
4. **CI/CD Pipeline** — CodeCommit + CodeBuild + CodePipeline
5. **AWS WAF** — Rate limiting, SQL injection protection
6. **X-Ray Tracing** — Distributed tracing
