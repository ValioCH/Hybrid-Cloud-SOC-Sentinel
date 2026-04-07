# Project Phases & Technical Milestones

## Phase 1: Endpoint Environment & Hardening
* **Bare-Metal OS Deployment:** Performed a clean installation of Windows 11 Pro on physical hardware to eliminate OEM bloatware and ensure a trusted baseline.
* **System Hardening & Optimization:** Leveraged the Chris Titus Tech Windows Utility to streamline system services, reduce the attack surface (from 160 to 118 processes), and close unnecessary logical ports.
* **Identity & Asset Governance:** Registered a custom personal domain and integrated it with Microsoft 365 / Entra ID. Established a professional identity management perimeter.

## Phase 2: Hybrid Cloud Fabric & Agent Troubleshooting
* **Azure Arc Onboarding:** Projected the physical workstation into Azure Resource Manager (ARM).
* **Technical Roadblock (Execution Policy):** Resolved a `PSSecurityException` during agent deployment caused by Phase 1 hardening. Implemented a session-specific `-ExecutionPolicy Bypass`.
* **Telemetry Pipeline:** Successfully deployed the Azure Monitor Agent (AMA). Configured Data Collection Rules (DCR) to stream Windows Event Logs.

## Phase 3: SIEM/SOAR & Telemetry Engineering
* **Microsoft Sentinel Provisioning:** Initialized the SIEM instance on top of the Log Analytics Workspace (`law-vch-security`).
* **Incident: Telemetry Outage (48h Gap):** Diagnosed a total ingestion failure using KQL gap analysis.
* **Resolution:** 1. Re-engineered DCR with **Custom XPath Queries** (targeting Event IDs 4624, 4625).
    2. Performed a clean AMA agent redeployment to restore the "Heartbeat" flow.
* **XDR Stack Integration:** Verified connectors for Microsoft Defender for Cloud and Entra ID Protection.

## Phase 4: Vulnerability Management (Current)
* **Initial Assessment:** Stabilized data flow allowed Defender for Cloud to identify the first critical security gaps (missing vulnerability assessment solution).
* **Remediation:** Triggered "Quick Fix" deployments to begin deep-system vulnerability scanning.