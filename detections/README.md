## Detection Pipeline Example

### Brute Force Authentication Detection

This alert demonstrates detection of repeated authentication failures originating from an attacker-controlled system.  
Wazuh correlated multiple failed login attempts and triggered a high-severity brute force alert mapped to MITRE ATT&CK technique **T1110 – Brute Force**.

The alert includes:

• Source attacker IP address  
• Target username  
• Authentication method (NTLM)  
• Event correlation timeline  
• Alert severity scoring  
• Automatic containment via Active Response firewall blocking

![Brute Force Alert](screenshots/02-bruteforce-alert.png)

Authentication failures detected and automatically blocked using Wazuh Active Response.

Detection logic validated using simulated password spraying activity from the Kali attacker VM inside an isolated lab network.
