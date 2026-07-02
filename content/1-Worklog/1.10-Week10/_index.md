---
title: "WEEK 10 WORKLOG"
date: "2025-11-10"
weight: 10
chapter: false
pre: " <b> 1.10 </b> "
---

# **WEEK 10 WORKLOG**

### **Week 10 Objectives**

* Complete the **React Flow canvas** for Cloud Nexus with custom nodes and edges.
* Develop UI components: GlassPanel, HUD, FloatingCommandBar, Terminal, ScanningSpinner, ResultModal.
* Build the **useAI** hook connecting the frontend to backend API (generate, scan, simulate).
* Deploy the Cloud Nexus application to AWS (ECS Fargate or EC2).
* Learn about **Kubernetes** and **Minikube** for container orchestration.
* Set up **Velero** backup for the Kubernetes cluster.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Mon) | Develop React Flow canvas: create CustomNode (10 node types with icon + color) and CustomEdge (smoothstep + animated); implement smartHandles and edgeRouting utilities. | 10/11/2025 | 10/11/2025 | |
| 2 (Tue) | Build UI components: GlassPanel (frosted glass effect), TopHUD (top status bar), FloatingCommandBar (terminal-style command bar), HackerOverlay, ResultModal. | 11/11/2025 | 11/11/2025 | |
| 3 (Wed) | Develop useAI hook: connect frontend to backend API (generate, scan, simulate); handle async/await, error handling, real-time logging to terminal; implement useStore (Zustand) for global state management. | 12/11/2025 | 12/11/2025 | |
| 4 (Thu) | Deploy Cloud Nexus to AWS: configure ECS Fargate cluster for frontend & backend containers; set up Application Load Balancer and Auto Scaling. | 13/11/2025 | 13/11/2025 | |
| 5 (Fri) | Learn Kubernetes: install Minikube, write deployment.yaml for Cloud Nexus, deploy the application; set up Velero backup for cluster resources. | 14/11/2025 | 14/11/2025 | |

---

### **Week 10 Achievements**

* Completed the **React Flow canvas** with drag-and-drop support for 10 node types, custom smoothstep edges with animated indicators, and smartHandles algorithm for optimal connection point selection.
* Built a complete set of **UI components** with a hacker/cyber aesthetic:
    * **GlassPanel**: Frosted glass background component for all panels (Scenarios, Edit, AttackPath).
    * **TopHUD**: Status bar displaying mode (view/edit), node count, edge count.
    * **FloatingCommandBar**: Terminal-style command bar supporting "generate", "scan", "simulate", "help", "clear" commands.
    * **HackerOverlay**: Matrix-style overlay for attack simulation visualization.
    * **ResultModal**: Modal for displaying AI results (topology generated, scan complete, simulation result).
    * **ScanningSpinner**: Animation spinner during scan/simulate operations.
* Developed **useAI hook** connecting frontend to 4 API endpoints:
    * Calls /api/ai/generate to generate topology from text prompts.
    * Calls /api/simulation/scan to scan for vulnerabilities.
    * Calls /api/simulation/run to run attack simulations.
    * Handles async/await, error handling, real-time logging to TerminalLine component.
* Used **Zustand** (useStore) for global state management: nodes, edges, scenarios, logs, mode, scanning/simulating status.
* Deployed Cloud Nexus to **AWS ECS Fargate**:
    * Created ECS cluster with Fargate launch type for frontend (port 5173) and backend (port 8000).
    * Set up Application Load Balancer for traffic routing.
    * Configured Auto Scaling based on CPU utilization.
* Learned **Kubernetes**: installed Minikube, created deployment.yaml for Cloud Nexus, successfully deployed using `kubectl apply`. Understood Pod, Node, and Cluster concepts.
* Set up **Velero**: installed via Helm, practiced backup (`velero backup create`) and restore (`velero restore create`) for cluster resources.
