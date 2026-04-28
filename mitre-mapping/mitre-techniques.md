# MITRE ATT&CK Technique Mapping

This document maps detection coverage from the **Home Threat Detection & Incident Response Lab** to MITRE ATT&CK techniques observed during simulated attacker activity.

The lab demonstrates how endpoint telemetry, network monitoring, and automated response workflows correlate to detect attacker behavior across multiple stages of the intrusion lifecycle.

---

# Detection Coverage Matrix

| Technique | Name | Detection Source | Rule / Telemetry |
|----------|------|-----------------|------------------|
| T1046 | Network Service Discovery | Suricata | Port scan alerts |
| T1110 | Brute Force Authentication | Windows Logs + Wazuh | Authentication failure monitoring |
| T1059.001 | PowerShell Execution | Wazuh Custom Rule | powershell-encoded-command.xml |
| T1003.001 | LSASS Credential Dumping | Wazuh Custom Rule | lsass-access-non-system.xml |
| T1048.003 | DNS Data Exfiltration | Suricata Custom Rule | dns-tunneling.rules |
| T1059.004 | Reverse Shell Execution | Suricata Custom Rule | reverse-shell.rules |

---

# Detection Strategy Overview

The lab detection pipeline provides layered behavioral visibility across both endpoint and network telemetry sources.

Detection layers include:

- Network reconnaissance monitoring
- Authentication attack detection
- PowerShell execution monitoring
- Credential access detection
- DNS tunneling detection
- Reverse shell detection
- Automated containment using Active Response

Together, these detections simulate how enterprise SOC environments correlate telemetry across multiple monitoring platforms to identify attacker activity throughout the intrusion lifecycle.

---

# SOC Detection Pipeline Alignment

This lab environment mirrors a simplified enterprise detection workflow:

Attacker Activity  
→ Network Telemetry (Suricata)  
→ Endpoint Telemetry (Wazuh Agent)  
→ Detection Rules (Custom + Built-in)  
→ Log Aggregation (Elastic Stack)  
→ Analyst Investigation (Kibana Dashboards)  
→ Automated Containment (Active Response)

This mapping demonstrates practical alignment between simulated attacker behavior and MITRE ATT&CK detection coverage strategies.
