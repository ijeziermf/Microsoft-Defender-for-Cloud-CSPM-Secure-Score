# Microsoft Defender for Cloud, CSPM & Secure Score

> **Azure Cloud Security Posture Management, tenant-level CSPM onboarding, Secure Score remediation, NIST compliance mapping.**

---

## What This Demonstrates

| Capability | Details |
|---|---|
| **Platform** | Microsoft Azure, Microsoft Defender for Cloud |
| **Focus Area** | Cloud Security Posture Management (CSPM), Secure Score |
| **Deliverables** | Secure Score analysis, remediation actions, compliance mapping |
| **Stakeholder Focus** | Cloud security, compliance officers, IT operations |
| **Industry Relevance** | Cloud-forward organizations, Azure customers, regulated industries |

---

## Overview

This lab documents the complete onboarding of Azure resources into **Microsoft Defender for Cloud**, enabling **Cloud Security Posture Management (CSPM)**, analyzing **Secure Score**, and implementing remediations across compute, networking, identity, and data protection.

The key discovery: **CSPM must be enabled at the tenant level, not just subscription level** for full risk detection and Secure Score accuracy. This insight significantly improved detection coverage and scoring completeness.

---

## Key Discoveries

| Issue | Root Cause | Resolution |
|---|---|---|
| Missing risk detections | CSPM enabled at subscription level only | Enabled CSPM at **tenant level** |
| Incomplete Secure Score | Identity and Data Protection findings absent | Tenant-level CSPM unlocked all categories |
| No Identity risks | Scope limitation | Tenant-level enablement surfaced 3 High, 4 Medium, 3 Low findings |

---

## Secure Score Analysis

### Initial State

| Metric | Value |
|---|---|
| **Secure Score** | 25% (6/32 recommendations active) |
| **Status** | Initializing (normal for new onboarding) |
| **Top Failing Controls** | Network, Compute, Data Protection, Identity & Access Management |

### Post-Remediation State

| Metric | Value | Change |
|---|---|---|
| **Secure Score** | Improved (see screenshot) | + remediation impact |
| **Recommendations Resolved** | NSG assignment, SSH key enforcement, encryption at host | 3 major controls |
| **Compliance Mappings** | Azure Security Benchmark, NIST 800-53, CIS Controls | Full framework coverage |

---

## Remediation Actions

### 1. Protect Internet-Facing VMs with NSGs

| Aspect | Details |
|---|---|
| **Issue** | VM flagged as internet-facing without Network Security Group |
| **Resolution** | Assigned NSG at **subnet level** (recommended best practice) |
| **Validation** | Defender automatically updated recommendation to "Completed" |
| **Secure Score Impact** | Informational (no score change) |

**Screenshot:** NSG assignment and validation

---

### 2. Require SSH Keys for Linux Authentication

| Aspect | Details |
|---|---|
| **Issue** | Password authentication enabled (less secure than key-based) |
| **Resolution** | Generated SSH key pair, disabled password authentication |
| **Validation** | SSH login confirmed from Azure Cloud Shell and local terminal |
| **Secure Score Impact** | Identity & Access Management control resolved |

**Note:** No passphrase used for lab simplicity (production should enforce passphrase).

---

### 3. Enable Encryption at Host

| Aspect | Details |
|---|---|
| **Issue** | VM created without encryption at host option |
| **Resolution** | Snapshot VM → Recreated with encryption at host enabled |
| **Validation** | Recommendation resolved successfully |
| **Secure Score Impact** | Data Protection control resolved |

**Real-World Constraint:** This mirrors production cloud engineering limitations, some settings require resource recreation.

---

## Regulatory Compliance Mapping

Defender for Cloud maps environment to multiple compliance frameworks:

| Framework | Coverage |
|---|---|
| **Azure Security Benchmark** | Native Azure security requirements |
| **NIST SP 800-53** | Federal security controls (US compliance) |
| **CIS Controls** | Industry security best practices |

**Screenshot:** Compliance dashboard showing framework alignment

---

## Challenges & Lessons Learned

| Challenge | Root Cause | Lesson |
|---|---|---|
| CSPM not showing risks | Enabled at subscription level only | **Always enable at tenant level** for full coverage |
| Secure Score initialization delays | Defender evaluates resources in cycles | Normal behavior, allow time for assessment |
| VM hardening conflicts | Lab 1 hardening vs. Defender recommendations | Validate compensating controls, document deviations |
| Encryption at host limitation | Setting only available at VM creation | Plan encryption requirements before deployment |

---

## Value to GRC Consulting

This lab demonstrates **hands-on cloud security implementation** for:

| Service | Application |
|---|---|
| **Cloud Security Assessments** | CSPM onboarding, Secure Score analysis, remediation planning |
| **Compliance Mapping** | NIST, CIS, Azure Benchmark alignment |
| **Cloud Hardening** | NSG configuration, SSH enforcement, encryption at rest |
| **Executive Reporting** | Secure Score trends, compliance posture, risk reduction |

---

## Tools & Platforms

| Tool/Platform | Use |
|---|---|
| **Microsoft Azure** | Cloud environment, VM deployment |
| **Microsoft Defender for Cloud** | CSPM, Secure Score, compliance mapping |
| **Log Analytics Workspace** | Advanced analytics, log retention |
| **Azure Security Benchmark** | Compliance framework |
| **NIST SP 800-53** | Compliance framework |
| **CIS Controls** | Compliance framework |

---

## Key Takeaways

1. **Tenant-Level CSPM is Critical**, Subscription-level enablement misses Identity and Data Protection risks
2. **Secure Score = Continuous Improvement**, Not a one-time fix, ongoing monitoring required
3. **Cloud Hardening Has Constraints**, Some settings (encryption at host) require upfront planning
4. **Compliance Mapping Adds Value**, Multiple frameworks demonstrate audit readiness

---

## Growth & Next Iterations

Future enhancements:
- Automated Secure Score monitoring and alerting
- Integration with Azure Policy for continuous compliance
- Expansion to multi-subscription governance
- Custom compliance initiative development

---

## Screenshots

| Description | Image |
|---|---|
| Defender for Cloud Overview | ![Defender Overview](https://github.com/user-attachments/assets/e0d61dcc-5486-43ef-92be-8347a70e1bd4) |
| CSPM Tenant-Level Enablement | ![CSPM Tenant](https://github.com/user-attachments/assets/b6de68b1-4748-4fe8-bc74-e92ca6345a85) |
| Log Analytics Connection | ![Log Analytics](https://github.com/user-attachments/assets/c369decc-4ec3-4560-86ef-02512183bc39) |
| Initial Secure Score (25%) | ![Initial Score](https://github.com/user-attachments/assets/cbfc41e2-8a3f-4fb5-a42a-2966fb3060c1) |
| NSG Assignment | ![NSG](https://github.com/user-attachments/assets/2d567fb0-1ca7-40f7-925c-611fa68b45fe) |
| SSH Key Configuration | ![SSH Keys](https://github.com/user-attachments/assets/963c46d4-12c8-4633-97a8-8b6dacd6d7ca) |
| Encryption at Host | ![Encryption](https://github.com/user-attachments/assets/8ce76f68-c49d-494b-a157-0e473cbbf836) |
| Compliance Mapping | ![Compliance](https://github.com/user-attachments/assets/15c260c2-5950-4e58-aa2c-4dd3dc6e2c91) |
| Post-Remediation Score | ![Final Score](https://github.com/user-attachments/assets/f0d45dd8-fdfd-4734-b38f-9cc519caebfe) |

---

## License

This project is for educational and portfolio demonstration purposes. Methodology may be adapted for client engagements.
