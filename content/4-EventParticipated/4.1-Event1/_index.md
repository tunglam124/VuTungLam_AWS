---
title: "FCAJ Community Day – Conference Call"
date: "2026-05-23"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Summary Report: FCAJ Community Day – Conference Call

## Event Objectives

- **Infrastructure & Cost:** Transition CloudFront billing to flat-rate pricing and optimize network performance
- **AI Product Development:** The 36-hour journey of building an intelligent UI generation tool (UTMorpho)
- **AI Reliability:** Understanding LLM non-determinism and error mitigation strategies
- **Context Engineering:** Why input data quality matters more than quantity
- **Multi-Agent Automation:** Applying multi-agent systems for complex data processing and credit scoring

---

## Agenda Overview

| | |
|---|---|
| **Time** | 9:00 AM – 12:00 PM, Saturday, May 23, 2026 |
| **Location** | AWS Vietnam Office |

---

## Key Highlights

### 1. Welcome & Introduction (8:30 – 9:00 AM)

- Check-in and networking
- Workshop objectives and agenda overview

### 2. Context Is Everything: Making AI Actually Work for You (9:00 – 09:30 AM)

#### What Is Context?

Context is not just supplementary information — it is "the information that helps AI understand the task behind the task." Four core elements:

| Element | Description |
|---|---|
| **Goal** | The actual outcome you want to achieve |
| **Situation** | Who you are, deadlines, constraints |
| **Constraints** | Tech stack, style, budget, format |
| **Evidence** | Source code, documents, examples, requirements |

#### Why AI Fails Without Context

- AI cannot read your mind — you must state the goal clearly
- Generic or off-target responses stem from poor input
- Verbose or constraint-violating output due to missing boundaries

#### Three Common Mistakes

1. **"The Internet Puller"** — Dumping entire articles, PDFs, or screenshots into a chat. Result: AI gets distracted, accuracy drops, token costs rise
2. **Stating the Obvious** — Telling AI what it already knows. Instead, focus on what matters next
3. **Missing Goals & Constraints** — Vague prompts like "Build me a website" yield vague answers

#### The Evolution of Context Systems

| Stage | Description |
|---|---|
| **Prompt** | Single question, no state |
| **Context** | Augmented with supporting documents |
| **Memory** | Personalization over time ("second AI brain") |

#### Framework for Good Context

1. Define the goal: What should AI help you achieve?
2. Filter relevant information: Provide only what is necessary
3. Set constraints: Technology, time, style
4. Define success criteria: What does a good answer look like?

> Context is not supplementary — context is the product experience. Context Engineering is becoming a core skill for the future.

---

### 3. Broadening the Cloud Horizon (09:30 AM – 12:00 PM)

#### Business Process Automation with Amazon Quick Suite

- **Agentic AI Solution:** Amazon Quick Suite simplifies the path from data to action
- **Data Ecosystem:** Connects 40+ data sources, databases, data warehouses, combined with Bedrock models and web search
- **Automation:** Auto-generates meeting minutes (MoM), sends emails, schedules follow-ups

#### Amazon CloudFront: From Edge to Origin

- **Flat-rate pricing** (launched Nov 2025) — predictable monthly costs, no bill shock from traffic spikes or DDoS
- **Cost optimization:** Free data transfer from AWS origin services to CloudFront; reduces EC2 CPU load
- **Security & Performance:**
  - 700+ global PoPs for low latency
  - TLS 1.3, mTLS, Edge DDoS protection
  - HTTP/3 (QUIC) for faster parallel resource loading

#### UTMorpho: Building a Product at LotusHacks

A 36-hour journey building an AI-powered UI generation tool with direct canvas editing:

- **Idea:** Solve the frustration of static AI-generated UI mockups. Every re-prompt changes the entire design
- **Key features:** Direct WYSIWYG canvas editing, preserve unrelated components, optimize token consumption
- **Lesson:** Real frustration creates real ideas — team chemistry matters more than individual skill

#### Why temperature = 0 Is Still Not Deterministic

- **Technical cause:** Floating-point operations on GPUs are non-associative; parallel execution order is non-deterministic
- **Business cause:** API provider inference batching changes per-request computation
- **Mitigation:** Majority voting, structured output (JSON mode), design for variance

#### Multi-Agent Credit Scoring for Startups

A VPBank case study on using multiple AI Agents to evaluate startup loan applications:

- **Challenge:** Traditional banking systems fail with startup data (no 3-year financial history, no conventional collateral)
- **Multi-Agent Model:** Financial Analyst, Market Analyst, Team Evaluator, Risk Assessor — cross-examining for consensus
- **ROI:**
  - Processing time: 2-3 weeks → 2-4 hours
  - 95% cost reduction per credit decision
  - Double the approval rate through multi-dimensional assessment

---

### 4. Networking & Lucky Draw

- 10 lucky draw rounds for VIP guests on the 36th floor
- Networking with students and AWS engineers
- Discussions on Cloud certification paths, Serverless and GenAI projects

---

## Key Takeaways

### AI Implementation
Context is the key differentiator that turns a generic language model into a reliable enterprise AI assistant.

### Career Orientation
The tech industry is shifting — big opportunities for versatile professionals who can code, integrate AI, and manage data workflows.

### Community & Networking
Engaging with AWS ecosystem experts bridges the gap between academic theory and real-world infrastructure architecture.

---

## Event Photos

{{< figure src="/images/bfb2481eacf02dae74e1.jpg" title="FCAJ Community Day" alt="Event photo" >}}

---

> The FCAJ Community Day provided practical insights into enterprise AI applications — from Context Engineering and CloudFront optimization to Multi-Agent credit scoring and 36-hour AI product development. It served as a valuable bridge between academic theory and real-world deployment.
