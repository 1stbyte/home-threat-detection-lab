# Brute Force Authentication Detection

## Detection Summary

This detection identifies repeated failed authentication attempts originating from a single source system inside the monitored lab network.

Such activity commonly indicates password spraying or brute-force credential guessing behavior.

---

## Detection Source

Tool:

Wazuh + Windows Security Logs

Telemetry Used:

Windows Event ID 4625  
Authentication failure alerts  
Source IP correlation

---

## Detection Logic

Alert triggers when multiple failed authentication attempts occur within a short time window from the same source IP address.

Repeated authentication failures against one or more user accounts indicate possible credential access attempts.

---

## MITRE ATT&CK Mapping

Technique:

T1110 — Brute Force

---

## Investigation Steps

SOC analyst workflow:

1. Identify source IP address generating failed login attempts
2. Identify targeted accounts
3. Determine whether authentication attempts succeeded
4. Review login timing patterns
5. Correlate activity with Suricata network telemetry

---

## Possible False Positives

User password typing mistakes  
Expired credentials  
Automated service authentication failures

---

## Response Actions

Recommended containment steps:

- Block attacker IP using Wazuh Active Response
- Reset affected credentials
- Monitor authentication attempts across additional endpoints
