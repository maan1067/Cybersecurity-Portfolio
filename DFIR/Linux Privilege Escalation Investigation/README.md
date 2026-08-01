
---

# Linux Privilege Escalation Investigation
![](Screenshot%202026-08-01%20043134.png)
## Overview

The Linux Privilege Escalation Investigation Lab focuses on analyzing Linux Auditd logs to reconstruct a privilege escalation attack that resulted in full root access.

During the investigation, Linux Audit Logs were analyzed to identify the malicious executable, determine how root privileges were obtained, identify the exploited vulnerability, and discover what sensitive data was accessed after the compromise.

The primary objective was to reconstruct the attack timeline using Linux Audit Logs, identify Indicators of Compromise (IOCs), and map the observed attacker behavior to the MITRE ATT&CK Framework.

---

# Scenario

A Linux server generated Auditd logs after suspicious activity was detected.

System administrators suspected that an attacker had exploited a local privilege escalation vulnerability to obtain root access.

The investigation focused on identifying:

* The malicious binary
* The process responsible for the privilege escalation
* The exploited CVE
* The vulnerability type
* The commands executed after gaining root
* The file that was exfiltrated
* Relevant MITRE ATT&CK techniques

---

# Investigation Process

## Stage 1 – Linux Audit Log Analysis

The investigation began by reviewing the Auditd logs to identify the most frequently executed commands.

Command frequency analysis quickly highlighted an unusual executable named **evil**, which did not belong to the operating system.

Evidence

```bash
grep 'comm=' audit.log | cut -d'"' -f2 | sort | uniq -c | sort -nr
```
![](900.png)
---

## Stage 2 – Malicious Binary Identification

The next step was locating every execution of the suspicious binary inside the audit log.

Searching for the executable revealed the malicious process:

* Binary Name: **evil**
* Binary Path:

```text
/home/btlo/evil/evil
```

* Process ID:

```text
829992
```

Evidence

```bash
grep 'comm="evil"' audit.log
```

---

## Stage 3 – Privilege Escalation Analysis

Following the same process ID revealed that the binary executed **sudo**, specifically **sudoedit**, and successfully obtained root privileges.

Audit records showed the transition from a normal user to:

```text
uid=0
euid=0
```

Immediately afterward, the attacker spawned a root shell.

Evidence

```text
comm="sudoedit"
exe="/usr/bin/sudo"

comm="sh"
exe="/usr/bin/dash"
uid=0
euid=0
```

This confirmed that the privilege escalation was successful.

---

## Stage 4 – Vulnerability Identification

Research into the observed sudo behavior indicated that the attacker exploited the well-known **Baron Samedit** vulnerability.

**Exploited CVE**

```text
CVE-2021-3156
```

**Vulnerability Type**

```text
Heap-Based Buffer Overflow
```

This vulnerability allows local users to obtain root privileges by exploiting a heap overflow in **sudo**.

---

## Stage 5 – Post-Exploitation Activity

After obtaining root access, the attacker executed several commands from the root shell.

The Auditd TTY records contained hexadecimal command data that was decoded during the investigation.

Decoded command:

```bash
cat /etc/shadow
```

This confirmed that the attacker accessed the Linux password database after becoming root.

Evidence

```bash
echo 636174202F6574632F736861646F770A | xxd -r -p
```

Output

```text
cat /etc/shadow
```

---

## Stage 6 – Evidence of File Exfiltration

Analysis confirmed that the attacker accessed and exfiltrated the following sensitive file:

```text
/etc/shadow
```

The `/etc/shadow` file stores password hashes for local Linux accounts and is a high-value target during post-exploitation activities.

---

# Indicators of Compromise (IOCs)

| Type                 | Value                      |
| -------------------- | -------------------------- |
| Malicious Binary     | evil                       |
| Binary Path          | /home/btlo/evil/evil       |
| Process ID           | 829992                     |
| Privilege Escalation | sudoedit                   |
| CVE                  | CVE-2021-3156              |
| Vulnerability        | Heap-Based Buffer Overflow |
| Root Shell           | /usr/bin/dash              |
| Exfiltrated File     | /etc/shadow                |

---

# MITRE ATT&CK Mapping

| Tactic               | Technique                                     |
| -------------------- | --------------------------------------------- |
| Privilege Escalation | T1068 – Exploitation for Privilege Escalation |
| Execution            | T1059.004 – Unix Shell                        |
| Credential Access    | T1003 – OS Credential Dumping                 |
| Defense Evasion      | T1070 – Indicator Removal on Host             |

---

# Key Findings

* Identified the malicious executable **evil**.
* Determined that process **829992** was responsible for the privilege escalation.
* Confirmed exploitation of **CVE-2021-3156 (Baron Samedit)**.
* Identified the vulnerability as a **Heap-Based Buffer Overflow**.
* Reconstructed the privilege escalation attack using Linux Audit Logs.
* Confirmed successful root access through **sudoedit**.
* Determined that the attacker spawned a root shell.
* Verified that the attacker accessed and exfiltrated the **/etc/shadow** file.
* Mapped attacker activity to the MITRE ATT&CK Framework.

---

# Tools Used

* Linux Auditd
* grep
* cut
* sort
* uniq
* xxd
* Visual Studio Code
* Linux Terminal
* MITRE ATT&CK
* CVE Research

---

# Skills Demonstrated

* Linux DFIR
* Linux Audit Log Analysis
* Privilege Escalation Investigation
* Incident Response
* Process Timeline Reconstruction
* IOC Extraction
* Threat Hunting
* Linux Forensics
* CVE Analysis
* MITRE ATT&CK Mapping

---
