---
title: "WEEK 7 WORKLOG"
date: "2026-05-25"
weight: 1
chapter: false
pre: " <b> 1.7 </b> "
---

# **WEEK 7 WORKLOG**

### **Week 7 Objectives**

* Initialize the **Cloud Nexus** project — a Threat Modeling platform using React + Vite + Tailwind CSS.
* Set up the **FastAPI** (Python) backend integrated with **Google Gemini AI** for topology generation and attack simulation features.
* Define network node types (Server, Database, Firewall, IPS, IDS, Router, Cloud, IoT, Attacker, Workstation) for the React Flow canvas.
* Learn about Serverless architecture with AWS Lambda and API Gateway to support backend deployment.
* Use CloudFormation to automate infrastructure deployment for the project.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Mon) | Initialize Cloud Nexus project: install Vite + React 18 + Tailwind CSS + React Flow; create frontend directory structure. | 25/05/2026 | 25/05/2026 | https://github.com/thawngs18/DEMO.git |
| 2 (Tue) | Set up FastAPI backend: create main.py with endpoints /api/ai/generate, /api/topology/validate, /api/simulation/scan, /api/simulation/run. | 26/05/2026 | 26/05/2026 | |
| 3 (Wed) | Integrate Google Gemini AI: write ai_service.py with system prompts (GENERATION_PROMPT, VALIDATION_PROMPT, SIMULATION_PROMPT, SCAN_PROMPT); configure Gemini client. | 27/05/2026 | 27/05/2026 | |
| 4 (Thu) | Define node definitions: create 10 node types (Server, Database, Firewall, IPS, IDS, Router, Cloud, IoT, Workstation, Attacker) with Lucide React icons and corresponding colors. | 28/05/2026 | 28/05/2026 | |
| 5 (Fri) | Learn AWS Lambda + API Gateway for Serverless backend; write CloudFormation template to deploy Cloud Nexus infrastructure. | 29/05/2026 | 29/05/2026 | |

---

### **Week 7 Achievements**

* Successfully initialized the **Cloud Nexus** project with frontend (React 18 + Vite + Tailwind CSS + React Flow) and backend (FastAPI) structure.
* Set up **FastAPI** with API endpoints: generate topology, validate, scan, and run simulation — using CORS middleware to allow frontend localhost:5173 connections.
* Successfully integrated **Google Gemini AI** (gemini-2.0-flash) with specialized system prompts for each security task:
    * GENERATION_PROMPT: Generate network topology from text descriptions.
    * VALIDATION_PROMPT: Check architectural vulnerabilities based on Zero Trust.
    * SIMULATION_PROMPT: Simulate step-by-step attack paths.
    * SCAN_PROMPT: Analyze attack surface and recommend scenarios.
* Completed definition of **10 node types** for React Flow canvas with distinct icons and colors: Server (cyan), Database (cyan), Firewall (green), IPS (green), IDS (green), Router (cyan), Cloud (cyan), IoT (cyan), Workstation (cyan), Attacker (red).
* Learned about **AWS Lambda** and **API Gateway** for Serverless architecture, wrote CloudFormation templates to automate deployment.
