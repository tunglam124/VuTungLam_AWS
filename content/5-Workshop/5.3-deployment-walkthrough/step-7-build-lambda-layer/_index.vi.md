---
title : "Build Lambda Layer"
date : "2025-10-10"
weight : 7
chapter : false
pre : " <b> Step 7 </b> "
---
# Step 7: Build Lambda Layer

---

Chứa Python dependencies (google-genai, FastAPI, pydantic, v.v.) cho Lambda.

---

### 7.1 Download wheels cho Python 3.12 ARM64

```powershell
$wheelDir = "C:\<USER>\AppData\Local\Temp\<TEMP_DIR>\wheels"
New-Item -ItemType Directory -Path $wheelDir -Force | Out-Null

pip download -r cdk/lambdas/api/requirements.txt --dest $wheelDir `
  --platform manylinux2014_aarch64 --python-version 3.12 --only-binary :all:
```

| Package | Version | Ghi chú |
|---------|---------|---------|
| fastapi | 0.139.0 | Pure Python |
| mangum | 0.21.0 | Pure Python |
| pydantic | 2.13.4 | Pure Python |
| pydantic-core | 2.46.4 | **Native** (.so) |
| google-genai | 2.10.0 | Pure Python |
| cffi | 2.0.0 | **Native** (.so) |
| cryptography | 49.0.0 | **Native** (.so) |
| websockets | 16.0 | **Native** (.so) |

> **⚠️ Quan trọng:** File `.so` phải đúng **Python 3.12** (`cp312`) và **ARM64** (`aarch64`).

---

### 7.2 Giải nén & đóng gói Layer

*(See English version for full PowerShell script)*

**Kiểm tra .so files:**
```powershell
$zip = [System.IO.Compression.ZipFile]::OpenRead($zipPath)
$zip.Entries | Where-Object { $_.FullName -like "*.so*" } | Format-Table FullName, Length
$zip.Dispose()
```

Expected:
```
python/pydantic_core/_pydantic_core.cpython-312-aarch64-linux-gnu.so
python/_cffi_backend.cpython-312-aarch64-linux-gnu.so
python/websockets/speedups.cpython-312-aarch64-linux-gnu.so
...
```

---

### 7.3 Publish Layer lên AWS

```powershell
aws lambda publish-layer-version --layer-name CloudNexus-PythonDeps `
  --description "Python3.12 ARM64 deps" --zip-file "fileb://$zipPath" `
  --compatible-runtimes python3.12 --compatible-architectures arm64 `
  --query "LayerVersionArn" --output text
```

**Expected:**
```
arn:aws:lambda:ap-southeast-1:<ACCOUNT_ID>:layer:CloudNexus-PythonDeps:1
```

📸 *[CHÈN ẢNH: Publish layer thành công]*
