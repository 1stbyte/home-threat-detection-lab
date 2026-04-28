# Incident Investigation Case Report

This report documents a simulated attacker intrusion scenario inside the **Home Threat Detection & Incident Response Lab** environment.

The investigation demonstrates how endpoint telemetry, network alerts, and custom detection engineering rules correlate to identify attacker behavior across the monitoring pipeline.

---

# Investigation Objective

The objective of this investigation was to simulate a multi-stage attacker intrusion inside an isolated monitoring environment and validate detection coverage across endpoint telemetry and network IDS visibility layers.

The scenario tests whether reconnaissance activity, authentication attacks, execution techniques, and credential access behavior can be detected and correlated across multiple security monitoring tools.

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

Wazuh (Endpoint telemetry + rule engine)  
Suricata (Network IDS)  
Elastic Stack (Log ingestion + dashboards)  
pfSense (Network segmentation firewall)

---

# Attack Scenario

A simulated attacker operating from the Kali Linux VM performed reconnaissance and authentication attacks against monitored endpoints inside the isolated lab environment.

The objective of the simulation was to validate detection visibility across both endpoint and network telemetry sources and confirm that layered monitoring controls successfully identified attacker techniques across multiple intrusion phases.

---

# Detection Timeline

## Phase 1 — Network Reconnaissance

Suricata detected port scanning behavior originating from the attacker VM.

Detection Source:

Suricata IDS Alert

Indicators Observed:

Rapid sequential connection attempts  
Multiple destination ports scanned  
Short time interval between probes

MITRE ATT&CK Technique:

T1046 — Network Service Discovery

---

## Phase 2 — Brute Force Authentication Attempts

Multiple failed login attempts were observed targeting endpoint user accounts.

Detection Source:

Windows Security Logs  
Wazuh Authentication Alerts

Indicators Observed:

Repeated Windows Event ID 4625 failures  
Single source IP targeting multiple accounts  
Elevated authentication failure frequency

MITRE ATT&CK Technique:

T1110 — Brute Force

Response Action:

Attacker IP automatically blocked using Wazuh Active Response

---

## Phase 3 — Suspicious PowerShell Execution

Encoded PowerShell execution was detected indicating possible attacker payload execution activity.

Detection Source:

Custom Wazuh Detection Rule

Rule:

powershell-encoded-command.xml

Indicators Observed:

powershell.exe -enc usage  
Encoded command-line arguments  
Suspicious parent-child process relationship

MITRE ATT&CK Techniques:

T1059.001 — PowerShell  
T1027 — Obfuscated Files or Information

---

## Phase 4 — Credential Access Attempt

Suspicious access attempts to LSASS memory were detected indicating potential credential harvesting activity.

Detection Source:

Custom Wazuh Detection Rule

Rule:

lsass-access-non-system.xml

Indicators Observed:

Unauthorized process requesting LSASS memory access  
Suspicious access permission flags  
Credential dumping behavior indicators

MITRE ATT&CK Technique:

T1003.001 — LSASS Credential Dumping

Response Action:

Endpoint investigated  
Credential reset recommended as precautionary containment step

---

## Phase 5 — Automated Containment Action

Repeated authentication failures triggered automated containment using Wazuh Active Response.

Response Action:

Firewall IP block initiated automatically

Detection Source:

auto-block-bruteforce.xml

MITRE ATT&CK Technique:

T1110 — Brute Force

---

## Phase 6 — DNS Tunneling Simulation

Suspicious DNS queries containing long encoded subdomain labels were detected during network monitoring.

Detection Source:

Suricata IDS

Indicators Observed:

High-frequency DNS queries  
Unusually long subdomain structures  
Encoded query behavior consistent with covert channels

MITRE ATT&CK Technique:

T1048.003 — Exfiltration Over Alternative Protocol

Response Action:

DNS traffic reviewed and correlated with endpoint telemetry

---

## Phase 7 — Reverse Shell Activity

Outbound connection behavior consistent with reverse shell activity was detected originating from a monitored endpoint.

Detection Source:

Suricata IDS

Indicators Observed:

Unexpected outbound connection to attacker VM  
Shell execution behavior detected  
Persistent interactive session indicators

MITRE ATT&CK Technique:

T1059.004 — Unix Shell

Response Action:

Connection terminated  
Endpoint isolated for investigation

---

# Detection Correlation Analysis

Detection coverage was achieved using layered telemetry sources across the monitoring pipeline.

Correlation workflow:

Suricata detected reconnaissance activity originating from the attacker system

Windows Security Logs identified authentication failures associated with brute-force attempts

Wazuh custom detection rules identified encoded PowerShell execution behavior

Wazuh credential access detection identified suspicious LSASS memory interaction attempts

Active Response automation triggered containment actions following authentication attack thresholds

Suricata detected reverse shell activity and DNS tunneling simulation behavior

This demonstrates how endpoint telemetry and network IDS alerts complement each other during attacker activity investigation.

---

# Investigation Outcome

The simulated attacker activity was successfully detected across multiple telemetry layers inside the monitoring environment.

Detection coverage confirmed visibility into:

Network reconnaissance activity

Authentication attack behavior

Encoded command execution techniques

Credential access attempts targeting LSASS memory

Reverse shell command execution behavior

DNS tunneling simulation indicators

Automated containment using Active Response controls

This investigation demonstrates how layered detection engineering techniques improve SOC visibility into attacker behavior across the intrusion lifecycle.

The scenario validates that endpoint telemetry, network IDS alerts, and automated response workflows can be correlated to identify and contain attacker activity in a simulated enterprise monitoring environment.
