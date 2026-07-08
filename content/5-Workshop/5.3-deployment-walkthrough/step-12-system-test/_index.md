---
title : "System Test & Validation"
date : "2025-10-10"
weight : 12
chapter : false
pre : " <b> Step 12 </b> "
---
# Step 12: System Test & Validation

---

### Health Check

```powershell
curl -s "https://<API_ID>.execute-api.ap-southeast-1.amazonaws.com/prod/api/health"
```

**Expected:**
```json
{"status":"ok"}
```

📸 *[SCREENSHOT: curl health check response]*

**Error Testing:**
```powershell
curl -s -X PUT "https://<API_ID>.execute-api.ap-southeast-1.amazonaws.com/prod/api/health"   # 405
curl -s "https://<API_ID>.execute-api.ap-southeast-1.amazonaws.com/prod/api/nonexistent"    # 404
```

---

### Frontend Test

Open URL in browser:
```
http://cloudnexusfrontendstack-<SUFFIX>.s3-website-ap-southeast-1.amazonaws.com
```

**Verify:** React fully loads, ReactFlow canvas displays, dark mode works.

📸 *[SCREENSHOT: Web interface in browser]*

---

### Generate Topology (AI)

```powershell
$body = '{"prompt":"simple web server with database"}'
[System.Text.Encoding]::UTF8.GetBytes($body) | Set-Content "$env:TEMP\req.json" -Encoding Byte -Force
curl -s -X POST "https://<API_ID>.execute-api.ap-southeast-1.amazonaws.com/prod/api/ai/generate" -H "Content-Type: application/json" --data-binary "@$env:TEMP\req.json"
```

**With quota:** Returns JSON topology (nodes + edges)
**Quota exhausted:** `500` → CloudWatch log: `ClientError: 429 RESOURCE_EXHAUSTED`

---

### Validate Topology

```powershell
$body = '{"nodes":[{"id":"db","data":{"label":"DB","type":"database"}}],"edges":[]}'
curl -s -X POST "https://<API_ID>.execute-api.ap-southeast-1.amazonaws.com/prod/api/topology/validate" -H "Content-Type: application/json" -d $body
```

---

### Run Simulation

```powershell
$body = '{"topology":{"nodes":[{"id":"attacker","data":{"label":"Hacker","type":"attacker"}},{"id":"server","data":{"label":"Web","type":"server"}}],"edges":[{"source":"attacker","target":"server"}]},"scenario_name":"SQL Injection","target_node_id":"server","scenario_description":"Attacker tries SQL injection"}'
[System.Text.Encoding]::UTF8.GetBytes($body) | Set-Content "$env:TEMP\sim.json" -Encoding Byte -Force
curl -s -X POST "https://<API_ID>.execute-api.ap-southeast-1.amazonaws.com/prod/api/simulation/run" -H "Content-Type: application/json" --data-binary "@$env:TEMP\sim.json"
```

---

### CloudWatch Logs

```powershell
aws logs describe-log-groups --log-group-name-prefix "/aws/lambda/CloudNexus"

$stream = aws logs describe-log-streams --log-group-name "/aws/lambda/CloudNexus-APIHandler" --order-by LastEventTime --descending --limit 1 --query "logStreams[0].logStreamName" --output text

aws logs get-log-events --log-group-name "/aws/lambda/CloudNexus-APIHandler" --log-stream-name "$stream" --limit 20 --query "events[].message" --output text
```

**Expected:**
```
INIT_START Runtime Version: python:3.12.mainlinev2.v11
START RequestId: xxx
END RequestId: xxx
REPORT RequestId: xxx  Duration: 61.09 ms  Billed Duration: 4048 ms  Memory Size: 512 MB  Max Memory Used: 193 MB  Init Duration: 3986.50 ms
```

| Metric | Value | Meaning |
|--------|-------|---------|
| Init Duration | ~4000ms | Cold start |
| Duration | ~60ms | Request processing |
| Memory Size | 512 MB | Allocated memory |
| Max Memory Used | ~193 MB | Actual memory used |
