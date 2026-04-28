# Credential Dumping Response Playbook

## Alert Trigger

This playbook is initiated when suspicious access to the LSASS process memory is detected.

Access to LSASS memory is commonly associated with credential dumping activity used by attackers to extract authentication material.

---

## Severity

High

Severity increases if:

- Activity originates from a non-administrative process
- Additional suspicious PowerShell execution is observed
- Authentication anomalies follow LSASS access
- Multiple endpoints show similar behavior

---

## Detection Sources

Tools:

Wazuh  
Windows Endpoint Telemetry  
Elastic Stack

Detection Rule:

lsass-access-non-system.xml

---

## Investigation Steps

SOC analyst workflow:

1. Identify process accessing LSASS memory
2. Review parent-child process relationships
3. Confirm whether the process is legitimate
4. Identify user account associated with activity
5. Review recent authentication activity from the endpoint
6. Check for lateral movement indicators
7. Correlate activity with Suricata alerts

---

## Containment Actions

Recommended response actions:

- Terminate suspicious process
- Isolate affected endpoint if compromise suspected
- Reset credentials associated with endpoint
- Monitor for additional credential access activity

---

## Escalation Criteria

Escalate incident if:

- Privileged credentials are accessed
- Multiple credential dumping attempts detected
- Lateral movement behavior observed
- Reverse shell activity detected

---

## MITRE ATT&CK Mapping

Technique:

T1003.001 — LSASS Credential Dumping

---

## Analyst Notes

Credential dumping is a high-confidence indicator of attacker post-exploitation behavior and should be investigated immediately.
