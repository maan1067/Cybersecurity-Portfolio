# Lockdown Lab
![](Screenshot%202026-07-20%20182345.png)
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
![](Screenshot%202026-07-20%20172605.png)
```
10.0.2.4
```

---

## 2. Identify the Enumeration Tool
![](Screenshot%202026-07-20%20183909.png)
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
![](Screenshot%202026-07-20%20174359.png)
showed the attacker initially accessing two network shares:

```
\\10.0.2.15\IPC$
\\10.0.2.15\Documents
```

---

## 4. Web Shell Upload
![](Screenshot%202026-07-20%20174614.png)
Reviewing SMB Create Requests revealed the attacker creating a malicious ASP.NET file inside the Documents share.

Uploaded file:

```
shell.aspx
```

The file provided remote code execution through the IIS web server.

---

## 5. Reverse Shell
![](Screenshot%202026-07-20%20172227.png)
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

# Memory Dump Analysis
![](R.jpg)
## Overview

This section focuses on the **Memory Forensics** phase of the investigation.

After identifying the attacker’s activity through network traffic analysis, the investigation moved to analyzing a captured Windows memory dump using **Volatility 3**. The objective was to identify malicious processes, discover persistence mechanisms, inspect network connections, and answer the investigation questions.

---

## Tools Used

- Volatility 3
- Windows Command Prompt
- FTK Imager (Memory Acquisition)
- GitHub

---

# Q6 - Kernel Base Address

### Question

> Your memory snapshot captures the system’s kernel in situ, providing vital context for the breach.
> What is the kernel base address in the dump?

### Method

The Windows kernel information was extracted using the following Volatility plugin:

```powershell
.\vol.exe -f C:\Intel\memdump.mem windows.info
```

The plugin returns detailed operating system information including:

- Windows Version
- Architecture
- Kernel Base Address
- DTB
- Build Number

### Evidence
![](Screenshot%202026-07-20%20185728.png)

# Q7 - Persistence Executable

### Question

> A trusted service launches an unfamiliar executable residing outside the usual IIS stack, signalling a persistence implant.
> What is the final full on-disk path of that executable?

### Method

The running process tree was enumerated using:
![](Screenshot%202026-07-20%20190834.png)
```powershell
.\vol.exe -f C:\Intel\memdump.mem windows.pstree
```

While reviewing the process hierarchy, an unusual executable was discovered.

Process relationship:

```
services.exe
    └── svchost.exe
            └── w3wp.exe
                    └── updatenow.exe
```

Unlike legitimate IIS binaries, the executable was located inside the Windows Startup folder.

### Evidence
![](Screenshot%2020326-07-20%20190834.png)

### Answer
![](Screenshot%202026-07-20%201590703.png)
```text
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\updatenow.exe
```

---

# Q8 - Reverse Shell Parent Process

### Question

> The reverse shell’s outbound traffic is handled by a built-in Windows process that also spawns the implanted executable.
> What is the name of this process, and what PID does it run under?

### Method

Network connections were inspected using:

```powershell
.\vol.exe -f C:\Intel\memdump.mem windows.netscan
```

The process tree from **windows.pstree** was then correlated with the active network connections.

The investigation showed that the malicious executable was launched by **w3wp.exe**, the IIS Worker Process.

The same process also established the outbound reverse shell connection to the attacker's listener.

### Evidence
![](Screenshot%202026-07-20%20191419.png)
```
images/
├── q8-netscan.png
└── q8-process-tree.png
```

### Answer

```
Process : w3wp.exe

PID : 4332
```

---

# Summary

The memory analysis revealed:

- The Windows kernel base address.
- A malicious persistence executable located in the Startup folder.
- IIS Worker Process (`w3wp.exe`) spawning the implant.
- Reverse shell communication originating from the IIS process.
- Successful correlation between network forensics and memory forensics artifacts.

---

## Skills Demonstrated

- Memory Forensics
- Windows Process Analysis
- Volatility 3
- Process Tree Analysis
- Network Connection Analysis
- Reverse Shell Investigation
- Incident Response
- Digital Forensics
