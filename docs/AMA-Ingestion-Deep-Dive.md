# Deep Dive: Solving the Telemetry Ingestion Gap

After successfully connecting the physical endpoint via Azure Arc, the environment faced a critical visibility issue: **Microsoft Sentinel was not receiving Security Event logs.**

## 🔍 Root Cause Analysis
The initial system hardening (Phase 1) implemented aggressive local audit policies and disabled non-essential services. This led to:
1. **AMA Agent Instability:** The Azure Monitor Agent (AMA) failed to establish a consistent heartbeat.
2. **Log Filtering:** The default Security XPath in the Data Collection Rule (DCR) was too broad, causing it to be silently dropped by the hardened OS restrictions.

## 🛠️ The Technical Fix (XPath Customization)
To resolve this, I transitioned from the default "All Security Events" stream to a granular **custom XPath query**. This ensures that only high-fidelity logs are prioritized, reducing noise and bypassing ingestion bottlenecks.

### The Granular Query:
The following XPath was implemented in the DCR (Data Collection Rule) to specifically target Logon/Logoff activity:

`Security!*[System[(EventID=4624 or EventID=4625 or EventID=4648)]]`

**Key Event IDs monitored:**
* **4624:** Successful Logon (Verification of access).
* **4625:** Failed Logon (Detection of Brute Force attempts).
* **4648:** Logon using explicit credentials (Lateral movement detection).

## 📈 Final Validation
After applying the custom DCR and performing a **clean re-installation of the AMA agent**, the telemetry pipeline stabilized. 

* **Validation Query:** `Heartbeat | summarize LastCall = max(TimeGenerated) by Computer`
* **Result:** Consistent 100% ingestion uptime.