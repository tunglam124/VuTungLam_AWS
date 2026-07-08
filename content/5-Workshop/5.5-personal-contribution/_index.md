---
title : "Personal Contribution"
date : "2025-10-10"
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---
# 5.5. Personal Contribution (0.5 pts)

---

### Originality

Project built from scratch, no pre-made template:
- Designed serverless architecture suitable for threat modeling
- Complete CDK stack code (3 separate stacks)
- Written Lambda handlers (FastAPI + Mangum)
- Integrated Google Gemini API (prompt engineering for network security)
- Built Lambda Layer for ARM64 Python 3.12

---

### Customizations

| Feature | Description |
|---------|------------|
| **FastAPI + Mangum** | FastAPI instead of plain handler (validation, OpenAPI docs) |
| **Lambda Layer ARM64** | Built for ARM64 — 20% cheaper than x86 |
| **Gemini Prompt Engineering** | 5 prompts: generation, validation, simulation, scan, defense |
| **Normalize node types** | Map user label → standardized (web_server → server) |
| **Cross-stack references** | SQS, DynamoDB passed via CDK export/import |

---

### Challenges & Solutions

| Challenge | Solution |
|-----------|---------|
| **`ImportModuleError: No module named 'google'`** | Layer zip missing `python/` prefix — rebuild |
| **`_pydantic_core.cpython-313-aarch64...`** | Downloaded wrong Python 3.13, need `--python-version 3.12` |
| **`_cffi_backend` missing** | Wheel extraction missing `.so` — extract all |
| **CloudFront Access Denied** | Account not verified — fallback S3 |
| **API key exhausted free tier quota** | Wait for reset or upgrade to paid tier |

---

### Reflection

> "Through this project, I gained deeper understanding of Lambda native extension compatibility, the importance of matching Python versions and architectures when building layers, and how CDK simplifies AWS infrastructure management as code."

---

### Future Development

1. **CloudFront** — HTTPS, custom domain, WAF (needs AWS Support)
2. **Real-time WebSocket** — API Gateway WebSocket
3. **Multi-region** — Disaster recovery
4. **CI/CD Pipeline** — CodeCommit + CodeBuild + CodePipeline
5. **AWS WAF** — Rate limiting, SQL injection protection
6. **X-Ray Tracing** — Distributed tracing
