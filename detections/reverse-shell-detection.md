# Reverse Shell Detection

## Detection Summary

This detection identifies potential reverse shell connections initiated from monitored endpoints to attacker-controlled infrastructure inside the lab network.

Reverse shells allow attackers to maintain interactive command execution access after initial compromise.

---

## Detection Source

Tool:

Suricata IDS

Telemetry Used:

TCP connection monitoring  
Shell execution indicators  
Outbound traffic inspection

Rule File:

reverse-shell.rules

---

## Detection Logic

Alert triggers when monitored endpoints establish suspicious outbound connections consistent with reverse shell behavior toward the attacker VM.

Reverse shells commonly use outbound connections to bypass inbound firewall restrictions.

---

## MITRE ATT&CK Mapping

Technique:

T1059.004 — Unix Shell

---

## Investigation Steps

SOC analyst workflow:

1. Identify affected endpoint
2. Confirm destination IP address
3. Review process execution logs
4. Correlate authentication activity timeline
5. Inspect network session metadata

---

## Possible False Positives

Administrative remote sessions  
Automation tooling  
Security testing activity inside lab environment

---

## Response Actions

Recommended containment steps:

- Block attacker IP address
- Terminate active shell sessions
- Isolate affected endpoint if required
- Review additional lateral movement indicators
