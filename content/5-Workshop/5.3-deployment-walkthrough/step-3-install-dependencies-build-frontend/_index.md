---
title : "Install Dependencies & Build Frontend"
date : "2025-10-10"
weight : 3
chapter : false
pre : " <b> Step 3 </b> "
---
# Step 3: Install Dependencies & Build Frontend

---

### Commands

```powershell
cd C:\<USER>\<PROJECT_DIR>
npm install
```

### Expected Output

```
up to date, audited 300+ packages in 5s
```

### Build Frontend

```powershell
npm run build
```

### Expected Output

```
dist/ generated successfully:
  index.html
  assets/index-xxxx.js
  assets/index-xxxx.css
```

### Verify

```powershell
Test-Path dist/index.html
# → True
```

📸 *[SCREENSHOT: Terminal showing successful build process]*
