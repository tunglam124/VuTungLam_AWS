---
title : "Get Source Code"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> Step 2 </b> "
---
# Step 2: Get Source Code

---

### Commands

```powershell
cd C:\<USER>\<PROJECT_DIR>
Get-ChildItem -Directory
```

### Project Structure

```
DEMO/
├── cdk/                    # AWS CDK infrastructure code
│   ├── bin/app.ts          # Entry point
│   ├── lib/                # Stack definitions
│   │   ├── config.ts
│   │   ├── simulation-stack.ts
│   │   ├── auth-api-stack.ts
│   │   └── frontend-stack.ts
│   ├── lambdas/api/        # Lambda source code
│   │   ├── main.py
│   │   ├── ai_service.py
│   │   └── requirements.txt
│   ├── lambdas/simulation/
│   ├── lambdas/notification/
│   ├── package.json
│   └── tsconfig.json
├── src/                    # React frontend source
├── public/
├── dist/                   # Frontend build output
├── package.json
└── baocao/                 # Report files
```

📸 *[SCREENSHOT: Project directory structure in terminal]*
