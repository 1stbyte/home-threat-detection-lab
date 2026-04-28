# Custom Wazuh Detection Rules

This folder contains custom Wazuh XML detection rules developed for the Home Threat Detection & Incident Response Lab.

These rules simulate real SOC detection engineering workflows and are mapped to MITRE ATT&CK techniques.

## Included Rules

### PowerShell Encoded Command Detection

File:
powershell-encoded-command.xml

Detects suspicious PowerShell execution using encoded command arguments.

MITRE:

- T1059.001 — PowerShell
- T1027 — Obfuscated Files or Information

---

### LSASS Memory Access Detection

File:
lsass-access-non-system.xml

Detects processes attempting to access LSASS memory, commonly associated with credential dumping activity.

MITRE:

- T1003.001 — LSASS Credential Dumping

---

### Brute Force Auto-Block Active Response
Automatically blocks attacker IP addresses after repeated authentication failures using Wazuh Active Response.

---

## Detection Coverage Summary

These custom rules provide layered endpoint detection coverage across multiple attacker techniques:

| Detection Type | Technique |
|---------------|-----------|
| PowerShell Obfuscation | Defense Evasion |
| LSASS Credential Access | Credential Dumping |
| Authentication Brute Force | Initial Access |

Together, these rules simulate behavioral detections commonly deployed in enterprise SOC environments to identify attacker execution, credential harvesting activity, and authentication abuse.

File:
auto-block-bruteforce.xml
Automatically blocks attacker IP addresses after repeated authentication failures using Wazuh Active Response.
