# Cyber Kill Chain

## Overview

The **Cyber Kill Chain** is a cybersecurity framework developed by **Lockheed Martin** in 2011 to describe the lifecycle of a cyber attack. It helps security teams understand how attackers operate and identify opportunities to detect and stop attacks before they achieve their objectives.

Unlike traditional malware-focused detection, the Cyber Kill Chain provides defenders with visibility into every phase of an intrusion, allowing organizations to implement layered security controls.

---

# Learning Objectives

* Understand the Cyber Kill Chain Framework
* Learn the seven phases of a cyber attack
* Identify attacker activities during each phase
* Understand defensive strategies for every stage
* Recognize the strengths and limitations of the framework

---

# Cyber Kill Chain Phases

| Phase                 | Attacker Goal                  | Defender Goal                            |
| --------------------- | ------------------------------ | ---------------------------------------- |
| Reconnaissance        | Gather target information      | Detect reconnaissance activities         |
| Weaponization         | Build malware and exploits     | Detect malicious payload creation        |
| Delivery              | Deliver malicious payload      | Block malicious delivery methods         |
| Exploitation          | Exploit vulnerabilities        | Prevent successful exploitation          |
| Installation          | Establish persistence          | Detect persistence mechanisms            |
| Command & Control     | Communicate with infected host | Detect outbound malicious communications |
| Actions on Objectives | Achieve attack goals           | Prevent data theft and impact            |

---

# 1. Reconnaissance

### Purpose

The attacker gathers information about the victim before launching the attack.

### Passive Recon

* Google Dorking
* WHOIS
* LinkedIn
* Social Media
* GitHub
* Public Breach Databases

### Active Recon

* Port Scanning
* Banner Grabbing
* Service Enumeration
* Social Engineering

### Common Tools

* theHarvester
* Hunter.io
* Maltego
* Shodan
* Recon-ng
* OSINT Framework

### SOC Detection

* Monitor scanning activity
* Detect unusual DNS requests
* Detect excessive connection attempts
* External threat intelligence

---

# 2. Weaponization

### Purpose

The attacker prepares the payload.

### Examples

* Office Macros
* VBA Scripts
* Backdoors
* Trojans
* Ransomware
* Exploits
* USB Malware

### Malware Components

* Payload
* Exploit
* Dropper
* Loader

### SOC Detection

* Malware Sandbox
* Static Analysis
* YARA Rules
* Antivirus
* Threat Intelligence

---

# 3. Delivery

### Common Delivery Methods

* Phishing Email
* Spear Phishing
* USB Drop
* Watering Hole
* Malicious Websites
* Drive-by Download

### SOC Detection

* Secure Email Gateway
* Web Filtering
* Proxy Logs
* Email Sandboxing

---

# 4. Exploitation

### Purpose

Execute malicious code by exploiting vulnerabilities.

### Examples

* CVEs
* Zero-Day Exploits
* Macro Execution
* Remote Code Execution

### Indicators

* New Processes
* Suspicious Command Line
* Registry Changes
* New Services

### SOC Detection

* Sysmon
* Windows Event Logs
* EDR
* IDS/IPS

---

# 5. Installation

### Purpose

Maintain persistence on the victim.

### Persistence Techniques

* Registry Run Keys
* Startup Folder
* Scheduled Tasks
* Windows Services
* Web Shell
* Backdoor
* Meterpreter

### MITRE ATT&CK

T1543.003

### SOC Detection

* Autoruns
* Sysmon Event IDs
* Registry Monitoring
* File Integrity Monitoring

---

# 6. Command & Control (C2)

### Purpose

Maintain communication between attacker and victim.

### Common C2 Channels

* HTTP
* HTTPS
* DNS Tunneling
* ICMP
* WebSockets

### Indicators

* Beaconing
* Regular DNS Requests
* Suspicious External Connections
* Unknown Domains

### SOC Detection

* Firewall Logs
* DNS Logs
* Proxy Logs
* Zeek
* Suricata
* Splunk
* Elastic SIEM

---

# 7. Actions on Objectives

### Final Goals

* Credential Theft
* Privilege Escalation
* Lateral Movement
* Data Collection
* Data Exfiltration
* Backup Deletion
* Ransomware Encryption
* Data Destruction

### SOC Detection

* UEBA
* DLP
* File Monitoring
* Privileged Access Monitoring
* SIEM Correlation Rules

---

# Advantages

* Easy to understand
* Structured attack lifecycle
* Improves detection planning
* Useful for SOC teams
* Helps map security controls

---

# Limitations

* Focuses mainly on malware attacks
* Does not effectively cover insider threats
* Less effective against modern cloud attacks
* Does not represent every MITRE ATT&CK technique
* Last major update was in 2011

---

# Cyber Kill Chain vs MITRE ATT&CK

| Cyber Kill Chain   | MITRE ATT&CK                       |
| ------------------ | ---------------------------------- |
| 7 attack phases    | Hundreds of techniques             |
| High-level model   | Detailed adversary behaviors       |
| Linear             | Non-linear                         |
| Simple             | Comprehensive                      |
| Good for beginners | Better for advanced threat hunting |

---

# Key Takeaways

* Every cyber attack follows a lifecycle.
* Detecting attacks early reduces damage.
* Reconnaissance is often invisible.
* Persistence enables attackers to return after initial access.
* C2 communication is one of the strongest indicators of compromise.
* Modern SOC teams combine the Cyber Kill Chain with MITRE ATT&CK for comprehensive threat detection.

---

## Skills Gained

* Threat Intelligence
* Threat Hunting
* Incident Response
* SOC Monitoring
* Malware Analysis
* Detection Engineering
* Defensive Security
* Attack Lifecycle Analysis
