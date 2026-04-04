Project Phases & Technical Milestones

Phase 1: Endpoint Environment & Hardening
Bare-Metal OS Deployment: Performed a clean installation of Windows 11 Pro on physical hardware to eliminate OEM bloatware and ensure a trusted baseline.
- System Hardening & Optimization: Leveraged the Chris Titus Tech Windows Utility to streamline system services, remove telemetry/bloat, and close unnecessary logical ports to reduce the attack surface.
- Identity & Asset Governance: Registered a custom personal domain and integrated it with Microsoft 365 / Entra ID (Azure AD). Established professional identity management and verified ownership of the lab's digital perimeter.

Phase 2: Hybrid Cloud Fabric (Azure Arc)
- Azure Arc Onboarding: Projecting the physical on-premises asset into the Azure Resource Manager (ARM) plane via Azure Arc for unified management.
- Network Path Engineering: Diagnosed and resolved log ingestion failures by deploying and configuring a Data Collection Endpoint (DCE) in the West Europe region.
- Telemetry Pipeline: Successfully deployed the Azure Monitor Agent (AMA). Configured Data Collection Rules (DCR) to stream Windows Event Logs and Performance Counters to the cloud.

Phase 3: SIEM/SOAR & XDR Integration
- Microsoft Sentinel Provisioning: Initialized the SIEM/SOAR instance on top of the Log Analytics Workspace (law-vch-security).
- XDR Stack Integration: Configured and verified Microsoft Defender XDR data connectors, including:
- Microsoft Defender for Endpoint
- Microsoft Entra ID (formerly Azure AD) Protection
- Microsoft Defender for Cloud Apps
- Pipeline Verification: Validated end-to-end data flow using Kusto Query Language (KQL) to confirm "Heartbeat" and security event ingestion.