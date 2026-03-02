# Lab 2 — Microsoft Defender for Cloud (CSPM) & Secure Score

## Overview
This lab focuses on onboarding Azure resources into Microsoft Defender for Cloud, enabling Cloud Security Posture Management (CSPM), analyzing Secure Score, and implementing remediations across compute, networking, identity, and data protection.

During this lab, I discovered that CSPM must be enabled **at the tenant level**, not just the subscription level for full risk detection and Secure Score accuracy. This insight significantly improved the quality of my results.

---

# 1. Environment Setup

## 1.1 Enable Defender for Cloud
Enabled Defender for Cloud at the subscription level.

**Screenshot:**  
`![Enable Defender for Cloud](./screenshots/defender-enable.png)`

---

## 1.2 Enable CSPM (Tenant-Level Requirement)
Initially, I only enabled CSPM at the subscription level, which caused:
- Missing risk detections  
- Incomplete Secure Score  
- No Identity or Data Protection findings  

After enabling CSPM at the **tenant level**, Defender began surfacing:
- 3 Low  
- 4 Medium  
- 3 High severity recommendations  

**Screenshot:**  
`![Enable CSPM](./screenshots/cspm-enable.png)`

---

## 1.3 Connect Log Analytics Workspace
Connected my Log Analytics workspace for advanced analytics and compliance mapping.

**Screenshot:**  
`![LAW Connection](./screenshots/law-connection.png)`

---

# 2. Secure Score Analysis

## 2.1 Initial Secure Score
Secure Score initially showed **initializing**, then updated to **25%**, with **6/32 recommendations active**.

**Screenshot:**  
`![Initial Secure Score](./screenshots/secure-score-initial.png)`

---

## 2.2 Top Failing Control Families
Defender identified the following as the weakest areas:

1. Network  
2. Compute  
3. Data Protection  
4. Identity & Access Management  

**Screenshot:**  
`![Control Families](./screenshots/control-families.png)`

---

# 3. Remediation Actions

## 3.1 Protect Internet-Facing VMs with NSGs
Defender flagged my VM as internet-facing without an NSG.

### Fix:
- Assigned NSG at the **subnet level** (recommended)
- Validated inbound/outbound rules
- Defender automatically updated the recommendation to “Completed”

Secure Score did **not** change because this control was informational.

**Screenshot:**  
`![NSG Fix](./screenshots/nsg-fix.png)`

---

## 3.2 Require SSH Keys for Linux Authentication
Defender recommended enforcing SSH key authentication.

### Fix:
- Generated SSH key pair  
- Disabled password authentication  
- Updated VM configuration  
- Enabled SSH login from both Azure Cloud Shell and my Mac Terminal  

I intentionally used **no passphrase** for lab simplicity.

**Screenshot:**  
`![SSH Fix](./screenshots/ssh-fix.png)`

---

## 3.3 Enable Encryption at Host
My VM did not support enabling encryption at host because I originally **deselected** the option during creation.

### Fix:
- Created a **snapshot** of the VM  
- Deployed a **new VM** from the snapshot  
- Enabled encryption at host during creation  

This allowed the recommendation to resolve successfully.

**Screenshot:**  
`![Encryption at Host](./screenshots/encryption-fix.png)`

---

# 4. Regulatory Compliance

Mapped my environment to:
- Azure Security Benchmark  
- NIST 800-53  
- CIS Controls  

**Screenshot:**  
`![Regulatory Compliance](./screenshots/regulatory-compliance.png)`

---

# 5. Post-Remediation Secure Score

Secure Score improved after applying remediations and enabling tenant-level CSPM.

**Screenshot:**  
`![Post Secure Score](./screenshots/secure-score-final.png)`

---

# 6. Reflection & Challenges

This lab surfaced several real-world challenges that strengthened my understanding of Azure security posture management.

### CSPM Not Showing Risks
I initially saw **no risks** because CSPM was only enabled at the subscription level.  
Enabling it at the **tenant level** unlocked:
- Identity risks  
- Data protection risks  
- Compute/networking findings  

### Secure Score Initialization Delays
Secure Score took time to update, which is normal because Defender evaluates resources in cycles.

### VM Hardening Conflicts
Some recommendations conflicted with my Lab 1 hardening steps like SSH-only login.  
I validated compensating controls and documented intentional deviations.

### Encryption at Host Limitation
Because I disabled encryption at host during VM creation, I had to:
- Snapshot the VM  
- Recreate it with encryption enabled  

This mirrors real-world cloud engineering constraints to keep in mind moving forward.

### Outcome
This lab improved my understanding of:
- CSPM lifecycle  
- Secure Score logic  
- Azure resource provider dependencies  
- VM hardening  
- Network security  
- Compliance frameworks  

