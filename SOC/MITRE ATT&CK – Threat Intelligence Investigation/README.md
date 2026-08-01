
# MITRE ATT&CK Threat Intelligence Lab

## Overview

The MITRE ATT&CK Threat Intelligence Lab focuses on operationalizing the **MITRE ATT&CK Framework** from a Blue Team perspective to analyze adversary behavior, identify relevant threat groups and software, and develop appropriate detection strategies.

During the investigation, multiple scenario-based questions were analyzed using the MITRE ATT&CK knowledge base. The investigation covered cloud discovery techniques, threat group identification, initial access tactics, ransomware behavior, and credential-based lateral movement techniques such as Pass the Hash.

The primary objective of this investigation was to understand how MITRE ATT&CK can be used to translate threat intelligence into actionable defensive measures, identify adversary techniques, and improve detection capabilities within an enterprise environment.

---

# Scenario

The Blue Team was tasked with performing threat intelligence activities for a company that relies heavily on cloud services such as **Azure AD and Office 365**.

The investigation focused on using the MITRE ATT&CK Framework to answer scenario-based questions involving:

* Cloud discovery
* Threat group identification
* Initial Access
* Ransomware behavior
* Account Access Removal
* Pass the Hash
* Authentication monitoring
* Detection engineering

The investigation required identifying the corresponding ATT&CK tactics, techniques, groups, and software associated with each scenario.

---

# Investigation Process

## Stage 1 – Cloud Discovery Investigation

The company heavily relies on cloud services such as Azure AD and Office 365.

The investigation focused on identifying which ATT&CK technique should be prioritized for mitigation when an attacker has already obtained valid credentials and attempts to perform discovery activities through cloud services.

The relevant MITRE ATT&CK technique was identified as:

**Cloud Service Dashboard (T1526)**

This technique describes adversaries accessing cloud service dashboards to obtain information about the cloud environment.

Because attackers with valid credentials may be able to access cloud management interfaces, monitoring and restricting access to cloud dashboards is an important defensive measure.

### MITRE ATT&CK

| Type         | Value                   |
| ------------ | ----------------------- |
| Technique    | Cloud Service Dashboard |
| Technique ID | T1526                   |
| Platform     | Cloud                   |

---

## Stage 2 – Threat Group Identification

During the investigation, an uncommon data flow was observed on:

```text
Port 4050
```

The network behavior was correlated with MITRE ATT&CK threat intelligence to identify the associated Advanced Persistent Threat group.

The investigation identified:

**APT-C-36 (Blind Eagle)**

The group is tracked by MITRE ATT&CK under:

```text
G0099
```

Identifying the threat group associated with unusual network activity provides valuable context for threat hunting and helps defenders investigate additional indicators and techniques associated with the group.

### Evidence

| Type           | Value       |
| -------------- | ----------- |
| Observed Port  | 4050        |
| Threat Group   | APT-C-36    |
| Alias          | Blind Eagle |
| MITRE Group ID | G0099       |

---

## Stage 3 – Initial Access Tactic Identification

The investigation then focused on the ATT&CK tactic responsible for techniques used by adversaries to gain an initial foothold inside a target environment.

The identified tactic was:

**Initial Access**

MITRE ATT&CK ID:

```text
TA0001
```

Initial Access contains techniques that adversaries use to establish an initial foothold within a compromised environment.

Understanding the tactic provides defenders with a structured way to identify and mitigate the different attack vectors that can be used to enter an organization.

### MITRE ATT&CK

| Type      | Value          |
| --------- | -------------- |
| Tactic    | Initial Access |
| Tactic ID | TA0001         |

---

## Stage 4 – Ransomware and Account Access Removal

The investigation included a scenario involving software capable of preventing users from accessing their accounts by locking accounts, deleting accounts, or changing passwords.

The identified software was:

**LockerGoga**

The corresponding MITRE ATT&CK Software ID is:

```text
S0372
```

The behavior is associated with:

**Account Access Removal (T1531)**

This technique describes adversary behavior intended to prevent legitimate users from accessing their accounts or systems.

The identification of the software and technique demonstrates how ATT&CK can be used to connect observed behavior with known malicious software.

### Evidence

| Type         | Value                  |
| ------------ | ---------------------- |
| Software     | LockerGoga             |
| Software ID  | S0372                  |
| Technique    | Account Access Removal |
| Technique ID | T1531                  |

---

## Stage 5 – Pass the Hash Investigation

The investigation also examined the use of **Pass the Hash**, a credential-based technique commonly used by attackers to authenticate to remote systems using a stolen password hash instead of the plaintext password.

The relevant MITRE ATT&CK technique was identified as:

**Pass the Hash**

```text
T1550.002
```

Pass the Hash can allow attackers to move laterally across an environment and authenticate to remote systems using compromised credentials.

Because this activity can resemble legitimate authentication, identifying abnormal authentication patterns is important for detection.

### Detection Strategy

The recommended detection approach identified during the investigation was:

> **Monitor newly created logons and credentials used in events and review for discrepancies.**

Additional Windows authentication telemetry can be correlated to identify suspicious network authentication and lateral movement behavior.

Relevant Windows events include:

* Event ID 4624 – Successful Logon
* Logon Type 3 – Network Logon
* Event ID 4648 – Explicit Credential Logon
* Event ID 4672 – Special Privileges Assigned

Monitoring authentication discrepancies across systems can help identify potential Pass the Hash activity.

### MITRE ATT&CK

| Type            | Value                        |
| --------------- | ---------------------------- |
| Technique       | Pass the Hash                |
| Technique ID    | T1550.002                    |
| Detection Focus | Authentication discrepancies |

---

# Indicators of Interest

| Type                   | Value                   |
| ---------------------- | ----------------------- |
| Cloud Technique        | Cloud Service Dashboard |
| Technique ID           | T1526                   |
| Threat Group           | APT-C-36                |
| Alias                  | Blind Eagle             |
| Group ID               | G0099                   |
| Observed Port          | 4050                    |
| Initial Access Tactic  | Initial Access          |
| Tactic ID              | TA0001                  |
| Software               | LockerGoga              |
| Software ID            | S0372                   |
| Account Access Removal | T1531                   |
| Pass the Hash          | T1550.002               |

---

# MITRE ATT&CK Mapping

| Tactic                             | Technique               | ID        |
| ---------------------------------- | ----------------------- | --------- |
| Discovery                          | Cloud Service Dashboard | T1526     |
| Initial Access                     | Initial Access          | TA0001    |
| Impact                             | Account Access Removal  | T1531     |
| Defense Evasion / Lateral Movement | Pass the Hash           | T1550.002 |
| Threat Group                       | APT-C-36 / Blind Eagle  | G0099     |
| Software                           | LockerGoga              | S0372     |

---

# Key Findings

* Identified **Cloud Service Dashboard (T1526)** as the relevant cloud discovery technique.
* Identified **APT-C-36 (Blind Eagle)** as the threat group associated with the observed port 4050 activity.
* Identified the MITRE group ID **G0099**.
* Identified **TA0001 – Initial Access** as the tactic associated with gaining an initial foothold.
* Identified **LockerGoga** as the software associated with the account access removal scenario.
* Identified the LockerGoga MITRE Software ID as **S0372**.
* Identified **T1531 – Account Access Removal** as the relevant ATT&CK technique.
* Identified **T1550.002 – Pass the Hash** as the relevant credential-based technique.
* Developed an authentication-monitoring approach for detecting potential Pass the Hash activity.
* Applied MITRE ATT&CK to correlate threat intelligence with practical Blue Team detection strategies.

---

# Tools & Resources

MITRE ATT&CK Framework

Threat Intelligence

Windows Security Event Logs

Cloud Security Concepts

Authentication Monitoring

Blue Team Detection Techniques

Network Traffic Analysis

---

# Skills Demonstrated

MITRE ATT&CK Analysis

Threat Intelligence

Blue Team Operations

Detection Engineering

Threat Group Identification

Cloud Security

Windows Authentication Analysis

Credential Attack Detection

Adversary Behavior Analysis

ATT&CK Technique Mapping

Security Monitoring

Incident Detection

---

# Conclusion

This investigation demonstrated how the **MITRE ATT&CK Framework** can be operationalized by a Blue Team to analyze adversary behavior and develop practical defensive strategies.

The investigation began by analyzing cloud discovery scenarios and identifying **Cloud Service Dashboard (T1526)** as an important technique to monitor when attackers obtain valid cloud credentials. Threat intelligence analysis was then used to identify **APT-C-36 (Blind Eagle)** based on the observed network activity on port 4050.

Additional scenarios focused on ransomware behavior and credential-based attacks. **LockerGoga (S0372)** was identified in relation to **Account Access Removal (T1531)**, while **Pass the Hash (T1550.002)** was analyzed from a detection perspective.

By combining threat intelligence, MITRE ATT&CK mapping, authentication monitoring, and Blue Team detection principles, the investigation demonstrated how the framework can be transformed from a knowledge base into actionable security controls and detection strategies.

---


