# OpenCTI – Threat Intelligence Investigation

## Overview

This lab focuses on using **OpenCTI (Open Cyber Threat Intelligence Platform)** to investigate, correlate, and visualize cyber threat intelligence.

The investigation covers:

* Threat Actors / Intrusion Sets
* Malware and Tools
* MITRE ATT&CK Attack Patterns
* Campaigns
* Vulnerabilities
* Indicators and Observations
* Relationships between threat intelligence entities
* Incident and event investigation

The main objective was to understand how OpenCTI represents threat intelligence as a connected knowledge graph and how analysts can use these relationships to investigate adversaries, malware, vulnerabilities, and attack techniques.

---

## Scenario

As a SOC / Threat Intelligence analyst, the objective was to investigate multiple threat intelligence entities using OpenCTI.

The investigation required answering questions about:

* Which threat actors use specific malware
* Which attack patterns are associated with adversaries
* Which tools are used during attacks
* Which vulnerabilities were exploited
* How malware, campaigns, and threat actors are related
* How specific attack techniques are represented
* How indicators and observations are organized
* How incident-related events can provide additional context

---

# Investigation Process

## Stage 1 — Understanding OpenCTI

OpenCTI is an open-source Cyber Threat Intelligence platform designed to **store, analyze, correlate, and visualize threat intelligence**.

The platform represents threat intelligence as interconnected entities rather than isolated indicators.

A simplified representation of the platform is:

```text
OpenCTI
   │
   └── STIX 2
        │
        ├── SDO — STIX Domain Objects
        │
        ├── SCO — STIX Cyber-observable Objects
        │
        └── SRO — STIX Relationship Objects
```

This structure allows an analyst to move from one entity to another and understand the relationships between them.

---

## Stage 2 — Understanding the STIX Data Model

OpenCTI uses the **STIX 2** standard to represent cyber threat intelligence.

### SDO — STIX Domain Objects

Used to represent higher-level intelligence entities such as:

* Malware
* Threat Actors
* Intrusion Sets
* Campaigns
* Attack Patterns
* Vulnerabilities

### SCO — STIX Cyber-observable Objects

Represent technical observables such as:

* IP addresses
* Domains
* File hashes
* Network artifacts

### SRO — STIX Relationship Objects

Represent relationships between entities.

For example:

```text
Threat Actor
     │
     ├── uses ──→ Malware
     │
     ├── uses ──→ Tool
     │
     ├── uses ──→ Attack Pattern
     │
     └── exploits ──→ Vulnerability
```

This relationship-based structure is one of the main strengths of OpenCTI.

---

# Stage 3 — OpenCTI Navigation

The investigation required navigating several major areas of the platform.

```text
Dashboard
Activities
Knowledge
Data
Settings
```

The most important sections for the investigation were:

```text
Activities
 ├── Analysis
 ├── Events
 └── Observations

Knowledge
 ├── Threats
 ├── Arsenal
 ├── Entities
 └── Locations
```

One important navigation finding was that **Indicators are located under Activities → Observations**.

---

# Stage 4 — Malware & Threat Group Investigation

## 4.1 — 4H RAT

### Question

Which threat group has used **4H RAT**?

### Investigation

Navigated to:

```text
Knowledge
→ Arsenal
→ Malware
→ Search: 4H RAT
→ Details / Description
```

The malware description states that **4H RAT has been used by Putter Panda since at least 2007**.

### Evidence

```text
4H RAT
   ↓
Used by
   ↓
Putter Panda
```

### Finding

**Putter Panda**

---

# Stage 5 — Attack Pattern Investigation

## 5.1 — Command-Line Interface

### Question

Which kill-chain phase is associated with the **Command-Line Interface** attack pattern?

### Investigation

Navigated to:

```text
Arsenal
→ Attack Patterns
→ Command-Line Interface
→ Details
→ Kill Chain Phases
```

### Evidence

The OpenCTI entity associates the attack pattern with:

```text
execution-ics
```

### Finding

**execution-ics**

> This value represents the kill-chain phase stored in the OpenCTI dataset.

---

# Stage 6 — Indicator Investigation

## 6.1 — Indicators Location

### Question

Which Activities section contains Indicators?

### Investigation

Checked:

```text
Activities
→ Observations
```

### Finding

**Observations**

This is important operationally because technical observables and indicators are investigated from the Observations section rather than the main Knowledge/Arsenal sections.

---

# Stage 7 — Cobalt Strike Relationship Analysis

## 7.1 — Intrusion Sets Associated with Cobalt Strike

### Question

Which intrusion sets are associated with **Cobalt Strike** with **Good confidence**?

### Investigation

Navigated to:

```text
Arsenal
→ Malware
→ Cobalt Strike
→ Knowledge
→ Intrusion Sets
```

The relationships showed two intrusion sets with Good confidence.

### Evidence

```text
Cobalt Strike
   │
   ├── associated with → CopyKittens
   │
   └── associated with → FIN7
```

### Finding

**CopyKittens, FIN7**

---

## 7.2 — Cobalt Strike Author

### Question

Who is listed as the author of the Cobalt Strike entity?

### Investigation

Navigated to:

```text
Cobalt Strike
→ Overview
→ Basic Information
→ Author
```

### Finding

**THE MITRE CORPORATION**

---

# Stage 8 — WhisperGate Investigation

WhisperGate was investigated through its relationship graph to identify associated attack patterns and technical behavior.

---

## 8.1 — Attack Pattern Relationships

### Question

How many attack pattern relationships are associated with WhisperGate?

### Investigation

Navigated to:

```text
WhisperGate
→ Knowledge
→ Distribution of Relations
→ Attack Pattern
```

### Evidence

```text
Attack Pattern Relationships = 28
```

### Finding

**28**

---

## 8.2 — Windows Utility Used to Disable Windows Defender

### Question

Which Windows utility does WhisperGate use to disable Windows Defender?

### Investigation

Navigated to:

```text
WhisperGate
→ Knowledge
→ Attack Patterns
→ InstallUtil
```

The associated description identifies:

```text
InstallUtil.exe
```

### Finding

**InstallUtil.exe**

---

## 8.3 — Native API Used to Shut Down the Host

### Question

Which native API does WhisperGate use to shut down the compromised host?

### Investigation

Navigated to:

```text
WhisperGate
→ Knowledge
→ Attack Patterns
→ System Shutdown/Reboot
```

The description identifies the API:

```text
ExitWindowsEx
```

with the shutdown flag:

```text
EXW_SHUTDOWN
```

### Finding

**ExitWindowsEx**

---

# Stage 9 — Saint Bear Investigation

The Saint Bear intrusion set was investigated to identify malware, tools, and vulnerabilities associated with its activity.

---

## 9.1 — Malware Associated with OutSteel

### Question

Which downloader malware is commonly paired with **OutSteel** in Saint Bear campaigns?

### Investigation

Navigated to:

```text
Saint Bear
→ Knowledge
→ Malware
```

The relationship information identified:

```text
Saint Bot
```

as a .NET downloader used by Saint Bear since at least March 2021.

### Finding

**Saint Bot**

---

## 9.2 — Data Exfiltration Tool

### Question

Which tool did Saint Bear use to exfiltrate data to cloud storage services?

### Investigation

Navigated to:

```text
Saint Bear
→ Knowledge
→ Tools
```

The associated tools included:

```text
Responder
Rclone
PsExec
ngrok
Impacket
CrackMapExec
BloodHound
```

The relevant tool for cloud-storage data exfiltration was:

### Finding

**Rclone**

---

## 9.3 — Microsoft Exchange Vulnerability

### Question

Which Microsoft Exchange vulnerability was exploited by Saint Bear?

### Investigation

Navigated to:

```text
Saint Bear
→ Knowledge
→ Vulnerabilities
```

The listed vulnerabilities included:

```text
CVE-2021-26084
CVE-2022-41040
CVE-2017-11882
```

### Finding

**CVE-2022-41040**

---

# Stage 10 — Campaign Investigation

## 10.1 — Strategic Web Compromise

### Question

Which campaign relies on the **Strategic Web Compromise** attack pattern?

### Investigation

Searched for:

```text
Strategic Web Compromise
```

Then navigated to:

```text
Attack Pattern
→ Knowledge
→ Campaigns
```

The associated campaign was identified as:

### Finding

**th3bug**

---

# Stage 11 — APT37 Intelligence Report

## 11.1 — Malware Entities

### Question

How many distinct malware entities are present in the **APT37 threat intelligence report**?

### Investigation

Searched for:

```text
APT37
```

Then opened the relevant report:

```text
Report
→ Entity Details
→ Entities Distribution
→ Malware
```

### Evidence

```text
Malware Entities = 8
```

### Finding

**8**

This demonstrates how OpenCTI reports can provide a high-level view of the entities referenced by a threat intelligence document.

---

# Stage 12 — Event Investigation

## 12.1 — Exfiltration Alert

### Question

What directory path was targeted in the **Exfiltration Alert** case?

### Investigation

Navigated to:

```text
Events
→ Exfiltration Alert - WebServer-01
→ Description
```

The event description referenced the web server upload directory.

### Evidence

```text
/var/www/html/uploads/
```

The description also provided evidence related to web shell persistence in the targeted location.

### Finding

**/var/www/html/uploads/**

---

# Stage 13 — Andariel Investigation

## 13.1 — Network Connections Discovery

### Question

Which command did Andariel use during Discovery to display TCP connections?

### Investigation

Searched for:

```text
Andariel
```

Then navigated to:

```text
Intrusion Set
→ Knowledge
→ Attack Patterns
→ T1049 System Network Connections Discovery
```

The technique description identified the command:

```text
netstat -naop tcp
```

### Finding

**netstat -naop tcp**

### SOC Relevance

This is particularly useful for detection engineering because network-connection discovery commands can be monitored through:

* Windows process creation telemetry
* EDR
* Sysmon
* SIEM logs
* Command-line auditing

---

# Stage 14 — DCRAT Investigation

## 14.1 — Threat Group Using DCRAT

### Question

Which threat group uses **DCRAT**?

### Investigation

Navigated to:

```text
Arsenal
→ Tools
→ DCRAT
→ Knowledge
→ Intrusion Sets
```

The associated intrusion set was identified.

### Finding

**APT-C-36**

---

# Threat Intelligence Relationship Map

The investigation demonstrated how OpenCTI can connect different intelligence entities.

A simplified representation is:

```text
                 ┌───────────────┐
                 │ Threat Group  │
                 └───────┬───────┘
                         │
          ┌──────────────┼──────────────┐
          │              │              │
         uses         uses          exploits
          │              │              │
          ▼              ▼              ▼
       Malware         Tools       Vulnerability
          │              │
          │              │
          ▼              ▼
    Attack Patterns   Exfiltration
          │
          ▼
       Campaign
```

This relationship model allows an analyst to pivot from a single piece of intelligence into a broader investigation.

For example:

```text
Malware
  ↓
Intrusion Set
  ↓
Attack Patterns
  ↓
Tools
  ↓
Campaigns
  ↓
Vulnerabilities
  ↓
Indicators
```

---

# Indicators of Compromise & Intelligence Findings

| Category                             | Finding                  |
| ------------------------------------ | ------------------------ |
| Malware                              | 4H RAT                   |
| Threat Group                         | Putter Panda             |
| Malware                              | Cobalt Strike            |
| Intrusion Sets                       | CopyKittens, FIN7        |
| Cobalt Strike Author                 | THE MITRE CORPORATION    |
| WhisperGate Attack Pattern Relations | 28                       |
| WhisperGate Utility                  | InstallUtil.exe          |
| WhisperGate Native API               | ExitWindowsEx            |
| Saint Bear Downloader                | Saint Bot                |
| Saint Bear Exfiltration Tool         | Rclone                   |
| Saint Bear Vulnerability             | CVE-2022-41040           |
| Campaign                             | th3bug                   |
| APT37 Malware Entities               | 8                        |
| Exfiltration Directory               | `/var/www/html/uploads/` |
| Andariel Discovery Command           | `netstat -naop tcp`      |
| DCRAT Threat Group                   | APT-C-36                 |

---

# MITRE ATT&CK Mapping

The investigation exposed multiple relationships to MITRE ATT&CK concepts.

| Activity               | Technique / Concept                  | Evidence                 |
| ---------------------- | ------------------------------------ | ------------------------ |
| Command-Line Interface | Command-line execution concept       | OpenCTI Kill Chain Phase |
| WhisperGate            | InstallUtil                          | `InstallUtil.exe`        |
| WhisperGate            | System Shutdown/Reboot               | `ExitWindowsEx`          |
| Andariel               | System Network Connections Discovery | `netstat -naop tcp`      |
| Saint Bear             | Cloud-storage Exfiltration           | `Rclone`                 |
| Saint Bear             | Vulnerability Exploitation           | `CVE-2022-41040`         |

> The OpenCTI dataset may expose ATT&CK-related information through attack-pattern entities, kill-chain phases, relationships, and descriptions. These fields should be interpreted according to the actual entity and relationship evidence rather than assuming every displayed label is itself an ATT&CK technique.

---

# SOC Analyst Perspective

This lab demonstrates a workflow that is directly applicable to SOC and Threat Intelligence investigations.

Instead of looking at an IOC in isolation:

```text
IOC
 ↓
Context
 ↓
Malware / Tool
 ↓
Threat Actor
 ↓
TTPs
 ↓
Campaign
 ↓
Vulnerability / Infrastructure
 ↓
Detection & Investigation
```

For example, if a SOC analyst discovers a suspicious malware sample, OpenCTI can help answer:

```text
What is this malware?
        ↓
Who uses it?
        ↓
What tools are associated with the actor?
        ↓
Which TTPs are commonly used?
        ↓
Which vulnerabilities are associated with the activity?
        ↓
Which campaigns are related?
        ↓
What should we hunt for?
```

This transforms raw threat intelligence into actionable investigation context.

---

# Investigation Methodology

The core investigation methodology used throughout the lab was:

```text
Question
   ↓
Search
   ↓
Open Entity
   ↓
Overview / Knowledge
   ↓
Inspect Relationships
   ↓
Read Description / Evidence
   ↓
Validate Finding
   ↓
Document Result
```

This approach avoids guessing and ensures that every finding is tied to an observable piece of intelligence within OpenCTI.

---

# OpenCTI vs MISP

A useful distinction between the two platforms is:

```text
MISP
↓
Events + Indicators + Sharing

OpenCTI
↓
Entities + Relationships + Knowledge Graph
```

MISP is heavily focused on sharing and managing threat intelligence events and indicators, while OpenCTI emphasizes representing relationships between intelligence entities and exploring them through a knowledge graph.

Both can therefore play complementary roles in a SOC / CTI environment.

---

# Key Findings

The investigation demonstrated that OpenCTI can be used to:

1. Identify threat groups associated with malware.
2. Investigate malware-to-threat-actor relationships.
3. Pivot from malware to attack patterns and tools.
4. Investigate vulnerabilities associated with threat activity.
5. Analyze campaigns and intelligence reports.
6. Investigate technical observables and indicators.
7. Examine incident/event descriptions.
8. Correlate adversary behavior with MITRE ATT&CK concepts.
9. Build a broader understanding of an attack from individual intelligence entities.

The most important takeaway was the ability to move from:

```text
Single Entity
      ↓
Relationships
      ↓
Threat Context
      ↓
Adversary Behavior
      ↓
Investigation Hypothesis
```

---

# Tools & Technologies

* OpenCTI
* STIX 2
* MITRE ATT&CK
* Threat Intelligence
* Knowledge Graph
* IOC Analysis
* Malware Intelligence
* Threat Actor Analysis

---

# Skills Demonstrated

* Cyber Threat Intelligence (CTI)
* Threat Actor Investigation
* Malware Intelligence
* IOC Investigation
* MITRE ATT&CK Analysis
* Threat Intelligence Correlation
* Knowledge Graph Investigation
* Vulnerability Intelligence
* Campaign Analysis
* SOC Investigation Methodology
* Evidence-Based Analysis

---

# Conclusion

This lab provided practical experience with OpenCTI as a threat intelligence investigation platform.

The investigation focused not only on finding individual answers, but on understanding how threat intelligence entities are connected.

The key analytical concept was:

```text
Search → Entity → Relationship → Context → Evidence → Finding
```

This relationship-driven approach is highly valuable for SOC analysts because it enables analysts to enrich alerts, investigate suspicious activity, identify adversary behavior, and develop threat-hunting hypotheses from structured intelligence.
