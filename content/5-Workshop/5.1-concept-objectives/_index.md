---
title : "Concept & Objectives"
date : "2025-10-10"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---
# 5.1. Concept & Objectives (1.0 pts)

---

### Context & Problem

**Cloud Nexus** is a Threat Modeling Platform for cybersecurity professionals and infrastructure architects. Users can design network topologies visually, then leverage AI (Google Gemini) to automatically detect vulnerabilities, simulate attack paths, and recommend defense measures.

**Target Customers:**
- Security Analysts
- Cloud Architects
- Cybersecurity Students

**Problems Solved:**
| Problem | Solution |
|---------|---------|
| Manual network vulnerability detection is time-consuming | AI automatically scans topology |
| Hard to visualize attack paths | Visual simulation on ReactFlow |
| Complex test environment setup | Serverless on AWS, no server management |
| No defense assessment tool | Compare attack paths before/after adding defense |

---

### Specific Objectives

| Criteria | Description |
|----------|------------|
| **Output** | REST API endpoints + Web Dashboard (React) |
| **AI Integration** | Google Gemini generates topology, analyzes vulnerabilities, simulates attacks |
| **Alert** | SNS notification when severe attack detected |
| **Serverless** | Entire backend on Lambda + API Gateway |
| **Infra as Code** | AWS CDK — deploy / destroy with single command |

**Success Criteria:**
1. Web dashboard loads from S3 static hosting
2. API Gateway returns `{"status":"ok"}` at `/api/health`
3. Lambda calls Google Gemini and returns valid topology JSON
4. Entire infrastructure deployed with `cdk deploy` and destroyed with `cdk destroy`

---

### Alignment with FCAJ / AWS

- **Serverless-first:** Lambda, API Gateway, DynamoDB, SQS, SNS, Step Functions
- **Infrastructure as Code:** AWS CDK (TypeScript)
- **Security:** IAM Role, Secrets Manager, Cognito, Principle of Least Privilege
- **Low cost:** Free tier for core services
