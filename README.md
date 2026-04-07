# 🛡️ Hybrid Cloud SOC Architecture: Microsoft Sentinel & Hardened Endpoint

## 📑 Executive Summary
Implementation of an end-to-end Security Operations Center (SOC) bridging a hardened physical Windows 11 environment with Azure's cloud-native SIEM/SOAR (Microsoft Sentinel). This project demonstrates full-stack visibility, from bare-metal optimization to cloud-native incident detection.

## 🏗️ Technical Stack
- **SIEM/SOAR:** Microsoft Sentinel | Log Analytics Workspace (LAW).
- **Hybrid Infrastructure:** Azure Arc | Azure Monitor Agent (AMA).
- **Endpoint:** ASUS TUF Gaming FA706L (Windows 11 Pro).
- **ASR (Attack Surface Reduction):** Chris Titus WinUtil (Reduced background processes from 160 to 118).
- **Identity & Compliance:** Microsoft Defender for Cloud | Granular Windows Security Auditing.

## 🚀 Phase 1: Deployment & Pipeline Validation (COMPLETED)
- **Hardening Baseline:** Established a trusted OS baseline by eliminating OEM bloatware and telemetry.
- **Telemetry Engineering:** Configured Data Collection Rules (DCR) to stream high-fidelity event logs (Auth Success/Failure).
- **Troubleshooting:** Resolved a critical AMA ingestion failure and hardware-level connectivity issues to maintain SOC uptime.

## 🔍 Detection Samples (KQL)
### [NEW] Brute Force Monitoring
Monitoring for EventID 4625 (An account failed to log on) to detect unauthorized access attempts.
*(Query code included in repository /KQL folder)*

## 📂 Repository Structure
- `/KQL`: Production-ready detection queries.
- `/Docs`: Architectural milestones and technical deep-dives.
- `/Artifacts`: Evidence of successful log ingestion and SOC visibility.

## 🚀 Key Milestones & Troubleshooting

### Phase 2: Hybrid Connectivity & Agent Deployment
* **Challenge:** The onboarding script for Azure Arc was blocked by the hardened system's PSSecurityException (UnauthorizedAccess).
* **Cause:** Strict PowerShell Execution Policy (AllSigned/Restricted) from Phase 1 hardening.
* **Resolution:** Executed a session-specific bypass to allow agent initialization:
  `powershell.exe -ExecutionPolicy Bypass -File .\OnboardingScript.ps1`
* **Evidence:** See logs in `/evidence/Post 3 - Agent problem.jpg`

### Phase 3: Telemetry Stabilization & Sentinel Ingestion
* **Challenge:** 48-hour "Heartbeat" gap in Log Analytics. No security events were being ingested after initial connection.
* **Troubleshooting:** Used KQL to perform a Gap Analysis, revealing that hardening policies were interfering with the Azure Monitor Agent (AMA).
* **Resolution:** 1. Re-configured Data Collection Rules (DCR) with custom XPath queries for Event IDs 4624 & 4625.
  2. Performed a clean redeployment of the AMA agent to reset local communication channels.
* **KQL Validation:** [Heartbeat Gap Analysis Query](./queries/heartbeat_analysis.kql)