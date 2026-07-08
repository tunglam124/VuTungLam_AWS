---
title : "Build Lambda Layer"
date : "2025-10-10"
weight : 7
chapter : false
pre : " <b> Step 7 </b> "
---
# Step 7: Build Lambda Layer

---

Contains Python dependencies (google-genai, FastAPI, pydantic, etc.) for Lambda.

---

### 7.1 Download wheels for Python 3.12 ARM64

```powershell
$wheelDir = "C:\<USER>\AppData\Local\Temp\<TEMP_DIR>\wheels"
New-Item -ItemType Directory -Path $wheelDir -Force | Out-Null

pip download -r cdk/lambdas/api/requirements.txt --dest $wheelDir `
  --platform manylinux2014_aarch64 --python-version 3.12 --only-binary :all:
```

| Package | Version | Notes |
|---------|---------|-------|
| fastapi | 0.139.0 | Pure Python |
| mangum | 0.21.0 | Pure Python |
| pydantic | 2.13.4 | Pure Python |
| pydantic-core | 2.46.4 | **Native** (.so) |
| google-genai | 2.10.0 | Pure Python |
| cffi | 2.0.0 | **Native** (.so) |
| cryptography | 49.0.0 | **Native** (.so) |
| websockets | 16.0 | **Native** (.so) |

> **⚠️ Important:** `.so` files must match **Python 3.12** (`cp312`) and **ARM64** (`aarch64`).

---

### 7.2 Extract and package Layer

```powershell
$baseDir = "C:\<USER>\AppData\Local\Temp\<TEMP_DIR>"
$extractDir = Join-Path $baseDir "python_tmp"
Remove-Item -Recurse -Force $extractDir -ErrorAction SilentlyContinue
New-Item -ItemType Directory -Path $extractDir -Force | Out-Null

Add-Type -Assembly "System.IO.Compression.FileSystem"
$wheels = Get-ChildItem "$wheelDir\*.whl"
foreach ($w in $wheels) {
    $zip = [System.IO.Compression.ZipFile]::OpenRead($w.FullName)
    foreach ($entry in $zip.Entries) {
        $name = $entry.FullName
        if ($name -match "\.dist-info/") { continue }
        if ($name.EndsWith("/")) { continue }
        if ($name -match "\.data/") { continue }
        $targetPath = Join-Path $extractDir $name
        $targetDir = Split-Path $targetPath -Parent
        if (!(Test-Path $targetDir)) { New-Item -ItemType Directory -Path $targetDir -Force | Out-Null }
        [System.IO.Compression.ZipFileExtensions]::ExtractToFile($entry, $targetPath, $true)
    }
    $zip.Dispose()
}

$layerDir = Join-Path $baseDir "_layer"
Remove-Item -Recurse -Force $layerDir -ErrorAction SilentlyContinue
New-Item -ItemType Directory -Path $layerDir -Force | Out-Null
Copy-Item -Recurse -Force $extractDir (Join-Path $layerDir "python")

$zipPath = Join-Path $baseDir "layer.zip"
Remove-Item $zipPath -Force -ErrorAction SilentlyContinue
Compress-Archive -Path "$layerDir\*" -DestinationPath $zipPath -Force
```

**Verify .so files:**
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

### 7.3 Publish Layer to AWS

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

📸 *[SCREENSHOT: Publish layer success]*
