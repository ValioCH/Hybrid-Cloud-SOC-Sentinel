# 🛡️ Hybrid Cloud SOC Lab & SOAR Automation

## 🚀 Executive Summary
This project demonstrates the architecture and implementation of an enterprise-grade **Hybrid SOC environment**. It bridges on-premises infrastructure with cloud-native security capabilities using **Microsoft Sentinel**, **Azure Arc**, and **Terraform**. The core highlight is a custom-built **SOAR (Security Orchestration, Automation, and Response)** workflow that automates phishing investigations using the **VirusTotal API v3**.

---

## 🏗️ Architecture Overview
The lab is built on a Zero Trust foundation, consisting of:
- **On-Premises Target:** A hardened Windows 11 Pro workstation managed via **Azure Arc**.
- **Cloud Infrastructure:** Azure VNETs, isolated subnets, and **Azure Bastion** for secure management.
- **Identity Layer:** **Entra ID** (vchsecurity.com) integrated with a cloud-hosted **Active Directory Domain Controller**.
- **SIEM/SOAR:** **Microsoft Sentinel** acting as the central brain for telemetry aggregation and automated response.
- **Infrastructure as Code:** Entire cloud stack deployed via **Terraform** for scalability and repeatability.

---

## 🛠️ Phase-by-Phase Technical Breakdown

### Phase 1: Endpoint Hardening & Azure Arc Integration
- **Attack Surface Reduction (ASR):** Optimized Windows 11 Pro baseline, reducing background processes from 160 to 118.
- **Hybrid Connectivity:** Overcame PowerShell execution policy barriers to onboard physical hardware into **Azure Resource Manager (ARM)** via **Azure Arc**.

### Phase 2: Telemetry Orchestration
- **Data Collection Rules (DCR):** Configured the **Azure Monitor Agent (AMA)** with custom XPath filters for Event IDs 4624 (Logon) and 4625 (Failed Logon).
- **KQL Gap Analysis:** Utilized Heartbeat logs to identify and resolve telemetry ingestion outages.

### Phase 3: Zero Trust & Network Security
- **Perimeter Defense:** Eliminated public RDP exposure by deploying **Azure Bastion** and enforcing "deny-by-default" Network Security Groups (NSGs).
- **Identity Hardening:** Enforced Granular RBAC and strict Group Policy Objects (GPOs), including account lockout policies after 5 failed attempts.

### Phase 4: SOAR Automation (The Crown Jewel) 💎
Implemented an automated **Phishing Response Playbook**:
1. **Detection:** Custom KQL analytics detect suspicious URLs in security logs.
2. **Analysis:** **Logic App** triggers, extracts the URL entity, and queries the **VirusTotal API v3**.
3. **Automated Response:** If the malicious threshold is met (e.g., 12+ engines confirmed), the system:
    - Enriches the incident with Threat Intel comments.
    - Automatically closes the incident as a **True Positive**.
    - Updates NSG rules to block the malicious source.

---

## 🧠 Technical Challenges & Solutions
- **The "JSON Trap":** Resolved `InvalidJson` errors in Logic Apps by manually editing the code view to ensure clean JSON array payloads instead of string-wrapped expressions.
- **State Management:** Developed a dynamic array logic using the `union()` expression to prevent NSG rule overwrites, ensuring the blocklist accumulates attackers instead of remembering only the latest one.
- **Cloud Constraints:** Handled "SkuNotAvailable" regional errors by decoupling location logic in **Terraform**, allowing a full stack redeployment to a different region in <60 seconds.

---

## 📈 Key Results
- **Zero-Touch Response:** Automated phishing investigation reduced response time from hours to seconds.
- **Full Visibility:** Centralized telemetry from hybrid sources into a single pane of glass in Microsoft Sentinel.
- **Scalable Defense:** Infrastructure is fully version-controlled and can be deployed via Terraform.

---

## 📂 Project Media
*Detailed screenshots and logs are available in the `/screenshots` folder.*

---

**Contact & Feedback:**
Feel free to reach out via [LinkedIn](https://www.linkedin.com/in/valentin-cholakov) to discuss SOC automation, Azure security, or Terraform!
README.md
Displaying README.md.