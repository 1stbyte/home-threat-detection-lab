# Reverse Shell Response Playbook

## Alert Trigger

This playbook is initiated when a monitored endpoint establishes a connection consistent with reverse shell activity.

Reverse shells allow attackers to maintain interactive command execution access after initial compromise.

---

## Severity

Critical

Severity increases if:

- Connection persists over time
- Endpoint communicates with attacker infrastructure
- Additional attacker techniques appear in timeline
- Multiple endpoints initiate similar connections

---

## Detection Sources

Tools:

Suricata IDS  
Elastic Stack  
Wazuh Endpoint Monitoring

Detection Rule:

reverse-shell.rules

---

## Investigation Steps

SOC analyst workflow:

1. Identify affected endpoint
2. Confirm destination IP address
3. Review active network connections
4. Identify executing process responsible for connection
5. Review authentication activity associated with endpoint
6. Check for persistence mechanisms
7. Correlate activity with DNS telemetry

---

## Containment Actions

Recommended response actions:

- Block attacker IP address
- Terminate reverse shell connection
- Isolate affected endpoint from network
- Reset affected user credentials

---

## Escalation Criteria

Escalate incident if:

- Connection re-establishes after termination
- Additional endpoints affected
- Credential dumping observed
- Data exfiltration suspected

---

## MITRE ATT&CK Mapping

Technique:

T1059.004 — Unix Shell

---

## Analyst Notes

Reverse shell activity is a strong indicator of active attacker control and should be treated as a confirmed compromise event.
