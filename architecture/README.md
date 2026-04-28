# Lab Topology Overview

The Home Threat Detection & Incident Response Lab simulates a small SOC-monitored enterprise environment designed to demonstrate layered threat detection across endpoint telemetry and network intrusion detection systems.

The environment operates inside an isolated subnet to safely simulate attacker activity while maintaining full monitoring visibility across the detection pipeline.

---

# Network Architecture

Lab Network Range:

10.0.50.0/24

This isolated subnet contains:

Attacker infrastructure  
Monitored endpoints  
Firewall segmentation controls  
Endpoint detection platform  
Network intrusion detection system  
Centralized logging pipeline  
Analyst investigation workstation  

Telemetry flows from endpoints and network sensors into a centralized Elastic Stack monitoring platform for investigation and alert correlation.

---

# Attacker VM

System:

Kali Linux  
IP Address:

10.0.50.10

Purpose:

Simulates adversary activity inside the lab network.

Simulated attacker behaviors include:

Nmap scanning  
Brute-force authentication attempts  
Encoded PowerShell execution  
Credential access attempts (LSASS interaction)  
Reverse shell activity  
DNS tunneling simulation  

These activities generate detection telemetry across both endpoint and network monitoring layers.

---

# Network Segmentation Firewall

System:

pfSense Firewall  
IP Address:

10.0.50.1

Purpose:

Controls traffic routing between attacker infrastructure and monitored endpoints while maintaining isolation inside the lab environment.

Responsibilities include:

Traffic inspection  
Network segmentation  
Controlled attack simulation boundary enforcement  

pfSense ensures attacker activity remains contained within the lab subnet.

---

# Monitored Endpoints

Systems:

Windows 10 VM — 10.0.50.20  
Ubuntu 22.04 VM — 10.0.50.30  

Installed Component:

Wazuh Agent

Purpose:

Endpoints generate telemetry used to detect attacker behavior across authentication activity, command execution, and credential access attempts.

Collected telemetry includes:

Authentication logs  
Process execution activity  
Command-line arguments  
Credential access indicators  
Security-relevant system behavior  

These endpoints simulate monitored enterprise workstations.

---

# Network Intrusion Detection Layer

System:

Suricata IDS  
IP Address:

10.0.50.50

Purpose:

Suricata monitors network traffic for attacker behavior occurring between the Kali attacker system and monitored endpoints.

Detection coverage includes:

Port scanning activity  
Reverse shell connections  
DNS tunneling behavior  
Suspicious outbound traffic patterns  

Suricata provides network-layer detection visibility complementary to endpoint telemetry.

---

# Endpoint Detection Platform

System:

Wazuh Manager  
IP Address:

10.0.50.40

Purpose:

Collects endpoint telemetry and applies custom detection engineering rules to identify attacker behavior across monitored hosts.

Detection coverage includes:

Encoded PowerShell execution  
Authentication attack patterns  
Credential dumping attempts  
Suspicious process execution  

Wazuh Active Response enables automated containment actions.

Example:

Automatic firewall blocking after repeated authentication failures

---

# Centralized Security Analytics Pipeline

Elastic Stack Components:

Elasticsearch — 10.0.50.60  
Logstash — 10.0.50.61  
Kibana — 10.0.50.62  

Purpose:

Centralizes alerts and telemetry from Wazuh and Suricata into a unified investigation platform.

Elastic Stack enables:

Log ingestion  
Security event correlation  
Threat hunting workflows  
Timeline reconstruction  
Dashboard visualization  

Kibana serves as the primary SOC analyst investigation interface.

---

# Analyst Workstation

System:

Security Analyst Workstation  
IP Address:

10.0.50.100

Purpose:

Used to investigate alerts generated across the monitoring environment.

Typical analyst workflows include:

Alert triage  
Log correlation  
Threat hunting  
Incident response validation  
Detection engineering testing  

This workstation simulates a SOC analyst investigation environment.

---

# Detection Visibility Pipeline

Security telemetry flows through the monitoring stack as follows:

Endpoints forward telemetry to Wazuh Manager

Network traffic is inspected by Suricata IDS

Alerts and logs are forwarded into Elastic Stack

Kibana dashboards support analyst investigation workflows

Wazuh Active Response performs automated containment when thresholds are triggered

This layered monitoring architecture mirrors real-world SOC detection pipelines used in enterprise security operations environments.
