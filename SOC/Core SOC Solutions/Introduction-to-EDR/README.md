# Introduction to Endpoint Detection and Response (EDR)

## Overview

Endpoint Detection and Response (EDR) is a security solution designed to monitor endpoint activity, detect malicious behavior, investigate security incidents, and provide automated or manual response capabilities. Unlike traditional antivirus software, EDR continuously collects endpoint telemetry and analyzes behavioral patterns to identify advanced threats that may bypass signature-based detection.

This lab introduces the core concepts of EDR, explains its architecture, and demonstrates how SOC analysts use EDR platforms to investigate and respond to endpoint security incidents.

---

## Learning Objectives

By completing this lab, I was able to:

- Understand the purpose of Endpoint Detection and Response (EDR).
- Differentiate between Antivirus (AV) and EDR solutions.
- Learn how endpoint telemetry is collected and analyzed.
- Explore the EDR detection and response workflow.
- Understand how SOC analysts investigate endpoint alerts using EDR platforms.

---

# What is an Endpoint?

An endpoint is any device connected to a network that can communicate with other systems.

Common examples include:

- Desktop Computers
- Laptops
- Windows Servers
- Linux Servers
- Mobile Devices
- Virtual Machines

Endpoints are common targets for attackers because they often store sensitive information and provide access to enterprise resources.

---

# What is EDR?

Endpoint Detection and Response (EDR) is an advanced endpoint security solution that continuously monitors endpoint activity, detects suspicious behavior, collects forensic evidence, and enables rapid incident response.

Instead of relying only on malware signatures, EDR focuses on behavioral analysis to identify attacks in real time.

---

# Why Organizations Need EDR

Traditional antivirus solutions primarily detect known malware using signature databases.

Modern attackers often use:

- PowerShell
- Command Prompt
- WMI
- Living-off-the-Land Binaries (LOLBins)
- Credential Theft
- Fileless Malware

These techniques may evade traditional antivirus products.

EDR addresses this challenge by monitoring endpoint behavior and identifying suspicious activities instead of relying solely on malware signatures.

---

# Core Components of an EDR Solution

## Endpoint Agent

A lightweight software agent installed on every endpoint.

Responsibilities include:

- Collecting telemetry
- Monitoring processes
- Tracking file activity
- Recording network connections
- Sending logs to the management server

---

## Management Console

The centralized platform where analysts monitor alerts, investigate incidents, and manage endpoints.

---

## Detection Engine

Analyzes collected telemetry using:

- Behavioral Analytics
- Detection Rules
- Threat Intelligence
- Machine Learning (in some solutions)

---

## Response Engine

Allows analysts or automated playbooks to respond to threats.

Common response actions include:

- Kill Process
- Isolate Host
- Delete Malicious File
- Block Hash
- Block IP Address
- Quarantine Endpoint

---

# Endpoint Telemetry

Telemetry refers to the continuous stream of security-related data collected from endpoints.

Examples include:

- Running Processes
- Process Creation Events
- Parent and Child Processes
- Registry Changes
- File Modifications
- User Logins
- Network Connections
- Command-Line Arguments
- Scheduled Tasks

Telemetry provides analysts with the visibility required for threat hunting and incident investigations.

---

# Detection Workflow

A typical EDR detection process follows these steps:

1. Endpoint activity is continuously monitored.
2. Telemetry is collected by the endpoint agent.
3. Detection rules analyze the collected data.
4. Suspicious activity triggers an alert.
5. The SOC analyst investigates the alert.
6. Appropriate response actions are taken.
7. Incident documentation is completed.

---

# Example Attack Scenario

An attacker sends a phishing email containing a malicious Microsoft Word document.

The user opens the document.

The document launches:

Word → PowerShell → Command Prompt → Malicious Payload

The EDR detects:

- Suspicious process chain
- PowerShell execution
- External network communication
- Malware download

The SOC analyst investigates the alert and isolates the compromised endpoint before the malware spreads.

---

# EDR vs Traditional Antivirus

| Traditional Antivirus | EDR |
|----------------------|-----|
| Signature-based detection | Behavioral detection |
| Detects known malware | Detects known and unknown threats |
| Limited visibility | Full endpoint visibility |
| Basic protection | Detection, Investigation, and Response |
| Minimal forensic data | Rich forensic telemetry |

---

# Popular EDR Solutions

Some of the most widely used EDR platforms include:

- Microsoft Defender for Endpoint
- CrowdStrike Falcon
- SentinelOne
- VMware Carbon Black
- Cortex XDR
- Sophos Intercept X

---

# SOC Analyst Responsibilities

When investigating an EDR alert, a SOC Analyst may:

- Identify the affected endpoint
- Review running processes
- Analyze parent-child process relationships
- Examine network connections
- Validate Indicators of Compromise (IOCs)
- Determine attack severity
- Perform containment actions
- Escalate incidents if necessary

---

# Skills Demonstrated

- Endpoint Security Fundamentals
- Endpoint Detection and Response (EDR)
- Behavioral Analysis
- Endpoint Telemetry Analysis
- Incident Investigation
- Threat Detection
- IOC Identification
- Security Monitoring
- Incident Response

---

# Key Takeaways

- EDR provides continuous monitoring of endpoint activity.
- Behavioral detection enables identification of advanced threats.
- Endpoint telemetry is essential for investigations.
- EDR platforms support rapid containment and response.
- SOC analysts rely on EDR to investigate endpoint-based attacks.

---

# References

- MITRE ATT&CK Framework
- NIST SP 800-61 Rev.2 – Computer Security Incident Handling Guide
- Microsoft Defender for Endpoint Documentation
- CrowdStrike Falcon Documentation
## Real-World Scenario

### Scenario

An employee receives a phishing email containing a malicious attachment.

### Detection

The EDR platform detects abnormal PowerShell execution initiated by Microsoft Word.

### Investigation

The SOC analyst reviews:
- Process Tree
- Network Connections
- File Hash
- Command Line
- User Activity

### Response

- Isolate the endpoint.
- Terminate malicious processes.
- Block IOCs.
- Document the incident.
