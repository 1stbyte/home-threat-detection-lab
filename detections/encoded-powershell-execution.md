# Encoded PowerShell Execution Detection

## Detection Summary

This detection identifies suspicious PowerShell execution using encoded command arguments commonly associated with attacker payload obfuscation.

Encoded PowerShell commands are frequently used to bypass detection controls during post-exploitation activity.

---

## Detection Source

Tool:

Wazuh Custom Detection Rule

Telemetry Used:

Process execution logs  
Command-line arguments  
Windows event telemetry

Rule File:

powershell-encoded-command.xml

---

## Detection Logic

Alert triggers when PowerShell executes with encoded command parameters such as:

powershell.exe -enc  
powershell.exe -EncodedCommand

These execution patterns are commonly used to hide attacker script activity.

---

## MITRE ATT&CK Mapping

Technique:

T1059.001 — PowerShell  
T1027 — Obfuscated Files or Information

---

## Investigation Steps

SOC analyst workflow:

1. Identify executing user account
2. Review parent process relationships
3. Inspect decoded command contents if available
4. Check timeline correlation with authentication activity
5. Review Suricata network telemetry for outbound connections

---

## Possible False Positives

Administrative automation scripts  
Software deployment tools  
Configuration management platforms

---

## Response Actions

Recommended containment steps:

- Investigate script origin
- Validate user activity
- Terminate suspicious processes if necessary
- Escalate if additional attacker behavior observed
