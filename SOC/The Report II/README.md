# The Report II – SOC Investigation

## Overview

The **The Report II** challenge from **Blue Team Labs Online (BTLO)** is an extension of the original *The Report* challenge.

The objective is to study the MITRE report **“11 Strategies of a World-Class Cybersecurity Operations Center”** and extract useful concepts, recommendations, organizational models, workflows, and technologies that can be applied to improve a newly established Security Operations Center (SOC).

The investigation covers SOC fundamentals, situational awareness, organizational structures, incident response, virtual SOC operations, Cyber Threat Intelligence (CTI), data sources, forensic support, threat intelligence concepts, and Red Teaming.

---

# Scenario

A newly established SOC is undergoing an improvement process and requires guidance to become a fully functional and mature security operations capability.

As part of the SOC improvement process, the analyst was assigned to study a report released by **MITRE** and identify useful outcomes that could be applied to SOC operations.

The investigation focused on answering questions related to:

* SOC responsibilities
* SOC organizational models
* Incident response workflows
* Situational awareness
* Virtual SOC operations
* Incident prioritization
* Mobile investigations
* Cyber Threat Intelligence
* Security data sources
* EDR retention
* Threat intelligence indicators
* Red Teaming and adversary emulation

---

# Reference

## MITRE Report

**11 Strategies of a World-Class Cybersecurity Operations Center**

**Official MITRE PDF:**

[MITRE – 11 Strategies of a World-Class Cybersecurity Operations Center](https://www.mitre.org/sites/default/files/2022-04/11-strategies-of-a-world-class-cybersecurity-operations-center.pdf?utm_source=chatgpt.com)

This report was the primary source used to answer the challenge questions.

---

# Investigation Process

---

## Stage 1 – SOC Entities and Responsibilities

The report explains that a SOC is distinct from several other entities within an organization.

A **NOC (Network Operations Center)** is primarily concerned with operating and maintaining network and other IT equipment.

A **SOC (Security Operations Center)** is primarily concerned with cyber attack monitoring, incident detection, and response.

An **ISCM (Information Security Continuous Monitoring)** program is generally focused on security compliance and risk measurement.

### Findings

| Entity   | Responsibility                                     |
| -------- | -------------------------------------------------- |
| **NOC**  | Operating and maintaining network and IT equipment |
| **SOC**  | Incident detection and response                    |
| **ISCM** | Security compliance and risk measurement           |

### Challenge Answer

`NOC, SOC, ISCM`

---

# Stage 2 – Basic SOC Workflow

The report presents a **Basic SOC Workflow** describing how a SOC handles security events and incidents.

After investigation and decision making, the SOC can select from four response options:

* **Block Activity**
* **Deactivate Account**
* **Continue Watching**
* **Refer to Outside Party**

These options provide different response paths depending on the investigation results and operational requirements.

### Challenge Answer

`Block Activity, Deactivate Account, Continue Watching, Refer to Outside Party`

---

# Stage 3 – Situational Awareness

Situational Awareness (SA) is an important capability for an effective SOC.

The report explains that the SOC needs to understand, maintain, and share situational awareness regarding its environment, threats, assets, risks, and security posture.

The report states that SOC situational awareness follows the:

**Observe → Orient → Decide → Act**

cycle.

This is known as the:

### OODA Loop

The OODA Loop is a self-reinforcing situational awareness decision cycle.

### Challenge Answer

`OODA Loop`

---

# Stage 4 – SOC Organizational Models

The report describes several organizational models based on factors such as constituency size, organizational structure, geographic distribution, and SOC maturity.

For a constituency size between **1,000 and 10,000 employees**, the identified organizational model is:

### Distributed SOC

A distributed model allows SOC capabilities and responsibilities to operate across different organizational locations or elements.

### Challenge Answer

`Distributed SOC`

---

# Stage 5 – Large Centralized SOC

The report also describes roles and responsibilities within larger centralized SOC structures.

One role is responsible for activities such as:

* Generating SOC metrics
* Maintaining situational awareness
* Conducting internal training
* Conducting external training

### Challenge Finding

**Situational Awareness, Communications, and Training** responsibilities are associated with this role/function within the SOC structure.

---

# Stage 6 – Expanded SOC Operations

The report provides a capability template covering multiple SOC organizational models.

Under the **Expanded SOC Operations** category, the capabilities include:

* Attack Simulation and Assessments
* Deception
* Insider Threat

For the **Coordinating & National SOCs** model, the optional capabilities identified in the challenge are:

* **Deception**
* **Insider Threat**

### Challenge Answer

`Deception, Insider Threat`

---

# Stage 7 – Virtual SOC and Remote Work

The report discusses **Virtual SOCs and Work from Home** scenarios.

This became particularly important during widespread events such as the **COVID-19 pandemic**, which forced many SOCs to operate partially or completely remotely.

The report recommends remote-access technologies including virtual consoles.

Two technologies specifically mentioned are:

### Integrated Lights-Out

**iLO**

### Integrated Dell Remote Access Controller

**iDRAC**

These technologies allow remote management of systems and infrastructure.

### Challenge Answer

`iLO, iDRAC`

---

# Stage 8 – Follow-the-Sun SOC Model

A SOC that needs to provide continuous **24/7 operations** can distribute its workload between teams located in different geographic regions and time zones.

This approach allows teams to hand over operational responsibilities between time zones and reduces the need for the same personnel to work night shifts.

The model is known as:

### Follow the Sun

### Challenge Answer

`Follow the Sun`

---

# Stage 9 – Incident Prioritization

The report describes prioritization of different security activities based on their importance and potential impact.

For the activities specified in the challenge:

| Activity                   | Priority   |
| -------------------------- | ---------- |
| Phishing                   | **Medium** |
| Insider Threat             | **High**   |
| Pre-incident Port Scanning | **Low**    |

### Challenge Answer

`Medium, High, Low`

---

# Stage 10 – Mobile Incident Investigation

The report mentions an open-source operating system that can assist with mobile incident investigation and forensic activities.

The operating system identified is:

### Santoku

Santoku is an open-source Linux-based platform designed with security, forensics, and mobile investigation use cases in mind.

### Challenge Answer

`Santoku`

---

# Stage 11 – Cyber Threat Intelligence

Cyber Threat Intelligence (CTI) is an important component of mature SOC operations.

Before selecting a CTI platform or tool, the report recommends considering support for open threat intelligence standards.

The two standards referenced are:

### STIX

**Structured Threat Information Expression**

### TAXII

**Trusted Automated Exchange of Intelligence Information**

These standards facilitate structured threat intelligence representation and automated intelligence exchange.

### Challenge Answer

`STIX, TAXII`

---

# Stage 12 – High-Volume Data Sources

SOC environments can collect extremely large amounts of security telemetry.

Some data sources can consume storage at extremely high rates, with certain sources reaching **terabytes per day**.

The data source identified in the challenge is:

### PCAP

**Packet Capture (PCAP)** provides detailed network traffic information and can generate extremely large datasets.

### Challenge Answer

`PCAP`

---

# Stage 13 – EDR Data Retention

Endpoint Detection and Response (EDR) data can be extremely valuable during forensic investigations.

Historical EDR information allows analysts to investigate activity that occurred before an incident was discovered.

The recommended retention period specified in the challenge is:

### 6 Months

### Challenge Answer

`6`

---

# Stage 14 – Pyramid of Pain

The report discusses threat intelligence concepts including the **Pyramid of Pain**.

The Pyramid of Pain categorizes indicators according to how difficult they are for an adversary to change.

The indicators identified in the challenge are:

| Difficulty      | Indicator    |
| --------------- | ------------ |
| **Trivial**     | Hash Values  |
| **Easy**        | IP Addresses |
| **Challenging** | Tools        |
| **Tough**       | TTPs         |

The concept demonstrates that higher-level behavioral indicators are generally more difficult and costly for adversaries to change.

### Challenge Answer

`Hash Values, IP Addresses, Tools, TTPs`

---

# Stage 15 – Red Teaming

Red Teaming is used to evaluate the defensive capabilities of an organization by simulating adversary behavior.

The report discusses an approach specifically designed to reproduce the behavior and **Tactics, Techniques, and Procedures (TTPs)** of an adversary.

This approach is known as:

### Adversary Emulation

Adversary emulation attempts to replicate realistic adversary behavior so that defensive teams can test detection, investigation, and response capabilities.

### Challenge Answer

`Adversary Emulation`

---

# Challenge Answers Summary

| Question | Answer                                                                                        |
| -------- | --------------------------------------------------------------------------------------------- |
| **Q1**   | `NOC, SOC, ISCM`                                                                              |
| **Q2**   | `Block Activity, Deactivate Account, Continue Watching, Refer to Outside Party`               |
| **Q3**   | `OODA Loop`                                                                                   |
| **Q4**   | `Distributed SOC`                                                                             |
| **Q5**   | Large Centralized SOC role related to **Situational Awareness, Communications, and Training** |
| **Q6**   | `Deception, Insider Threat`                                                                   |
| **Q7**   | `iLO, iDRAC`                                                                                  |
| **Q8**   | `Follow the Sun`                                                                              |
| **Q9**   | `Medium, High, Low`                                                                           |
| **Q10**  | `Santoku`                                                                                     |
| **Q11**  | `STIX, TAXII`                                                                                 |
| **Q12**  | `PCAP`                                                                                        |
| **Q13**  | `6`                                                                                           |
| **Q14**  | `Hash Values, IP Addresses, Tools, TTPs`                                                      |
| **Q15**  | `Adversary Emulation`                                                                         |

---

# Key Findings

* Identified the distinction between **NOC, SOC, and ISCM** responsibilities.
* Identified four response options in the **Basic SOC Workflow**.
* Identified the **OODA Loop** as the SOC situational awareness decision cycle.
* Identified **Distributed SOC** as the applicable organizational model for the specified constituency size.
* Identified **Deception** and **Insider Threat** as optional capabilities for Coordinating & National SOCs.
* Identified **iLO** and **iDRAC** as virtual console technologies for remote SOC operations.
* Identified **Follow the Sun** as a model for distributing 24/7 SOC workload across time zones.
* Identified incident priorities for phishing, insider threat, and pre-incident port scanning.
* Identified **Santoku** as an open-source OS useful for mobile incident investigations.
* Identified **STIX** and **TAXII** as open CTI standards.
* Identified **PCAP** as a high-volume security data source.
* Identified **6 months** as the EDR data retention period relevant to forensic support.
* Identified the four requested levels of the **Pyramid of Pain**.
* Identified **Adversary Emulation** as the Red Teaming approach for mimicking adversary TTPs.

---

# Tools / Sources Used

* **Blue Team Labs Online – The Report II**
* **MITRE – 11 Strategies of a World-Class Cybersecurity Operations Center**
* PDF document analysis
* PDF text search
* SOC workflow analysis
* SOC organizational model analysis
* Cyber Threat Intelligence concepts
* Incident prioritization analysis
* Threat intelligence analysis

---

# Reference

### Official MITRE Report

**11 Strategies of a World-Class Cybersecurity Operations Center**

[Open the official MITRE PDF](https://www.mitre.org/sites/default/files/2022-04/11-strategies-of-a-world-class-cybersecurity-operations-center.pdf?utm_source=chatgpt.com)

---

# Skills Demonstrated

* SOC Architecture Analysis
* SOC Organizational Model Analysis
* Incident Response
* Incident Prioritization
* Situational Awareness
* OODA Loop Analysis
* Cyber Threat Intelligence
* STIX / TAXII
* Threat Intelligence Analysis
* Pyramid of Pain
* EDR Analysis and Retention
* Digital Forensics Concepts
* Mobile Forensics
* Virtual SOC Operations
* Remote SOC Architecture
* Red Teaming
* Adversary Emulation
* MITRE Framework Analysis
* Security Operations Center Fundamentals
