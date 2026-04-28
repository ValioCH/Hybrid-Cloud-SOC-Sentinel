# Case Study: Brute Force Detection & Investigation

## 🛡️ Sentinel Detection Logic
To identify the attack, a custom KQL Analytics Rule was deployed. The logic focuses on high-frequency logon failures from non-system IP addresses.

### Investigation Steps:
1. **Trigger:** An incident was created in Microsoft Sentinel labeled "Brute Force Attack Detected (RDP)".
2. **Analysis:** Used the **Investigation Graph** to map the relationship between the attacking IP (`kali`) and the targeted endpoint.
3. **Verification:** Cross-referenced Event Viewer logs on the local host with the `SecurityEvent` table in Log Analytics.

## 📈 Key Findings
- **Mean Time to Detect (MTTD):** Real-time (under 5 minutes based on ingestion latency).
- **Attacker Origin:** Internal Lab IP (192.168.1.3).
- **Target Integrity:** Account remained secure due to lockout policy, but visibility was crucial for identifying the source.

## ✅ Conclusion
The SOC pipeline successfully ingested, parsed, and alerted on the threat. This validates the configuration of the Data Collection Rules (DCR) and the effectiveness of the KQL detection logic.