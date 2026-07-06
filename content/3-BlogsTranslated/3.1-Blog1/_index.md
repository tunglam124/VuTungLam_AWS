---
title: "Blog 1"
date: "2026-06-09"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Well-Architected Best Practices for Software Supply Chain Security

<span class="meta-info">by Trevor Schiavone and Desiree Brunner | on 26 MAY 2026 | in</span> [Security, Identity, & Compliance](https://aws.amazon.com/blogs/security/category/security-identity-compliance/), [Best Practices](https://aws.amazon.com/blogs/security/category/post-types/best-practices/) | [Permalink](https://aws.amazon.com/blogs/security/well-architected-best-practices-for-software-supply-chain-security/)

Recent supply chain attacks — Shai-Hulud, Chalk/Debug, tea.xyz token farming, and axios — have demonstrated a sobering reality: a single compromised maintainer account can propagate malicious packages across thousands of consumer environments simultaneously. These attacks exploit two fronts — compromised maintainer credentials that publish malicious packages, and consumer environments that download and execute them.

This post explores best practices for **package consumers**, aligned with the [AWS Well-Architected Framework — Security Pillar](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html).

---

## 1. Use Temporary Credentials & Grant Least Privilege

The Shai-Hulud worm scanned developer environments and CI/CD pipelines for secrets — npm tokens, GitHub tokens, IAM access keys. Long-lived credentials exposed this way enable threat actors to propagate malware and access cloud resources.

**Key practices:**

- **Use temporary credentials** — `aws login` for local development, IAM Identity Center for short-lived CLI credentials, OIDC federation (GitHub Actions, GitLab CI) for CI/CD pipelines. Temporary credentials expire automatically, limiting the window of exposure. [SEC02-BP02](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_identities_unique.html)
- **Grant least privilege** — assign minimum permissions; use temporary elevated permissions when higher privilege is needed. [SEC03-BP02](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_permissions_least_privileges.html)
- **Audit and rotate long-term credentials** — if long-lived credentials are unavoidable, store them in AWS Secrets Manager with automatic rotation and audit logging. [SEC02-BP05](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_identities_audit.html)

Use Amazon GuardDuty and AWS CloudTrail to detect abnormal IAM activity and identify potentially compromised credentials.

---

## 2. Implement Defense in Depth

Even with temporary credentials and least privilege, a single compromised account can publish malicious packages. Defense in depth creates multiple layers of protection that prevent sprawl after initial compromise.

### Artifact Signing with AWS Signer

[AWS Signer](https://docs.aws.amazon.com/signer/latest/developerguide/Welcome.html) provides cryptographic signing for packages and container images using FIPS 140-3 Level 3 validated HSMs. The signing authorization model separates concerns — developer credentials shouldn't have signing permissions; only CI/CD pipeline roles should.

**Container image signing workflow** (with new Amazon ECR managed signing):
1. Developer/CI/CD builds an image and pushes to Amazon ECR
2. Amazon ECR automatically triggers signing via Signer
3. Signer verifies permissions and signs the image digest
4. Signature stored alongside the image in OCI artifact format
5. Admission controllers (Kyverno for EKS, lifecycle hooks for ECS) verify signatures before deployment

**Benefits over custom signing infrastructure:** fully managed, automated, centralized governance, native EKS/ECS integration, FIPS 140-3 Level 3 compliance.

### Centralize Dependency Management

Use [AWS CodeArtifact](https://aws.amazon.com/codeartifact/) to host and manage software packages. Package group configuration defines an approved list of upstream sources and blocks all others — a direct control against typosquatting attacks. Centralization allows pinning dependency versions and quickly removing compromised packages across your portfolio. [SEC11-BP05](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_appsec_centralize_services_for_packages_and_dependencies.html)

For npm packages, **provenance attestation** (available since npm 9.5) links a published package to its source repository and CI/CD workflow using Sigstore. Verification ensures the package wasn't tampered between build and publication.

### Scan Dependencies Throughout the SDLC

- **In development** — Kiro performs software composition analysis during code reviews
- **In repositories and pipelines** — Amazon Inspector scans code, dependencies, and IaC
- **For container images** — Amazon Inspector provides continuous scanning of ECR images and CI/CD integration

Traditional CVE-based scanners miss supply chain zero-days like Shai-Hulud. AWS detects these through **behavioral analysis at scale** — cross-account signals from MadPot threat intelligence and incident response across millions of customers. Findings are contributed to the OpenSSF Malicious Packages Repository (MAL-ID). For the tea.xyz campaign, average time from submission to formal identification was ~30 minutes.

**SBOMs** (SPDX/CycloneDX) enable rapid assessment of exposure during incidents — identify which applications contain compromised packages and prioritize remediation.

### Configure Logging and Monitoring

Use CloudTrail, GuardDuty, Security Hub, and AWS Config for visibility. Key CloudTrail events to monitor for supply chain incidents:

- `sts:AssumeRole` from unexpected IP addresses or regions
- `secretsmanager:GetSecretValue` from unfamiliar sources
- `ecr:PutImage` from developer workstations (bypassing CI/CD)
- `lambda:UpdateFunctionCode` outside normal deployment windows
- `iam:CreateAccessKey` followed by immediate API activity

Combine with Amazon EventBridge rules to trigger automated responses when Amazon Inspector detects malicious packages or unusual credential access patterns. [SEC04: Detection](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/detection.html)

---

## Conclusion

Recent supply chain incidents reflect ongoing efforts by threat actors targeting package registries, CI/CD pipelines, and developer credentials. The controls described here work together:

- **Temporary credentials** limit the value of stolen tokens
- **Centralized dependency management** reduces attack surface at the registry level
- **Artifact signing** ensures unsigned artifacts cannot reach production
- **Continuous scanning** identifies compromised packages early
- **Logging and monitoring** enables rapid detection and forensics

Each layer narrows the window of opportunity for a threat actor. The Well-Architected Framework provides the blueprint — implementation is up to you.
