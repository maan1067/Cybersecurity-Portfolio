# Introduction to SOAR

## Overview

SOAR stands for **Security Orchestration, Automation, and Response**.

It is a security platform designed to automate repetitive security tasks, orchestrate security tools, and improve incident response efficiency.

SOAR helps SOC analysts reduce investigation time and respond to threats faster by automating common workflows.

---

# Learning Objectives

After completing this room, I was able to:

- Understand what SOAR is.
- Differentiate between SIEM and SOAR.
- Understand Security Orchestration.
- Understand Security Automation.
- Understand Incident Response Playbooks.
- Learn how SOAR platforms improve SOC efficiency.

---

# What is SOAR?

SOAR is a platform that combines three security capabilities:

- Security Orchestration
- Security Automation
- Incident Response

Its goal is to reduce manual work for SOC analysts.

---

# Components of SOAR

## 1. Security Orchestration

Orchestration connects different security tools together.

Examples:

- SIEM
- Firewall
- EDR
- Threat Intelligence Platforms
- Email Security
- Endpoint Protection

Instead of working separately, all tools communicate through SOAR.

---

## 2. Security Automation

Automation performs repetitive tasks without human intervention.

Examples include:

- Enriching IOCs
- Blocking malicious IP addresses
- Isolating compromised endpoints
- Sending notifications
- Creating incident tickets
- Running malware analysis automatically

---

## 3. Incident Response

SOAR executes predefined response workflows called **Playbooks**.

Examples:

- Phishing response
- Malware response
- Insider threat investigation
- Ransomware containment
- Data exfiltration investigation

---

# What is a Playbook?

A Playbook is a predefined sequence of automated actions executed after a security alert.

Example:

Alert Generated

↓

Extract IOC

↓

Query VirusTotal

↓

Check Threat Intelligence

↓

Block IP

↓

Isolate Host

↓

Notify SOC Analyst

↓

Create Incident Ticket

---

# SOAR Workflow

```
Alert

↓

SIEM

↓

SOAR

↓

Automation

↓

Investigation

↓

Response
```

---

# SIEM vs SOAR

| SIEM | SOAR |
|------|------|
| Collects Logs | Automates Response |
| Detects Alerts | Executes Actions |
| Correlates Events | Runs Playbooks |
| Investigation | Incident Response |
| Monitoring | Automation |

---

# Benefits of SOAR

- Faster Incident Response
- Reduced Manual Work
- Improved Detection
- Standardized Workflows
- Better Collaboration
- Lower Mean Time To Respond (MTTR)
- Reduced Analyst Fatigue

---

# Common SOAR Platforms

- Cortex XSOAR
- Splunk SOAR (Phantom)
- IBM QRadar SOAR
- Microsoft Sentinel Automation
- Tines
- Swimlane

---

# Example Use Case

Scenario:

A phishing email reaches an employee.

Without SOAR:

- Analyst investigates manually.
- Checks VirusTotal.
- Extracts IOC.
- Blocks sender.
- Creates ticket.

Time:
20–40 minutes.

With SOAR:

- IOC extracted automatically.
- VirusTotal lookup.
- Sandbox analysis.
- Email quarantine.
- Endpoint isolation.
- Ticket creation.
- Analyst reviews only the final result.

Time:
1–3 minutes.

---

# Skills Gained

- SOAR Fundamentals
- Security Automation
- Incident Response
- Playbook Design
- Security Orchestration
- Threat Intelligence Integration
- SOC Automation Concepts

---

# Key Takeaways

- Learned the purpose of SOAR.
- Understood how SOAR differs from SIEM.
- Explored orchestration and automation concepts.
- Learned how playbooks improve incident response.
- Understood how SOAR reduces SOC workload and accelerates investigations.
