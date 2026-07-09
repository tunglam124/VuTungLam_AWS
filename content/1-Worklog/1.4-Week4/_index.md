---
title: "WEEK 4 WORKLOG"
date: "2026-05-11"
weight: 1
chapter: false
pre: " <b> 1.4 </b> "
---

# **WEEK 4 WORKLOG**

### **Week 4 Objectives**

* Conceptualize and design the architecture for an automated IAM Security Incident Response system on AWS following the Zero Trust model.
* Set up real-time security monitoring and alerting infrastructure (CloudTrail, SNS).
* Build automation workflows using event-driven architecture (EventBridge, AWS Lambda).
* Master incident response processes and apply the Least Privilege principle by optimizing configurations within Free Tier.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Mon) | **Sandbox & Monitoring Setup**: Create a secure IAM testing environment and configure AWS CloudTrail to log all Management events. | 11/05/2026 | 11/05/2026 | |
| 2 (Tue) | **Alert Pipeline Setup**: Configure Amazon SNS notification channel and handle cross-region architecture synchronization to us-east-1. | 12/05/2026 | 12/05/2026 | |
| 3 (Wed) | **Event Filter Construction**: Analyze logs and write Event Pattern JSON on Amazon EventBridge to catch privilege escalation behavior. | 13/05/2026 | 13/05/2026 | |
| 4 (Thu) | **Automation Source Code Development**: Write Python script for AWS Lambda to parse JSON, automatically revoke permissions, and send alerts. | 14/05/2026 | 14/05/2026 | |
| 5 (Fri) | **Integration & Testing**: Connect EventBridge to Lambda, conduct Live Test of unauthorized Admin privilege assignment, debug via CloudWatch. | 15/05/2026 | 15/05/2026 | |

---

### **Week 4 Achievements**

* Monday (Day 1):
    * Successfully initialized the workshop-test-user testing environment (IAM Sandbox).
    * Set up IAM Role IAM-Security-Lambda-Role in compliance with the least privilege principle.
    * Activated the CloudTrail monitoring system (IAM-Security-Trail), logging API traces to an S3 Bucket with SSE-S3 encryption to fully optimize costs.
* Tuesday (Day 2):
    * Deployed an emergency alert system via Amazon SNS Topic (Security-Alert-Topic).
    * Discovered and successfully resolved the system Region "phase mismatch" issue, synchronizing all resources (SNS, S3) to the N. Virginia region (us-east-1) to capture Global IAM events.
* Wednesday (Day 3):
    * Completed the event-driven security system architecture design.
    * Successfully set up EventBridge Rule with Custom JSON Pattern, filtering 100% accurately AttachUserPolicy commands related to AdministratorAccess.
* Thursday (Day 4):
    * Completed Python source code development using the Boto3 library on AWS Lambda.
    * Code successfully parsed violation data, identified the attacker, and executed the iam:DetachUserPolicy API successfully. Integrated automatic alert email sending.
* Friday (Day 5):
    * Completed full pipeline integration: CloudTrail -> EventBridge -> Lambda -> SNS.
    * Successfully performed Live Test simulating an incident: The system automatically detected and revoked unauthorized AdministratorAccess privileges in under 3 seconds.
    * Completely fixed the CloudWatch Log Group initialization error due to incorrect region configuration, ensuring a smooth operational monitoring flow.
