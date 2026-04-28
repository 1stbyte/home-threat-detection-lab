# LSASS Credential Access Detection

## Detection Summary

This detection identifies suspicious attempts to access LSASS process memory.

Credential dumping tools commonly interact with LSASS to extract authentication material from memory.

---

## Detection Source

Tool:

Wazuh Custom Detection Rule

Telemetry Used:

Process access events  
Memory access permissions  
Endpoint telemetry logs

Rule File:

lsass-access-non-system.xml

---

## Detection Logic

Alert triggers when processes request elevated access permissions to:

lsass.exe

Suspicious access flags include:

0x1010  
0x1FFFFF

These permissions are frequently associated with credential dumping attempts.

---

## MITRE ATT&CK Mapping

Technique:

T1003.001 — LSASS Credential Dumping

---

## Investigation Steps

SOC analyst workflow:

1. Identify process accessing LSASS
2. Review parent process execution chain
3. Validate legitimacy of requesting application
4. Review authentication activity timeline
5. Correlate network telemetry with Suricata alerts

---

## Possible False Positives

Security tools  
Endpoint protection agents  
Backup software interacting with LSASS

---

## Response Actions

Recommended containment steps:

- Investigate suspicious process origin
- Terminate unauthorized processes
- Reset affected credentials
- Monitor endpoints for lateral movement indicators
