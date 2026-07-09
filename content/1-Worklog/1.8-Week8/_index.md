---
title: "WEEK 8 WORKLOG"
date: "2026-06-08"
weight: 1
chapter: false
pre: " <b> 1.8 </b> "
---

# **WEEK 8 WORKLOG**

### **Week 8 Objectives**

* Build a complete CI/CD pipeline for the **Cloud Nexus** project using **AWS CodePipeline**, **CodeBuild**, and **CodeDeploy**.
* Dockerize the React frontend and FastAPI backend for consistent deployment.
* Use **Terraform** to manage the CI/CD infrastructure as Infrastructure as Code (IaC).
* Integrate automated testing steps into the pipeline.
* Learn about AWS CodeCommit as the source repository for the pipeline.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Mon) | Write Dockerfiles for frontend (React + Vite) and backend (FastAPI + Uvicorn); create docker-compose.yml for multi-container orchestration. | 08/06/2026 | 08/06/2026 | |
| 2 (Tue) | Set up AWS CodeCommit repository for Cloud Nexus source code; configure IAM roles for the pipeline. | 09/06/2026 | 09/06/2026 | |
| 3 (Wed) | Build CI pipeline with AWS CodeBuild: automate Docker image builds, run unit tests for FastAPI backend. | 10/06/2026 | 10/06/2026 | |
| 4 (Thu) | Set up CD pipeline with AWS CodeDeploy: deploy Docker containers to EC2; configure AppSpec and scripts. | 11/06/2026 | 11/06/2026 | |
| 5 (Fri) | Use Terraform to define the entire CI/CD infrastructure (VPC, ECR repositories, CodePipeline, CodeBuild projects, CodeDeploy groups). | 12/06/2026 | 12/06/2026 | |

---

### **Week 8 Achievements**

* Successfully wrote **Dockerfiles** for frontend (multi-stage React + Vite) and backend (FastAPI + Uvicorn), along with **docker-compose.yml** for multi-container orchestration.
* Set up **AWS CodeCommit** repository and configured IAM roles with Least Privilege permissions for the pipeline.
* Built **CI pipeline** with AWS CodeBuild:
    * Build Docker images for both frontend and backend.
    * Run unit tests for FastAPI backend (Pydantic model validation).
    * Push images to Amazon ECR.
* Set up **CD pipeline** with AWS CodeDeploy:
    * Deploy Docker containers to EC2 instances.
    * Configure AppSpec.yml with hooks (BeforeInstall, ApplicationStart, ValidateService).
    * Write deployment scripts to pull images from ECR and start containers.
* Used **Terraform** (HCL) to define the entire CI/CD infrastructure:
    * Leveraged variables and .tfvars files for flexible configuration management.
    * Created VPC, subnets, ECR repositories, CodePipeline, CodeBuild projects, CodeDeploy application and deployment groups.
    * Successfully ran `terraform init`, `plan`, and `apply` to deploy infrastructure.
* Gained a solid understanding of the **CI/CD** workflow and applied it to the real-world Cloud Nexus project.
