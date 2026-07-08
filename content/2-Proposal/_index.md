---
title: "Proposal"
date: "2026-07-04"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# Cloud Nexus — Project Proposal

---

## 1. Project Overview

**Cloud Nexus** is a Threat Modeling Platform for cybersecurity professionals and infrastructure architects. The system allows users to design network topologies visually, then leverage AI (Google Gemini) to automatically detect vulnerabilities, simulate attack paths, and recommend defense measures.

| Component | Technology |
|-----------|------------|
| Frontend | React + Vite + ReactFlow + Tailwind CSS |
| Backend | FastAPI on AWS Lambda + API Gateway |
| AI | Google Gemini API (Gemini 2.0 Flash) |
| Infrastructure | AWS CDK (TypeScript), Python 3.12 ARM64 |
| AWS Services | S3, API Gateway, Lambda, Cognito, DynamoDB, SQS, SNS, Step Functions, Secrets Manager |

---

## 2. Objectives

### General Objective
Build a serverless platform on AWS that automates network security assessment — from topology design to vulnerability detection and attack simulation.

### Specific Objectives
- **Output:** REST API endpoints + Web Dashboard (React)
- **AI Integration:** Google Gemini generates topology, analyzes vulnerabilities, simulates attacks
- **Alert:** SNS notification when severe attack is detected
- **Serverless:** Entire backend on Lambda + API Gateway
- **Infra as Code:** AWS CDK — deploy / destroy with single command

### Success Criteria
1. Web dashboard loads from S3 static hosting
2. API Gateway returns `{"status":"ok"}` at `/api/health`
3. Lambda calls Google Gemini and returns valid topology JSON
4. Entire infrastructure deployed with `cdk deploy` and destroyed with `cdk destroy`

---

## 3. Problem Statement

| Problem | Solution |
|---------|----------|
| Manual network vulnerability detection is time-consuming | AI automatically scans topology |
| Hard to visualize attack paths | Visual simulation on ReactFlow |
| Complex test environment setup | Serverless on AWS, no server management |
| No defense assessment tool | Compare attack paths before/after adding defense |

### Target Audience
- Security Analysts
- Cloud Architects
- Cybersecurity Students

---

![Architecture Diagram](/images/1783482999271_7294040460361473390_g172388743919642419_7e7bc145b9dbf0b86747b4370039c64b.jpg)

---

## 4. Timeline (Jun 1 → Jul 4)

| Phase | Content | Duration |
|-------|---------|----------|
| **Kickoff** | Environment setup, IAM policy, AWS CLI | Jun 1 → Jun 4 |
| **Frontend** | Build UI with React + ReactFlow | Jun 5 → Jun 9 |
| **Backend** | FastAPI + AI service + Gemini integration | Jun 10 → Jun 14 |
| **Infrastructure** | AWS CDK stacks (Simulation, API, Frontend, Auth) | Jun 15 → Jun 19 |
| **Deployment** | Build Lambda Layer, deploy stacks | Jun 20 → Jun 23 |
| **Integration** | Connect frontend-backend, configure API key | Jun 24 → Jun 27 |
| **Testing** | Full system test, bug fixing | Jun 28 → Jun 30 |
| **Finalization** | Reports, documentation, cleanup | Jul 1 → Jul 4 |

---

## 5. Budget

### AWS Monthly Cost (Estimated)

| Service | Cost |
|---------|------|
| S3 Static Hosting | ~$0.01 |
| API Gateway | $0 (free tier) |
| Lambda | $0 (free tier) |
| Cognito | $0 (free tier) |
| DynamoDB | $0 (free tier) |
| SQS | $0 (free tier) |
| SNS | $0 (free tier) |
| Step Functions | $0 (free tier) |
| Secrets Manager | ~$0.40 |
| **Total** | **~$0.41/month** |

### Google Gemini API Cost
- Gemini 2.0 Flash: free tier with low rate limit
- Extra cost only when exceeding free tier

### Summary
The project is entirely within AWS Free Tier + Google Gemini Free Tier, with virtually no operational costs.

---

## 6. Risk Assessment

| Risk | Description | Severity | Mitigation |
|------|-------------|----------|------------|
| **API Key Leak** | Google API key committed to Git | High | Secrets Manager + .gitignore |
| **Unexpected Cost** | Lambda called excessively / attacked | Medium | CloudWatch Alarm, budget alert |
| **AI Response Error** | Gemini returns invalid JSON | Medium | Retry logic (2 times), fallback |
| **Lambda Timeout** | AI response too slow (>30s) | Low | Increase timeout, use async SQS |
| **CDK Deploy Error** | AWS CDK version mismatch | Low | Pin version, pre-deploy validation |
| **CORS** | Browser blocks cross-origin requests | Low | CORS middleware pre-configured |
| **Data Loss** | DynamoDB accidentally deleted | Medium | Backup, Point-in-Time Recovery |

---

*Cloud Nexus — Project Proposal Document*
