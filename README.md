# Microsoft Defender for Cloud (CSPM) & Secure Score

## Overview
This lab focuses on onboarding Azure resources into Microsoft Defender for Cloud, enabling Cloud Security Posture Management (CSPM), analyzing Secure Score, and implementing remediations across compute, networking, identity, and data protection.

During this lab, I discovered that CSPM must be enabled **at the tenant level**, not just the subscription level for full risk detection and Secure Score accuracy. This insight significantly improved the quality of my results.

---

# 1. Environment Setup

## 1.1 Enable Defender for Cloud
Enabled Defender for Cloud at the subscription level.

**Screenshot:**  
<img width="1512" height="1084" alt="Screenshot 2026-02-26 at 1 08 34 AM" src="https://github.com/user-attachments/assets/e0d61dcc-5486-43ef-92be-8347a70e1bd4" />

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
<img width="1402" height="1079" alt="Screenshot 2026-02-27 at 11 51 29 AM" src="https://github.com/user-attachments/assets/b6de68b1-4748-4fe8-bc74-e92ca6345a85" />

---

## 1.3 Connect Log Analytics Workspace
Connected my Log Analytics workspace for advanced analytics and compliance mapping.

**Screenshot:**  
<img width="1784" height="896" alt="image" src="https://github.com/user-attachments/assets/c369decc-4ec3-4560-86ef-02512183bc39" />

---

# 2. Secure Score Analysis

## 2.1 Initial Secure Score
Secure Score initially showed **initializing**, then updated to **25%**, with **6/32 recommendations active**.

**Screenshot:**  
<img width="1358" height="1037" alt="Screenshot 2026-02-27 at 11 58 57 AM" src="https://github.com/user-attachments/assets/cbfc41e2-8a3f-4fb5-a42a-2966fb3060c1" />

---

## 2.2 Top Failing Control Families
Defender identified the following as the weakest areas:

1. Network  
2. Compute  
3. Data Protection  
4. Identity & Access Management  

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
<img width="1264" height="510" alt="image" src="https://github.com/user-attachments/assets/2d567fb0-1ca7-40f7-925c-611fa68b45fe" />

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
<img width="989" height="611" alt="Screenshot 2026-02-27 at 3 15 01 PM" src="https://github.com/user-attachments/assets/963c46d4-12c8-4633-97a8-8b6dacd6d7ca" />

---

## 3.3 Enable Encryption at Host
My VM did not support enabling encryption at host because I originally **deselected** the option during creation.

### Fix:
- Created a **snapshot** of the VM  
- Deployed a **new VM** from the snapshot  
- Enabled encryption at host during creation  

This allowed the recommendation to resolve successfully.

**Screenshot:**  
<img width="2586" height="990" alt="Screenshot 2026-03-03 140020" src="https://github.com/user-attachments/assets/8ce76f68-c49d-494b-a157-0e473cbbf836" />

<img width="1612" height="948" alt="Screenshot 2026-03-03 135911" src="https://github.com/user-attachments/assets/63e59d42-f005-49c7-9b73-012a6073f668" />

---

# 4. Regulatory Compliance

Mapped my environment to:
- Azure Security Benchmark  
- NIST 800-53  
- CIS Controls  

**Screenshot:** 
<img width="2348" height="1456" alt="image" src="https://github.com/user-attachments/assets/15c260c2-5950-4e58-aa2c-4dd3dc6e2c91" />

---

# 5. Post-Remediation Secure Score

Secure Score improved after applying remediations and enabling tenant-level CSPM.

**Screenshot:**  
<img width="1798" height="1180" alt="image" src="https://github.com/user-attachments/assets/f0d45dd8-fdfd-4734-b38f-9cc519caebfe" />

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

