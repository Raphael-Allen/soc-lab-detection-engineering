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
MITRE: T1110 — Brute Force

### PowerShell Execution Detection
index=windows EventCode=4104
| search ScriptBlockText="*IEX*" OR ScriptBlockText="*DownloadString*"

MITRE: T1059.001 — PowerShell

### Credential Dump Detection
index=windows EventCode=4688
| search Process_Command_Line="*lsass*"

MITRE: T1003 — Credential Dumping

### Persistence Detection
index=windows EventCode=4698

MITRE: T1053 — Scheduled Tasks

### Sysmon Detection
index=windows EventCode=3

Detects:

Network connections
Beaconing behaviour
SOC Investigation Workflow

## This lab demonstrates a real SOC process:

Alert → Investigation → Validation → Response
Steps:
Identify attacker IP
Identify targeted accounts
Analyze timeline
Check for successful login
Confirm compromise

## Key Skills Demonstrated:
SIEM deployment (Splunk)
Detection engineering
Log analysis (Windows + Sysmon)
MITRE ATT&CK mapping
Incident investigation
Threat simulation

## Outcome

Successfully built a full SOC detection lab capable of detecting:

Brute force attacks
PowerShell malware
Credential dumping
Persistence mechanisms
Network activity

## Future Improvements:
Add Sigma rules
Correlate multi-stage attacks
Build alert severity scoring
Add automated response

---
