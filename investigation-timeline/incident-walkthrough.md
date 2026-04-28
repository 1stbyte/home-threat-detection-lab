# Incident Investigation Walkthrough

This walkthrough documents a simulated attacker intrusion scenario inside the **Home Threat Detection & Incident Response Lab** environment.

The investigation demonstrates how endpoint telemetry, network alerts, and detection engineering rules correlate to identify attacker behavior across the monitoring pipeline.

---

# Environment Overview

Lab Network:

10.0.50.0/24

Attacker System:

Kali Linux  
10.0.50.10

Monitored Endpoints:

Windows 10 VM  
Ubuntu 22.04 VM

Detection Stack:

- Wazuh (Endpoint telemetry + rule engine)
- Suricata (Network IDS)
- Elastic Stack (Log ingestion + dashboards)
- pfSense (Network segmentation firewall)

---

# Attack Scenario

A simulated attacker operating from the Kali Linux VM performed reconnaissance and authentication attacks against monitored endpoints inside the isolated lab environment.

The objective of the simulation was to validate detection visibility across both endpoint and network telemetry sources.

---

# Detection Timeline

## Phase 1 — Network Reconnaissance

Suricata detected port scanning behavior originating from the attacker VM.

Detection Source:

Suricata IDS Alert

MITRE ATT&CK Technique:

T1046 — Network Service Discovery

---

## Phase 2 — Brute Force Authentication Attempts

Multiple failed login attempts were observed targeting endpoint user accounts.

Detection Source:

Windows Security Logs  
Wazuh Authentication Alerts

MITRE ATT&CK Technique:

T1110 — Brute Force

---

## Phase 3 — Suspicious PowerShell Execution

Encoded PowerShell execution was detected indicating possible attacker payload execution activity.

Detection Source:

Custom Wazuh Detection Rule  
powershell-encoded-command.xml

MITRE ATT&CK Technique:

T1059.001 — PowerShell

---

## Phase 4 — Credential Access Attempt

Suspicious access attempts to LSASS memory were detected indicating potential credential harvesting activity.

Detection Source:

Custom Wazuh Detection Rule  
lsass-access-non-system.xml

MITRE ATT&CK Technique:

T1003.001 — LSASS Credential Dumping

---

## Phase 5 — Containment Action

Repeated authentication failures triggered automated containment using Wazuh Active Response.

Response Action:

Firewall IP block initiated automatically

Detection Source:

auto-block-bruteforce.xml

MITRE ATT&CK Technique:

T1110 — Brute Force

---

# Investigation Outcome

The simulated attack activity was successfully detected across both endpoint and network telemetry layers.

Detection visibility confirmed:

- Network reconnaissance detection
- Authentication attack detection
- PowerShell execution monitoring
- Credential dumping detection
- Automated containment capability

This investigation demonstrates how layered detection engineering techniques improve visibility into attacker behavior inside SOC monitoring environments.
