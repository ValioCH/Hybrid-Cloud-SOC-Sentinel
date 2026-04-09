# Security Simulation: RDP Brute Force with THC Hydra

## 🎯 Objective
To verify the detection capabilities of Microsoft Sentinel and testing local account lockout policies against an automated credential stuffing/brute force attack.

## 🛠️ Tools & Environment
- **Attacker:** Kali Linux (Rolling Release)
- **Tool:** THC Hydra v9.5
- **Target:** Hardened Windows 11 Pro (Azure Arc Enabled)
- **Protocol:** RDP (Port 3389)

## ⚡ Execution
The attack was executed using a common password wordlist against a known local user account to simulate a targeted external threat.

**Command used:**
`hydra -l HackerTarget -P /usr/share/wordlists/rockyou.txt -t 4 rdp://192.168.1.27`

## 📊 Observations
1. **Local Defense:** The Windows Account Lockout Policy triggered after 5 failed attempts, effectively neutralizing the brute force but causing a local Denial of Service (DoS) for the user.
2. **Telemetry:** Security Event ID 4625 was successfully generated and captured by the Azure Monitor Agent (AMA).