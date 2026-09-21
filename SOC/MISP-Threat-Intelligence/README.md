

---

# MISP — Threat Intelligence Investigation

## Overview

The MISP Lab focuses on using MISP (Malware Information Sharing Platform) as a Threat Intelligence Platform to investigate, correlate, and share threat intelligence across trusted communities.

MISP is not just an IOC database — it is an intelligence-sharing platform built around **Events** and **Attributes**, with additional structuring through **Objects**, **Galaxies**, **Tags**, and **Taxonomies**. It enables analysts to attribute activity to threat actors, link campaigns, enrich indicators with context, and share structured intelligence with partner organizations.

This investigation covers two parts:

1. **Core MISP Investigation** — exploring MISP entities (Malware, Attack Patterns, Indicators) and their relationships.
2. **Scenario-Based Investigation** — investigating an APT28 campaign targeting Ukraine and EU countries, correlating event metadata with threat intelligence.

The primary objective of this investigation was to navigate MISP, investigate threat intelligence entities, identify relationships between adversaries and their tools or techniques, extract Indicators of Compromise and contextual intelligence, and classify observed activity using the appropriate CTI structures where evidence supported it.

---

## Scenario

A SOC analyst is investigating multiple suspicious activities involving known malware families, threat groups, attack patterns, and vulnerabilities.

The organization uses MISP as its Threat Intelligence Platform to enrich investigations with contextual information about adversaries, campaigns, and infrastructure.

The investigation required analyzing MISP events and their relationships to answer questions such as:

* Which threat group uses a specific malware?
* Which attack patterns are associated with a malware family?
* Which vulnerabilities have been exploited by a threat actor?
* Which campaign is associated with a specific event?
* What indicators are linked to a targeted campaign?

The investigation was performed through MISP's event view, attribute tables, galaxies, and relationship views.

---

## MISP Core Concepts

| Concept | Description |
|---------|-------------|
| **Event** | A container grouping related threat intelligence — typically everything known about a single incident, campaign, or report. |
| **Attribute** | An atomic indicator or contextual data point (IP, domain, hash, filename, URL, comment). Attributes with the `to_ids` flag set are treated as actionable indicators. |
| **Object** | A structured group of related attributes (e.g., a File object bundling filename, hashes, size, and path). |
| **Galaxy** | A library of structured knowledge (threat actors, malware families, ATT&CK techniques, countries). |
| **Tag** | A label attached to events or attributes for classification, filtering, and automation. |
| **Taxonomy** | A curated, machine-readable vocabulary of tags (TLP, PAP, Admiralty Scale, etc.). |
| **Feeds** | External or local sources of indicators that can be cached for correlation or fetched into the instance. |
| **Communities** | Trusted groups of organizations that share intelligence through MISP. |

These concepts structure how MISP organizes and shares threat intelligence — from atomic indicators up to attributed campaigns.

---

## Investigation Methodology

The investigation followed a consistent, evidence-driven approach applied to every question:

```text
Question
   ↓
Search / Investigation Path
   ↓
Open Event / Attribute / Object / Galaxy / Entity
   ↓
Inspect Relationships / Context
   ↓
Read Evidence
   ↓
Validate Finding
   ↓
Document Result
```

The core principle:

> **Don't memorize the answer. Memorize the investigation path.**

Each finding in this document is supported by a navigable path inside MISP, allowing it to be reproduced by any analyst with access to the same instance.

---

# Investigation & Findings

## Stage 1 — Malware & Threat Actor Investigation

### 1.1 — 4H RAT Malware

#### Question

What is the name of the group that uses the 4H RAT malware?

#### Investigation Path

```text
Arsenal
   → Malware
   → Search: 4H RAT
   → Entity Details
   → Description
```

#### Evidence

```text
4H RAT is malware that has been used by Putter Panda since at least 2007.
```

#### Finding

**Putter Panda**

#### SOC Relevance

If 4H RAT samples are detected in an environment, correlating them with Putter Panda's known TTPs, infrastructure, and targeting patterns allows the SOC to prioritize the investigation and pivot to related activity.

---

### 1.2 — Command-Line Interface Attack Pattern

#### Question

What kill-chain phase is linked with the Command-Line Interface Attack Pattern?

#### Investigation Path

```text
Arsenal
   → Attack Patterns
   → Search: Command-Line Interface
   → Entity Details
   → Kill Chain Phases
```

#### Evidence

```text
Kill Chain Phases: execution-ics
```

#### Finding

**execution-ics**

> **Note — MISP vs MITRE ATT&CK terminology:**
>
> `execution-ics` is a **Kill Chain Phase label** present in the MISP dataset. It is not equivalent to a MITRE ATT&CK Technique ID. The distinction is:
>
> * **MISP / Kill Chain Phase** → `execution-ics`
> * **MITRE ATT&CK Technique** → e.g., `T1059` (Command and Scripting Interpreter)
> * **STIX Attack Pattern** → the entity itself, independent of the label.
>
> The kill-chain phase label from MISP is not substituted for a MITRE ATT&CK Technique ID unless the evidence explicitly supports that mapping.

#### SOC Relevance

Understanding the kill-chain phase associated with an attack pattern helps the SOC prioritize detections at the correct stage of the attack lifecycle.

---

### 1.3 — Indicators Location

#### Question

Within the Activities category, which tab would house the Indicators?

#### Investigation Path

```text
Activities
   → Observations
```

#### Evidence

```text
Technical elements, detection rules and artefacts identified during a cyber attack
are listed under Observations.
```

#### Finding

**Observations**

---

## Stage 2 — APT28 Campaign Investigation

### 2.1 — Event ID

#### Question

What event ID has been assigned to the APT28 event?

#### Investigation Path

```text
Event Actions
   → List Events
   → Filter: APT28
   → Event ID Column
```

#### Evidence

```text
Event ID: 211
Event Info: "Hanger Bulletin": UAC-0001 (APT28) carries out cyberattacks
            against Ukraine and EU countries using the exploit CVE-2026-21509
            (CERT-UA#19542)
Creator Org: CIRCL
```

#### Finding

**211**

---

### 2.2 — Microsoft Naming for APT28

#### Question

Refer to the event galaxies. How does Microsoft refer to APT28 group?

#### Investigation Path

```text
Event (ID 211)
   → Galaxies
   → Microsoft Activity Group actor
   → STRONTIUM
```

#### Evidence

```text
Galaxy Cluster: Microsoft Activity Group actor
Name: STRONTIUM
```

#### Finding

**STRONTIUM**

#### SOC Relevance

Threat actors are tracked under different names across vendors. Knowing that Microsoft refers to APT28 as STRONTIUM enables analysts to correlate intelligence across Microsoft Defender, Sentinel, and other Microsoft telemetry with MISP threat intelligence.

---

### 2.3 — Microsoft Office CVE

#### Question

What CVE, targeting MS Office, was used in the attack?

#### Investigation Path

```text
Event (ID 211)
   → Attributes
   → Vulnerability Object
   → id: vulnerability
```

#### Evidence

```text
Event Info: "using the exploit CVE-2026-21509"
Attribute (id: vulnerability): CVE-2026-21509
References:
  - https://vulnerability.circl.lu/vuln/CVE-2026-21509
  - https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-21509
```

#### Finding

**CVE-2026-21509**

#### SOC Relevance

Knowing the exploited CVE allows the SOC to prioritize patching, build detection rules for exploitation attempts, and assess exposure across the organization.

---

### 2.4 — Covenant C2 DLL MD5

#### Question

What is the MD5 hash of the dropped Covenant C2 DLL?

#### Investigation Path

```text
Event (ID 211)
   → Attributes
   → Search: Covenant
   → File Object
   → MD5
```

#### Evidence

```text
Object name: file
filename: covenant.dll
md5: 6f528ad405bffa4a8c2f61b1fa2172fd
Tag: COVENANT
```

#### Finding

**6f528ad405bffa4a8c2f61b1fa2172fd**

#### SOC Relevance

The MD5 hash of `covenant.dll` can be used to:

* Hunt across endpoints and EDR telemetry for the dropped DLL.
* Enrich SIEM alerts.
* Feed detection engineering with a known-bad indicator.
* Pivot into further investigation of Covenant C2 activity in the environment.

---

### 2.5 — CERT-UA Report URL

#### Question

What is the URL of the CERT-UA report referenced in the event attributes?

#### Investigation Path

```text
Event (ID 211)
   → Attributes
   → Report Object
   → link
```

#### Evidence

```text
Object name: report
link: https://cert.gov.ua/article/6287250
title: "Hanger Bulletin": UAC-0001 (APT28) carries out cyberattacks
       against Ukraine and EU countries using the exploit
       CVE-2026-21509 (CERT-UA#19542)
```

#### Finding

**https://cert.gov.ua/article/6287250**

#### SOC Relevance

The CERT-UA report provides authoritative context about the campaign — TTPs, IOCs, targeting, and attribution. This supports incident scoping and strategic intelligence for organizations in affected sectors.

---

## Stage 3 — Indicator Investigation (Prynt Stealer)

### 3.1 — Malware Family for MD5 Hash

#### Question

What malware name is related to the following attribute?
MD5 Hash: `661842995f7fdd2e61667dbc2f019ff3`

#### Investigation Path

```text
Search
   → MD5 Hash: 661842995f7fdd2e61667dbc2f019ff3
   → Event 208
   → Event Info
```

#### Evidence

```text
Event ID: 208
Event Info: Prynt Stealer Spotted In the Wild — A New Info Stealer
            Performing Clipper And Keylogger Activities
```

#### Finding

**Prynt Stealer**

> **Note:** External labels from third-party sources (e.g., VirusTotal) may not match the family name recorded in MISP. In this case, the MISP event explicitly identified the family as Prynt Stealer.

#### SOC Relevance

Correlating a suspicious hash with a MISP event provides immediate malware-family context, enabling targeted hunting, detection engineering, and prioritization of the investigation.

---

# Threat Intelligence Relationship Map

```text
Event (ID 211)
   │
   ├── Threat Actor      → APT28 (Microsoft naming: STRONTIUM)
   ├── Vulnerability     → CVE-2026-21509
   ├── File Object       → covenant.dll
   │     └── MD5         → 6f528ad405bffa4a8c2f61b1fa2172fd
   ├── Report Object     → CERT-UA — Hanger Bulletin / CERT-UA#19542
   └── Galaxies          → Microsoft Activity Group actor, Enterprise Attack - Intrusion Set
```

```text
Event (ID 208)
   │
   └── Malware Family    → Prynt Stealer
         └── MD5 Hash    → 661842995f7fdd2e61667dbc2f019ff3
```

This relationship-driven view reflects how MISP connects atomic indicators to higher-level intelligence — transforming isolated indicators into attributed, contextualized activity.

---

# Threat Intelligence Findings

| Category | Finding |
|----------|---------|
| Threat Actor | APT28 (Microsoft naming: STRONTIUM) |
| Threat Actor | Putter Panda |
| Malware | 4H RAT |
| Malware | Prynt Stealer |
| Kill Chain Phase | `execution-ics` |
| Attack Pattern | Command-Line Interface |
| Vulnerability | CVE-2026-21509 (Microsoft Office) |
| File (Dropped) | covenant.dll |
| Hash (MD5) | `6f528ad405bffa4a8c2f61b1fa2172fd` |
| Hash (MD5) | `661842995f7fdd2e61667dbc2f019ff3` |
| Campaign (Related) | "Hanger Bulletin" — UAC-0001 (APT28) |
| Report | CERT-UA — Hanger Bulletin / CERT-UA#19542 |
| Event ID | 211 |
| Event ID | 208 |

---

# Threat Intelligence Classification

> **Rule:** Classification in this section is based strictly on evidence from MISP. Kill-chain phase labels, CVE IDs, and malware family names are not converted into MITRE ATT&CK Technique IDs unless evidence in MISP supports the mapping.

| Area | Finding | Identifier / Classification | Evidence |
|------|---------|-----------------------------|----------|
| Execution | Command-Line Interface | `execution-ics` — MISP Kill Chain Phase | Q1.2 |
| Vulnerability | Microsoft Office Exploitation | `CVE-2026-21509` — CVE | Q2.3 |

> **Note:** No MITRE ATT&CK Technique IDs are asserted in this document unless explicitly supported by MISP evidence. MISP Kill Chain Phase labels and CVE identifiers are distinct concepts and are documented as such.

---

# SOC Analyst Perspective

MISP supports multiple SOC workflows beyond IOC lookup:

```text
MISP Indicator
      ↓
IOC Enrichment
      ↓
Threat Actor / Malware Context
      ↓
SIEM / EDR Investigation
      ↓
Detection / Hunting
```

Practical applications demonstrated during this investigation:

* **Alert Enrichment** — Correlating a suspicious hash (e.g., `661842995f7fdd2e61667dbc2f019ff3`) with a MISP event provided immediate malware-family context (Prynt Stealer).
* **Threat Hunting** — Using the MD5 of `covenant.dll` to hunt for Covenant C2 activity across endpoints.
* **Vulnerability Intelligence** — Linking `CVE-2026-21509` to an active APT28 campaign supported patch prioritization.
* **Threat Actor Profiling** — Mapping APT28 across vendor naming conventions (STRONTIUM) enabled cross-vendor correlation.
* **Incident Response** — Accessing the CERT-UA report provided authoritative campaign context for scoping and containment.
* **Detection Engineering** — Extracted indicators such as hashes and filenames can support detection engineering, while CVE information can support vulnerability management and exposure assessment.

---

# MISP vs OpenCTI

| Aspect | MISP | OpenCTI |
|--------|------|---------|
| Core structure | Events + Attributes + Objects | Entities + Relationships |
| Focus | Threat intelligence sharing | Knowledge graph |
| Data model | Event-centric with structuring via Galaxies / Objects | STIX 2.x based graph |
| Primary use | Sharing within trusted communities | Correlating and visualizing adversary activity |

MISP emphasizes event-based intelligence management and sharing, while OpenCTI emphasizes relationship-based analysis and knowledge-graph exploration. Both can support complementary CTI workflows.

---

# Key Findings

* Identified **Putter Panda** as the threat group associated with **4H RAT**.
* Identified `execution-ics` as the **MISP Kill Chain Phase** label for the Command-Line Interface attack pattern — distinct from a MITRE ATT&CK Technique ID.
* Located indicators under **Activities → Observations**.
* Investigated **APT28 event (ID 211)** and identified:
  * Microsoft's naming convention for APT28: **STRONTIUM**.
  * Exploited Microsoft Office vulnerability: **CVE-2026-21509**.
  * Dropped Covenant C2 DLL MD5: **`6f528ad405bffa4a8c2f61b1fa2172fd`**.
  * CERT-UA report reference: **CERT-UA — Hanger Bulletin / CERT-UA#19542**.
* Correlated MD5 hash **`661842995f7fdd2e61667dbc2f019ff3`** with **Prynt Stealer** via MISP event 208.
* Demonstrated evidence-based investigation across MISP entities, attributes, objects, galaxies, and relationships.

---

# Tools & Technologies

* **MISP** (Malware Information Sharing Platform)
* **MITRE ATT&CK** (referenced for terminology distinction)
* **CVE / CIRCL Vulnerability Lookup**
* **CERT-UA Report** (external reference)
* **MISP Galaxies** (Microsoft Activity Group actor, Enterprise Attack — Intrusion Set)

---

# Skills Demonstrated

* Cyber Threat Intelligence (CTI)
* Threat Intelligence Investigation
* MISP Analysis
* Event / Attribute / Object / Galaxy Navigation
* Threat Actor Attribution
* Malware Family Identification
* Vulnerability Intelligence
* IOC Investigation
* Threat Correlation
* MITRE ATT&CK Terminology Discipline
* SOC Investigation
* Incident Response Support
* Evidence-Based Analysis
* Threat Hunting Context

---

# Conclusion

This investigation demonstrated the use of MISP as a Threat Intelligence Platform for structured, evidence-based investigation. By navigating events, attributes, objects, and galaxies, the investigation connected atomic indicators to attributed threat actors, malware families, vulnerabilities, and campaigns.

The key methodological principle applied throughout was:

> **Question → Search → Entity / Attribute → Relationship → Evidence → Finding**

Each finding was supported by a navigable investigation path inside MISP — reinforcing that in Threat Intelligence work, **the evidence trail matters as much as the answer.**

This write-up is part of a consistent SOC Analyst portfolio alongside the OpenCTI – Threat Intelligence Investigation, applying the same investigation methodology, evidence discipline, and SOC-relevance framing across platforms.

---

# References

* **MISP Project** — https://www.misp-project.org/
* **MITRE ATT&CK** — https://attack.mitre.org/
* **CERT-UA** — https://cert.gov.ua/
* **Microsoft Security Response Center (MSRC)** — https://msrc.microsoft.com/
* **CIRCL Vulnerability Lookup** — https://vulnerability.circl.lu/

---

**Note on terminology accuracy:** Throughout this document, MISP-specific labels (Kill Chain Phases, taxonomy tags, CVE identifiers, galaxy cluster names) are kept distinct from MITRE ATT&CK Technique IDs. No MITRE technique mapping is asserted unless supported by MISP evidence.

