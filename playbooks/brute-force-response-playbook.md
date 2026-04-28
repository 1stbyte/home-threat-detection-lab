# Brute Force Authentication Response Playbook

## Alert Trigger

This playbook is initiated when multiple failed authentication attempts are detected from a single source system within a short time window.

This behavior may indicate password spraying or brute-force credential access activity.

---

## Severity

Medium → High

Severity increases if:

- Authentication attempts succeed
- Multiple accounts are targeted
- Activity originates from external systems
- Attempts occur across multiple endpoints

---

## Detection Sources

Tools:

Wazuh  
Windows Security Logs  
Suricata IDS (optional correlation)

Relevant Events:

Windows Event ID 4625 — Failed login attempt  
Windows Event ID 4624 — Successful login attempt

---

## Investigation Steps

SOC analyst workflow:

1. Identify source IP generating failed login attempts
2. Identify targeted user accounts
3. Determine whether authentication attempts succeeded
4. Review authentication attempt timing patterns
5. Check whether multiple endpoints were targeted
6. Correlate activity with Suricata network telemetry
7. Review endpoint process activity for suspicious behavior

---

## Containment Actions

Recommended response actions:

- Block attacker IP using Wazuh Active Response
- Temporarily disable affected accounts if compromise suspected
- Reset impacted user credentials
- Increase monitoring on targeted systems

---

## Escalation Criteria

Escalate incident if:

- Authentication attempts succeed
- Privileged accounts are targeted
- Multiple endpoints show activity
- Suspicious PowerShell or LSASS activity follows authentication attempts

---

## MITRE ATT&CK Mapping

Technique:

T1110 — Brute Force

Sub-techniques:

T1110.001 — Password Guessing  
T1110.003 — Password Spraying

---

## Analyst Notes

Brute-force authentication attempts are often an early-stage attacker technique used to gain initial access.

Successful authentication following repeated failures should be treated as a potential account compromise event.
