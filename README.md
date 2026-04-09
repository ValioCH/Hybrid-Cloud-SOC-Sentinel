# 🛡️ Hybrid Cloud SOC Architecture
### Microsoft Sentinel & Hardened Endpoint Integration

## 📑 Executive Summary
Implementation of an end-to-end Security Operations Center (SOC) bridging a hardened physical Windows 11 environment with Azure's cloud-native SIEM/SOAR (Microsoft Sentinel). This project demonstrates full-stack visibility, from bare-metal optimization to cloud-native incident detection.

---

## 🏗️ Technical Stack
- **SIEM/SOAR:** Microsoft Sentinel | Log Analytics Workspace (LAW)
- **Hybrid Infrastructure:** Azure Arc | Azure Monitor Agent (AMA)
- **Endpoint:** ASUS TUF Gaming FA706L (Windows 11 Pro)
- **ASR (Attack Surface Reduction):** Chris Titus WinUtil (Processes: 160 -> 118)
- **Identity & Compliance:** Microsoft Defender for Cloud | Granular Windows Security Auditing
- **Attack Simulation:** THC Hydra (Kali Linux)

---

## 📂 Repository Structure
- `/queries` - Production-ready KQL detection scripts.
- `/docs` - Architectural milestones and technical deep-dives.
- `/evidence` - Evidence of successful log ingestion and SOC visibility.

---

## 🚀 Project Phases & Key Milestones

### Phase 1: Deployment & Pipeline Validation (COMPLETED)
- **Hardening Baseline:** Established a trusted OS baseline by eliminating OEM bloatware and telemetry.
- **Telemetry Engineering:** Configured Data Collection Rules (DCR) to stream high-fidelity event logs.
- **Troubleshooting:** Resolved critical AMA ingestion failure and hardware-level connectivity issues.

### Phase 2: Hybrid Connectivity & Agent Deployment
- **Challenge:** Azure Arc onboarding blocked by `PSSecurityException`.
- **Cause:** Strict PowerShell Execution Policy from Phase 1 hardening.
- **Resolution:** Executed session-specific bypass:  
  `powershell.exe -ExecutionPolicy Bypass -File .\OnboardingScript.ps1`

### Phase 3: Telemetry Stabilization & Sentinel Ingestion
- **Challenge:** 48-hour "Heartbeat" gap in Log Analytics (No security events ingested).
- **Troubleshooting:** Performed Gap Analysis via KQL, revealing policy interference with the AMA.
- **Resolution:** 1. Re-configured DCR with custom XPath queries for Event IDs 4624 & 4625.
  2. Performed clean redeployment of the AMA agent.
- **Validation:** [Heartbeat Gap Analysis Query](./queries/heartbeat_analysis.kql)

### Phase 4: Attack Simulation & Threat Hunting (COMPLETED)
- **Scenario:** Controlled RDP Brute Force attack using **THC Hydra** from Kali Linux.
- **Observation:** Windows Account Lockout policies triggered after the 5th attempt (First line of defense).
- **Sentinel Analysis:** Traced the attack chain and visualized the source IP in the **Sentinel Investigation Graph**.
- **Outcome:** Deployed a custom Analytics Rule to automate incident creation for future brute-force attempts.

---

## 🔍 Detection Samples (KQL)

### [NEW] Brute Force Detection
Advanced monitoring for **EventID 4625** (Logon Failure). Identifies source IP, targeted accounts, and frequency to differentiate between single failures and automated attacks.
- **Script:** [brute_force_detection.kql](./queries/brute_force_detection.kql)