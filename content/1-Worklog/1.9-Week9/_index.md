---
title: "WEEK 9 WORKLOG"
date: "2026-06-08"
weight: 1
chapter: false
pre: " <b> 1.9 </b> "
---

# **WEEK 9 WORKLOG**

### **Week 9 Objectives**

* Complete the **AI Simulation Engine** for Cloud Nexus: develop in-depth system prompts for Gemini AI.
* Develop attack simulation API endpoints: scan topology, run simulation, run-with-defense.
* Implement node/edge normalization logic from AI responses and network device type mapping.
* Integrate **Prometheus** and **Grafana** to monitor FastAPI backend performance.
* Learn advanced **AWS CodeDeploy** and debug deployment scripts.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Mon) | Develop AI Simulation Engine: write SIMULATION_PROMPT with detailed attack path tracing, Zero Trust logic, realistic attack technique descriptions (nmap, CVE exploit, brute-force). | 08/06/2026 | 08/06/2026 | |
| 2 (Tue) | Build /api/simulation/run and /api/simulation/run-with-defense endpoints; implement SimulationRequest/SimulationResponse models; develop normalize_node for flat/nested JSON from AI. | 09/06/2026 | 09/06/2026 | |
| 3 (Wed) | Develop SCAN_PROMPT and VALIDATION_PROMPT: attack surface analysis, Zero Trust vulnerability checking, attack scenario generation (SQL Injection, Lateral Movement, DDoS IoT Botnet). | 10/06/2026 | 10/06/2026 | |
| 4 (Thu) | Debug and optimize AI service: handle JSON parse errors, implement retry logic for truncated responses, type_mapping for network devices (internet→cloud, pc→workstation, db→database). | 11/06/2026 | 11/06/2026 | |
| 5 (Fri) | Set up Prometheus + Grafana for monitoring: configure metrics endpoint for FastAPI, create dashboards for CPU, memory, request latency; research cAdvisor for container metrics. | 12/06/2026 | 12/06/2026 | |

---

### **Week 9 Achievements**

* Completed the **AI Simulation Engine** with in-depth system prompts:
    * SIMULATION_PROMPT: Guides Gemini to simulate ethical hacking attacks step-by-step with real techniques (nmap -sV scan, CVE exploit, SSH brute-force, data exfiltration via DNS tunneling).
    * SIMULATION_WITH_DEFENSE_PROMPT: Re-runs simulation with defenses, identifies blocking point at the first effective security node.
    * SCAN_PROMPT: Analyzes attack surface and generates scenarios (SQL Injection, Lateral Movement, DDoS IoT Botnet).
* Built complete **API endpoints**:
    * POST /api/simulation/scan — scan topology for vulnerabilities.
    * POST /api/simulation/run — run attack simulation.
    * POST /api/simulation/run-with-defense — re-run with defense measures applied.
* Implemented **normalize_node** function handling 2 JSON formats (flat and nested) from AI responses, along with **type_mapping** to map common device names (internet→cloud, pc→workstation, db→database, fw→firewall).
* Successfully debugged issues: JSON parse errors from truncated responses (implemented retry logic), handled missing id/position in node data.
* Set up **monitoring** system with **Prometheus** (metrics collection) and **Grafana** (dashboard visualization):
    * Configured metrics endpoint for FastAPI backend.
    * Created dashboards for CPU usage, memory usage, request latency, error rates.
    * Researched cAdvisor for Docker container monitoring.
