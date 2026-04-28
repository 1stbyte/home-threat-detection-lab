# Suspicious PowerShell Execution Response Playbook

## Alert Trigger

This playbook is initiated when PowerShell executes using encoded command arguments.

Encoded PowerShell execution is commonly used to hide attacker payload execution and evade detection mechanisms.

---

## Severity

Medium → High

Severity increases if:

- Execution occurs outside normal administrative activity
- Activity originates from unexpected user accounts
- Network connections follow execution
- Additional attacker techniques appear in timeline

---

## Detection Sources

Tools:

Wazuh  
Windows Process Telemetry  
Elastic Stack

Detection Rule:

powershell-encoded-command.xml

---

## Investigation Steps

SOC analyst workflow:

1. Identify executing user account
2. Review command-line arguments
3. Identify parent process
4. Determine origin of execution
5. Check for outbound network connections
6. Correlate activity with authentication logs
7. Review endpoint timeline for persistence indicators

---

## Containment Actions

Recommended response actions:

- Terminate suspicious PowerShell process
- Validate legitimacy with system owner
- Block suspicious external connections if observed
- Monitor endpoint for additional suspicious execution

---

## Escalation Criteria

Escalate incident if:

- Execution originates from unknown user
- Activity targets multiple endpoints
- Persistence mechanisms detected
- Credential dumping activity follows execution

---

## MITRE ATT&CK Mapping

Technique:

T1059.001 — PowerShell  
T1027 — Obfuscated Files or Information

---

## Analyst Notes

Encoded PowerShell execution is frequently observed during attacker lateral movement and payload delivery stages.
