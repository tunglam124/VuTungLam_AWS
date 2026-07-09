---
title: "WEEK 12 WORKLOG"
date: "2026-07-06"
weight: 12
chapter: false
pre: " <b> 1.12 </b> "
---

# **WEEK 12 WORKLOG**

### **Week 12 Objectives**

* Deploy **frontend** to AWS via S3 static hosting and CloudFront CDN.
* Complete **frontend-backend integration** and ensure CORS works end-to-end.
* Integrate **AI services** and test the full application workflow.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Tue) | - Build `CloudNexus-Secrets` stack and create Secrets Manager to store GOOGLE_API_KEY<br>- Build `CloudNexus-Backend` stack with Lambda (FastAPI via Mangum), API Gateway HTTP API and IAM roles<br>- Configure Lambda Layer with Python dependencies: fastapi, mangum, google-genai<br>- First deploy of both stacks to AWS<br>- Initialize frontend structure with Vite + React + ReactFlow + Zustand + TailwindCSS<br>- Configure build script to deploy frontend to S3 bucket<br>- Deploy S3 bucket and set up CloudFront distribution for frontend | 06/07/2026 | 06/07/2026 | |
| 2 (Wed) | - Fix CORS preflight OPTIONS error from CloudFront to API Gateway returning 400 Bad Request<br>- Remove CORS config from API Gateway to avoid double-handling with FastAPI CORSMiddleware<br>- Add `@app.options` handler in FastAPI for preflight requests<br>- Update `allow_origins` in CORSMiddleware to include CloudFront URL and localhost<br>- Add new Lambda Layer with full dependencies<br>- Rebuild and redeploy Lambda function | 07/07/2026 | 07/07/2026 | |
| 3 (Thu) | - Configure `VITE_API_URL` in `.env.production` pointing to production API Gateway endpoint<br>- Set up build configuration for Vite in production mode<br>- Redeploy built frontend bundle to S3 and invalidate CloudFront cache<br>- Test frontend connection from CloudFront to backend API | 08/07/2026 | 08/07/2026 | |
| 4 (Fri) | - Complete FastAPI backend with `GET /` returning API metadata<br>- Verify all endpoints: `/api/health`, `/api/ai/generate`, `/api/topology/validate`, `/api/simulation/scan`<br>- Check CORS headers on all endpoints from CloudFront origin<br>- End-to-end test of AI generate topology flow from frontend | 09/07/2026 | 09/07/2026 | |
| 5 (Sat) | - Integrate and test the full workflow: AI generate topology, topology validation, simulation scan, simulation run, simulation with defense<br>- Perform real-world testing from CloudFront frontend to ensure all features are stable<br>- Fix `/api/simulation/with-defense` endpoint to return full `attack_steps` and `defense_mechanisms`<br>- Optimize Lambda function names and CloudFormation outputs | 10/07/2026 | 10/07/2026 | |

---

### **Week 12 Achievements**

* **Backend** deployed completely on AWS Lambda with FastAPI, running through the Mangum adapter.
* **API Gateway HTTP API** operational, exposing all endpoints for frontend access via CloudFront.
* **Secrets Manager** securely stores `GOOGLE_API_KEY`; Lambda reads it via IAM grant.
* **Frontend** deployed to S3 and served through **CloudFront CDN**.
* **CORS** correctly handled via FastAPI `CORSMiddleware`, allowing requests from the CloudFront origin.
* **Lambda Layer** containing `fastapi`, `mangum`, `google-genai` ensures Lambda has all dependencies.
* Full **end-to-end flow** operational from frontend to backend: AI generate topology, topology validation, simulation scan, simulation run, simulation with defense.
* **Infrastructure** managed entirely via **AWS CDK** and can be redeployed at any time.
