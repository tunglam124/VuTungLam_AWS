---
title: "WEEK 11 WORKLOG"
date: "2026-06-22"
weight: 11
chapter: false
pre: " <b> 1.11 </b> "
---

# **WEEK 11 WORKLOG**

### **Week 11 Objectives**

* Build the **serverless infrastructure** for Cloud Nexus using **AWS CDK (TypeScript)**.
* Develop **CDK stacks**: Simulation Stack (SQS, DynamoDB, S3, Step Functions, SNS) and Auth Stack (Cognito).
* Create **Lambda functions** in Python 3.12 ARM64 with FastAPI via Mangum adapter.
* Configure **API Gateway HTTP API** and IAM roles for Lambda execution.
* Set up **Secrets Manager** for secure Google API key storage.
* Establish **CI/CD pipeline** with CDK synth, deploy, and destroy commands.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Mon) | Set up CDK project with TypeScript: initialize cdk app, configure TypeScript config, define CloudNexusStack; research Python 3.12 ARM64 Lambda compatibility. | 22/06/2026 | 22/06/2026 | |
| 2 (Tue) | Build **Simulation Stack**: create SQS queue (buffered scan requests), DynamoDB table (topology + results), S3 bucket (artifacts), Step Functions state machine (orchestrator), SNS topic (alerts). | 23/06/2026 | 23/06/2026 | |
| 3 (Wed) | Build **Auth Stack** with Cognito User Pool; build **Secrets Stack**: create Secrets Manager secret for GOOGLE_API_KEY; research Lambda Layer structure for Python dependencies. | 24/06/2026 | 24/06/2026 | |
| 4 (Thu) | Create **Lambda Layer** for Python 3.12 ARM64: package fastapi, mangum, google-genai, pydantic into proper layer structure; develop Lambda function with FastAPI app + Mangum handler. | 25/06/2026 | 25/06/2026 | |
| 5 (Fri) | Assemble **API Stack**: configure API Gateway HTTP API, IAM roles, Cognito authorizer; integrate all outputs (bucket names, queue URLs, table ARNs) via CDK context; run `cdk synth` and `cdk deploy` for the first time. | 26/06/2026 | 26/06/2026 | |

---

### **Week 11 Achievements**

* Successfully initialized **AWS CDK (TypeScript)** project with `cdk init app --language typescript`, configured `tsconfig.json` and `cdk.json` for the Cloud Nexus project.
* Built **Simulation Stack** (`CloudNexusSimulationStack`) containing:
  * **SQS** standard queue as buffer for simulation requests.
  * **DynamoDB** table with partition key `PK` (topology/results storage).
  * **S3** bucket for generated topology JSON artifacts.
  * **Step Functions** state machine orchestrating multi-step simulations.
  * **SNS** topic for security alert notifications.
* Built **Secrets Stack** using `aws-cdk-lib/aws-secretsmanager` to create `GOOGLE_API_KEY` secret with auto-generated rotation.
* Built **Cognito Auth Stack**: User Pool with email/password sign-in, App Client for frontend integration.
* Developed **Python 3.12 ARM64 Lambda Layer**: created `/python/lib/python3.12/site-packages/` structure containing `fastapi==0.115.0`, `mangum==0.17.0`, `google-genai==1.0.0`, `pydantic==2.9.0`. Configured Lambda function with `architecture: Architecture.ARM_64` and `runtime: Runtime.PYTHON_3_12`.
* Implemented **FastAPI application** with Mangum handler: defined routes (`/api/health`, `/api/ai/generate`, `/api/topology/validate`, `/api/simulation/scan`, `/api/simulation/run`, `/api/simulation/run-with-defense`), integrated CORS middleware.
* Built **API Stack** (`CloudNexusApiStack`) with:
  * **API Gateway HTTP API** with Lambda integration.
  * **Cognito User Pool Authorizer** for protected endpoints.
  * **IAM roles** granting Lambda read access to Secrets Manager and full access to SQS, DynamoDB, SNS, Step Functions.
* Successfully ran `cdk synth` (CloudFormation template generation) and `cdk deploy --all` to deploy all stacks to AWS.
* Verified all stack outputs (API Gateway URL, S3 bucket name, SQS queue URL, DynamoDB table name, Cognito User Pool ID) for frontend configuration.
