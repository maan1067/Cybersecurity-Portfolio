# Lockdown Lab

## Overview

This lab simulates a real-world multi-stage intrusion against a public-facing Microsoft IIS server. The investigation involved analyzing network traffic, memory artifacts, and malware to reconstruct the complete attack chain.

This write-up currently covers the **PCAP Analysis** phase of the investigation.

---

# Scenario

TechNova Systems' SOC detected suspicious outbound traffic from a public-facing IIS server. Initial evidence suggested that the server had been compromised through a web shell, allowing an attacker to establish remote access.

The objective was to identify the attacker's activities, reconstruct the intrusion timeline, and collect indicators of compromise (IOCs).

---

# PCAP Analysis

## Objective

Analyze the captured network traffic to identify:

- Attacker IP
- Reconnaissance activity
- Enumeration techniques
- SMB share access
- Web shell upload
- Reverse shell communication

---

# Investigation Process

## 1. Identify the Attacker

Using Wireshark Conversations and endpoint statistics, the host generating the reconnaissance traffic was identified.

**Attacker IP**

```
10.0.2.4
```

---

## 2. Identify the Enumeration Tool

Filtering HTTP requests revealed the following User-Agent:

```
Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)
```

This confirms that the attacker used:

```
Nmap NSE
```

---

## 3. SMB Share Enumeration

Filtering SMB2 Tree Connect Requests:

```
smb2.cmd == 3
```

showed the attacker initially accessing two network shares:

```
\\10.0.2.15\IPC$
\\10.0.2.15\Documents
```

---

## 4. Web Shell Upload

Reviewing SMB Create Requests revealed the attacker creating a malicious ASP.NET file inside the Documents share.

Uploaded file:

```
shell.aspx
```

The file provided remote code execution through the IIS web server.

---

## 5. Reverse Shell
![](Screenshot%202026-07-20%20175729.png)
After the web shell was executed, the compromised server initiated an outbound connection back to the attacker.

Reverse Shell Details

| Source | Destination | Port |
|---------|------------|------|
|10.0.2.15|10.0.2.4|4443|

Port **4443** was used as the reverse shell listener.

---

# Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
|Attacker IP|10.0.2.4|
|Victim IP|10.0.2.15|
|Web Shell|shell.aspx|
|SMB Share|\\10.0.2.15\IPC$|
|SMB Share|\\10.0.2.15\Documents|
|Reverse Shell Port|4443|

---

# MITRE ATT&CK Mapping

| Tactic | Technique |
|---------|-----------|
|Reconnaissance|Active Scanning (T1595)|
|Discovery|Network Service Discovery (T1046)|
|Lateral Movement|SMB/Windows Admin Shares (T1021.002)|
|Execution|Web Shell (T1505.003)|
|Command and Control|Application Layer Protocol (T1071)|

---

# Key Findings

- Identified the attacker's source IP.
- Confirmed reconnaissance using Nmap NSE.
- Observed SMB share enumeration.
- Detected the upload of a malicious ASP.NET web shell.
- Identified the reverse shell connection over TCP port 4443.
- Successfully reconstructed the initial intrusion chain using only packet analysis.

---

# Skills Demonstrated

- Network Forensics
- Wireshark Analysis
- SMB Traffic Analysis
- HTTP Traffic Analysis
- IOC Identification
- Attack Timeline Reconstruction
- MITRE ATT&CK Mapping
