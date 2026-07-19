
# MITRE ATT&CK Framework

## Overview

This room introduces the **MITRE ATT&CK Framework**, one of the most important knowledge bases used by SOC Analysts, Threat Hunters, Incident Responders, Red Teams, and Blue Teams.

Unlike traditional security models, ATT&CK documents **real-world attacker behaviors (TTPs)** based on actual cyber intrusions.

Throughout this room, I explored how attackers operate, how defenders map attacks to ATT&CK techniques, and how additional MITRE projects such as **CAR**, **D3FEND**, **AADAPT**, **ATLAS**, and **CALDERA** improve detection and defensive capabilities.

---

# Learning Objectives

* Understand MITRE ATT&CK Framework
* Learn the difference between Tactics, Techniques and Procedures (TTPs)
* Explore ATT&CK Matrix
* Investigate Threat Actors using ATT&CK
* Learn Threat Intelligence mapping
* Understand MITRE CAR
* Learn MITRE D3FEND
* Explore other MITRE projects

---

# What is MITRE ATT&CK?

MITRE ATT&CK is a public knowledge base that documents attacker behavior based on real-world observations.

It provides defenders with a common language for describing attacks.

Instead of asking:

> "What malware was used?"

Security teams ask:

> "What technique was used?"

This makes detection independent from malware names.

---

# TTP Model

ATT&CK is based on **Tactics, Techniques and Procedures (TTPs).**

| Component | Description                                     |
| --------- | ----------------------------------------------- |
| Tactic    | Why the attacker performs an action             |
| Technique | How the attacker achieves the goal              |
| Procedure | The exact implementation used by a threat actor |

Example:

Initial Access → Phishing → Spearphishing Attachment

---

# ATT&CK Matrix

The ATT&CK Matrix organizes attacker behavior into tactical phases.

Examples include:

* Reconnaissance
* Resource Development
* Initial Access
* Execution
* Persistence
* Privilege Escalation
* Defense Evasion
* Credential Access
* Discovery
* Lateral Movement
* Collection
* Command & Control
* Exfiltration
* Impact

Each technique has:

* Technique ID
* Description
* Detection methods
* Mitigations
* Threat Groups using it
* Related software

---

# Threat Intelligence

ATT&CK allows analysts to map adversary behavior.

Example:

Threat Group:

**Mustang Panda (G0129)**

Known for:

* Phishing
* Defense Evasion
* Scheduled Tasks
* Cobalt Strike
* Access Token Manipulation

Instead of only knowing **who attacked**, analysts understand:

* How they attack
* Which techniques they prefer
* How to detect them
* How to mitigate future attacks

---

# ATT&CK Navigator

One of the most useful MITRE tools.

It allows analysts to:

* Highlight techniques
* Build Detection Coverage
* Compare Threat Groups
* Create Heat Maps
* Measure Security Maturity

Very useful for:

* SOC Teams
* Threat Hunters
* Detection Engineers
* Purple Teams

---

# MITRE CAR (Cyber Analytics Repository)

CAR provides ready-made analytics that help defenders detect ATT&CK techniques.

Each analytic includes:

* ATT&CK mapping
* Detection logic
* Splunk examples
* Pseudocode
* LogPoint implementations

Purpose:

Convert ATT&CK knowledge into real SIEM detections.

---

# MITRE D3FEND

ATT&CK explains:

> **How attackers attack**

D3FEND explains:

> **How defenders stop them**

Examples:

* Credential Rotation
* User Behavior Analysis
* Network Monitoring
* Traffic Inspection
* Artifact Analysis

D3FEND maps defensive techniques directly against ATT&CK techniques.

---

# Other MITRE Projects

## CALDERA

Automated adversary emulation platform.

Used for:

* Purple Teaming
* Detection Validation
* Red Team Automation

---

## ATT&CK Emulation Plans

Provides step-by-step attack simulations based on real APT groups.

Useful for:

* Blue Team exercises
* Threat Hunting labs
* Detection engineering

---

## AADAPT

Framework dedicated to attacks targeting:

* Blockchain
* Cryptocurrency
* Digital Wallets
* Smart Contracts

---

## ATLAS

Framework focused on AI Security.

Covers attacks against:

* Machine Learning
* LLMs
* AI Models
* Prompt Injection
* Prompt Obfuscation

---

# Key Concepts Learned

* ATT&CK is based on attacker behavior rather than malware.
* Every technique has a unique ID.
* Threat Intelligence becomes actionable by mapping attacks to ATT&CK.
* ATT&CK improves SOC investigations.
* CAR translates ATT&CK into SIEM detection logic.
* D3FEND maps defensive techniques.
* CALDERA enables adversary emulation.
* ATLAS focuses on AI threats.
* AADAPT focuses on blockchain security.

---

# Room Answers

| Question                           | Answer                                  |
| ---------------------------------- | --------------------------------------- |
| Hide Artifacts Tactic              | Defense Evasion                         |
| Create Account Technique ID        | T1136                                   |
| Mustang Panda Country              | China                                   |
| Recon Technique ID                 | T1598                                   |
| Access Token Manipulation Software | Cobalt Strike                           |
| Aviation Threat Group              | APT33                                   |
| Office 365 Sub-technique           | Cloud Accounts                          |
| Related Tool                       | Ruler                                   |
| Mitigation                         | User Account Management                 |
| Detection Strategy                 | DET0546                                 |
| CAR-2019-07-001 Tactic             | Defense Evasion                         |
| Analytic Type                      | Situational Awareness                   |
| D3FEND Sub-technique               | User Geolocation Logon Pattern Analysis |
| Digital Artifact                   | Network Traffic                         |
| AADAPT Technique ID                | ADT3025                                 |
| ATLAS Tactic                       | Defense Evasion                         |

---

# Why This Room Matters

As a SOC Analyst, understanding MITRE ATT&CK is essential because almost every modern SIEM, EDR, XDR, SOAR, and Threat Intelligence platform maps alerts to ATT&CK techniques. Instead of only identifying malware, analysts focus on attacker behaviors, enabling stronger detection, better incident response, and improved threat hunting.

---

## Skills Gained

* MITRE ATT&CK
* Threat Intelligence
* Threat Actor Profiling
* ATT&CK Navigator
* Detection Engineering
* CAR Analytics
* D3FEND
* Threat Hunting
* SOC Analysis
* Blue Team Fundamentals

