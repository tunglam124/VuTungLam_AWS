---
title : "Cài dependencies & Build Frontend"
date : "2025-10-10"
weight : 3
chapter : false
pre : " <b> Step 3 </b> "
---
# Step 3: Cài Dependencies & Build Frontend

---

### Thao tác

```powershell
cd C:\<USER>\<PROJECT_DIR>
npm install
```

### Expected output

```
up to date, audited 300+ packages in 5s
```

### Build frontend

```powershell
npm run build
```

### Expected output

```
dist/ generated successfully:
  index.html
  assets/index-xxxx.js
  assets/index-xxxx.css
```

### Kiểm tra

```powershell
Test-Path dist/index.html
# → True
```

📸 *[CHÈN ẢNH: Terminal hiển thị quá trình build thành công]*
