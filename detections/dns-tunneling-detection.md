# DNS Tunneling Detection

## Detection Summary

This detection identifies suspicious DNS queries containing unusually long subdomain labels that may indicate covert data exfiltration activity.

DNS tunneling is commonly used by attackers to bypass traditional network filtering controls.

---

## Detection Source

Tool:

Suricata IDS

Telemetry Used:

DNS query inspection  
Network traffic monitoring  
Subdomain length analysis

Rule File:

dns-tunneling.rules

---

## Detection Logic

Alert triggers when DNS queries contain unusually long encoded subdomain labels consistent with tunneling behavior.

Repeated long DNS queries from a single source host indicate possible covert communication channels.

---

## MITRE ATT&CK Mapping

Technique:

T1048.003 — Exfiltration Over Unencrypted/Obfuscated Non-C2 Protocol

---

## Investigation Steps

SOC analyst workflow:

1. Identify source host generating DNS queries
2. Review frequency of DNS requests
3. Inspect queried domain structure
4. Correlate endpoint activity with Wazuh alerts
5. Monitor outbound traffic behavior

---

## Possible False Positives

Content delivery networks  
Telemetry-heavy applications  
Security software update services

---

## Response Actions

Recommended containment steps:

- Block suspicious DNS domains
- Investigate endpoint generating traffic
- Monitor outbound communications
- Escalate if additional exfiltration indicators observed
