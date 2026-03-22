# SOC Lab — Detection Engineering Project

## Overview

This project demonstrates the design and implementation of a home SOC lab used to simulate and detect real-world cyber attacks using:

- Splunk SIEM  
- Sysmon endpoint telemetry  
- Windows Security Logs  
- Kali Linux attacker  

The lab replicates a full attack lifecycle, from reconnaissance to persistence, with detection rules built for each stage.

---

## Lab Environment

| Component | Role | OS |
|----------|------|----|
| Kali Linux | Attacker | Kali |
| Windows 10 | Victim | Windows 10 |
| Splunk | SIEM | Windows |

---

## Simulated Attack Chain

| Phase | Technique | Tool |
|------|--------|------|
| Reconnaissance | Port scanning | nmap |
| Initial Access | RDP brute force | xfreerdp |
| Execution | PowerShell | IEX WebClient |
| Credential Access | LSASS dump | rundll32 |
| Persistence | Scheduled task | schtasks |

---

## Detection Engineering

Each attack stage was detected using Splunk queries and alerts.

---

### Brute Force Detection

```
index=windows EventCode=4625 Logon_Type=3
| stats count by Source_Network_Address
| where count > 5
```
