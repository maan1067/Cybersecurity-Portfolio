# Phishing Analysis Tools

## Overview

This TryHackMe room focuses on using security tools to investigate phishing emails safely and efficiently.

Rather than manually inspecting every email, analysts learn how to automate the extraction of email artifacts, inspect malicious URLs, analyze suspicious attachments, and detonate malware inside secure sandbox environments.

---

## Objectives

- Analyze email headers
- Extract malicious URLs
- Verify sender information
- Investigate suspicious attachments
- Calculate file hashes
- Analyze malware behavior
- Collect Indicators of Compromise (IOCs)
- Perform phishing investigations using real-world tools

---

# Information Collection

During phishing investigations analysts should always collect:

## Email Header

- Sender Email
- Sender IP Address
- Reverse DNS
- Subject
- Recipient
- Reply-To
- Date & Time

## Email Body

- URLs
- Attachments
- SHA256 Hash
- MD5 Hash
- Domains
- IP Addresses

> Never click links or open attachments directly.

---

# Email Header Analysis Tools

## Google Message Header Analyzer

https://toolbox.googleapps.com/apps/messageheader/analyzeheader

Analyzes SMTP headers and identifies routing information.

---

## Microsoft Message Header Analyzer

https://mha.azurewebsites.net/

Provides another method for parsing email headers.

---

## MailHeader

https://mailheader.org/

Alternative email header analyzer.

---

# IP Reputation Tools

## IPinfo

https://ipinfo.io/

Used to investigate sender IP addresses.

---

## URLScan

https://urlscan.io/

Safely renders suspicious websites and collects:

- Screenshot
- Network activity
- Domains
- IPs
- Cookies
- JavaScript

---

## Cisco Talos Reputation

https://talosintelligence.com/reputation

Checks IP and Domain reputation.

---

## Task Answer

**Question**

What is the official site name of the bank that capitai-one.com tried to resemble?

**Answer**

```
capitalone.com
```

---

# Email Body Analysis

Analysts should inspect:

- Embedded URLs
- Attachments
- File hashes
- Root domains

Useful tools include:

## URL Extractor

https://www.convertcsv.com/url-extractor.htm

Extracts all URLs from raw email source.

---

## CyberChef

Can automatically extract:

- URLs
- Domains
- Encoded strings

---

## File Reputation

### VirusTotal

https://www.virustotal.com/

### Cisco Talos File Reputation

https://talosintelligence.com/talos_file_reputation

Used to check attachment reputation.

---

## Task Answer

How can you manually get the location of a hyperlink?

```
Copy Link Location
```

---

# Malware Sandboxes

Instead of executing malware locally, analysts use sandbox environments.

Popular services include:

## Any.Run

https://app.any.run/

Provides:

- Process Tree
- Network Connections
- DNS Requests
- HTTP Traffic
- Registry Activity
- File Activity

---

## Hybrid Analysis

https://www.hybrid-analysis.com/

---

## Joe Sandbox

https://www.joesecurity.org/

Supports:

- URL Analysis
- MITRE ATT&CK
- YARA
- Sigma
- Malware Behavior

---

# PhishTool

https://phishtool.com/

PhishTool automates phishing investigations.

It extracts:

- Sender
- Recipient
- Subject
- Originating IP
- Attachments
- URLs
- VirusTotal Reputation
- Email Headers

It also supports incident classification and IOC extraction.

---

## Task Answer

Look at the Strings output.

What is the name of the EXE file?

```
#454326_PDF.exe
```

---

# Phishing Case 1

## Scenario

Investigate a phishing email impersonating Netflix.

### Findings

| Indicator | Value |
|------------|-------|
| Brand | Netflix |
| From | JGQ47wazXe1xYVBrkeDg-JOg7ODDQwWdR@JOg7ODDQwWdR-yVkCaBkTNp.gogolecloud.com |
| Originating IP | 209[.]85[.]167[.]226 |
| Suspicious Domain | etekno[.]xyz |
| Shortened URL | hxxps[://]t[.]co/yuxfZm8KPg?amp==1 |

---

# Phishing Case 2

Analyzed using Any.Run.

## Findings

| Indicator | Value |
|------------|-------|
| Classification | Suspicious activity |
| PDF | Payment-updateid.pdf |
| SHA256 | cc6f1a04b10bcb168aeec8d870b97bd7c20fc161e8310b5bce1af8ed420e2c24 |
| Malicious IPs | 2[.]16[.]107[.]24, 2[.]16[.]107[.]83 |
| Bad Process | svchost.exe |

---

# Phishing Case 3

Analyzed using Any.Run.

## Findings

| Indicator | Value |
|------------|-------|
| Classification | Malicious activity |
| Excel File | CBJ200620039539.xlsx |
| SHA256 | 5f94a66e0ce78d17afc2dd27fc17b44b3ffc13ac5f42d3ad6a5dcfb36715f3eb |
| Domains | biz9holdings[.]com, findresults[.]site, ww38[.]findresults[.]site |
| IPs | 75[.]2[.]11[.]242, 103[.]224[.]182[.]251, 204[.]11[.]56[.]48 |
| Exploit | CVE-2017-11882 |

---

# Additional Resources

- https://mxtoolbox.com
- https://phishtank.com
- https://www.spamhaus.org
- https://github.com/ninoseki/eml_analyzer

---

# Skills Gained

- Email Header Analysis
- URL Investigation
- IOC Collection
- Malware Sandbox Analysis
- Threat Intelligence
- Attachment Analysis
- SHA256 Verification
- Phishing Detection
- Any.Run Investigation
- PhishTool Usage
- VirusTotal Analysis

---
