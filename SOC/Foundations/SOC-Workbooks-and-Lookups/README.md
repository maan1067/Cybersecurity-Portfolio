# SOC Workbooks and Lookups

## Overview

Security Operations Centers (SOCs) investigate hundreds or even thousands of security alerts every day. To ensure investigations remain consistent, accurate, and efficient, organizations rely on standardized documentation and internal knowledge resources.

Rather than investigating alerts from scratch, SOC analysts follow predefined investigation guides called **Workbooks**, **Runbooks**, and **Playbooks**. They also use internal lookup systems and external Threat Intelligence platforms to collect context, validate Indicators of Compromise (IOCs), and make informed decisions.

This room introduces the documentation and lookup resources that support professional SOC investigations.

---

# Learning Objectives

After completing this room, you will be able to:

- Understand the purpose of SOC documentation.
- Differentiate between Workbooks, Runbooks, and Playbooks.
- Understand investigation lookups.
- Perform IOC enrichment.
- Use Threat Intelligence during investigations.
- Follow standardized SOC investigation workflows.

---

# Why Standardized Investigations Matter

Every SOC analyst has a different level of experience and technical knowledge.

Without standardized investigation procedures:

- Analysts may investigate alerts differently.
- Important evidence may be overlooked.
- Investigation quality becomes inconsistent.
- False positives increase.
- Incident response becomes slower.

Organizations solve this challenge by documenting investigation procedures that every analyst follows.

## Benefits

- Faster investigations
- Consistent investigation quality
- Reduced human error
- Better knowledge sharing
- Easier onboarding for new analysts
- Improved incident response efficiency

---

# SOC Documentation

SOC documentation provides structured guidance that helps analysts investigate alerts using the same methodology across the organization.

The three most common documentation types are:

- Workbook
- Runbook
- Playbook

Each serves a different purpose during security operations.

---

# SOC Workbook

A **Workbook** is a standardized investigation guide created for a specific alert type.

Instead of deciding investigation steps manually, analysts follow predefined instructions.

## Workbook Contents

- Alert Description
- Investigation Objective
- Required Evidence
- Validation Steps
- Investigation Checklist
- Threat Intelligence References
- Escalation Criteria
- Reporting Instructions

### Example

Alert

```text
Suspicious PowerShell Execution
```

Workbook Steps

```text
Read Alert

↓

Review Parent Process

↓

Review Command Line

↓

Review Executing User

↓

Review Host

↓

Extract IOC

↓

Threat Intelligence Lookup

↓

Determine Verdict
```

---

# Runbook

A **Runbook** is a technical guide that explains how to perform one operational task.

Unlike Workbooks, Runbooks focus on actions rather than investigations.

Examples include:

- Reset Password
- Isolate Endpoint
- Block IP Address
- Investigate Phishing Email
- Disable User Account
- Validate Malware Detection

---

# Playbook

A **Playbook** defines the complete response process for an entire security incident.

Unlike Runbooks, Playbooks coordinate multiple departments.

Example:

```text
Ransomware Detection

↓

SOC Team

↓

DFIR Team

↓

IT Operations

↓

Network Team

↓

Management

↓

Legal

↓

Recovery
```

---

# Workbook vs Runbook vs Playbook

| Workbook | Runbook | Playbook |
|-----------|----------|-----------|
| Investigation Guide | Technical Procedure | Incident Response Plan |
| Alert Focused | Task Focused | Incident Focused |
| Used by SOC Analysts | Used by Analysts and Engineers | Used by Multiple Teams |

---

# Investigation Lookups

Security alerts rarely contain enough information by themselves.

SOC analysts perform **Lookups** to collect additional context before making a decision.

Common lookups include:

- User Lookup
- Host Lookup
- Asset Lookup
- IP Lookup
- Domain Lookup
- URL Lookup
- File Hash Lookup
- Email Lookup

The collected context helps determine whether the activity is malicious or legitimate.

---

# Internal Investigation Resources

## Asset Inventory

Asset Inventory stores information about organizational devices.

Typical information includes:

- Hostname
- Asset Owner
- Department
- Operating System
- Installed Software
- Device Criticality
- Asset Type

---

## Active Directory Lookup

Active Directory provides user information such as:

- Username
- Department
- Manager
- Group Membership
- User Privileges
- Account Status
- Last Login

---

## Configuration Management Database (CMDB)

The CMDB stores relationships between organizational assets.

Analysts use it to identify:

- Asset Ownership
- Business Criticality
- Connected Systems
- Service Dependencies

---

# External Threat Intelligence

External Threat Intelligence platforms help analysts enrich Indicators of Compromise.

| Platform | Purpose |
|----------|----------|
| VirusTotal | File, Hash, URL, Domain Reputation |
| AbuseIPDB | IP Reputation |
| ThreatFox | IOC Intelligence |
| MalwareBazaar | Malware Sample Lookup |
| URLScan | Website Investigation |
| WHOIS | Domain Registration Information |
| ANY.RUN | Interactive Malware Sandbox |

---

# IOC Enrichment

IOC Enrichment is the process of collecting additional information about an Indicator of Compromise.

Common IOC Types

- IP Address
- Domain
- URL
- File Hash
- Email Address
- Hostname

## IOC Enrichment Workflow

```text
Receive Alert

↓

Extract IOC

↓

Identify IOC Type

↓

Threat Intelligence Lookup

↓

Collect Reputation

↓

Validate IOC

↓

Continue Investigation
```

---

# Typical SOC Investigation Workflow

```text
Receive Alert

↓

Read Workbook

↓

Review Alert Details

↓

Identify User

↓

Identify Host

↓

Extract IOCs

↓

Perform Internal Lookups

↓

Perform Threat Intelligence Lookups

↓

Review Logs

↓

Validate Activity

↓

Determine Verdict

↓

Write Investigation Report

↓

Escalate if Required

↓

Close Alert
```

---

# Best Practices

- Always follow standardized documentation.
- Never investigate from memory alone.
- Validate every IOC.
- Use multiple Threat Intelligence sources.
- Document every investigation step.
- Escalate when additional expertise is required.

---

# Common Mistakes

- Ignoring the Workbook.
- Trusting one Threat Intelligence source.
- Skipping IOC validation.
- Closing alerts too quickly.
- Poor investigation documentation.
- Ignoring asset criticality.

---

# Practical Scenario

## Alert

Suspicious PowerShell Execution

### Investigation

1. Open the PowerShell Workbook.
2. Review the affected user.
3. Review the affected host.
4. Review the command line.
5. Review the parent process.
6. Extract the file hash.
7. Search VirusTotal.
8. Check AbuseIPDB for related IPs.
9. Validate whether the activity is authorized.
10. Determine the verdict.
11. Write the investigation report.
12. Escalate if necessary.

---

# Skills Learned

- Standardized Investigations
- Workbook Usage
- Runbook Execution
- Playbook Concepts
- IOC Enrichment
- Threat Intelligence
- Security Documentation
- Asset Investigation
- Incident Investigation

---

# Tools Used

- VirusTotal
- AbuseIPDB
- ThreatFox
- MalwareBazaar
- URLScan
- WHOIS
- ANY.RUN
- Active Directory
- CMDB

---

# Interview Notes

## Workbook

Used to investigate alerts.

## Runbook

Used to perform operational tasks.

## Playbook

Used to coordinate complete incident response.

Remember:

Workbook → Investigation

Runbook → Task

Playbook → Incident

---

# Interview Questions

### What is a SOC Workbook?

A Workbook is a standardized investigation guide that defines how analysts investigate a specific alert type.

---

### What is the difference between a Workbook and a Runbook?

A Workbook explains how to investigate an alert, while a Runbook explains how to perform a technical task.

---

### What is a Playbook?

A Playbook coordinates the complete response to a security incident involving multiple teams.

---

### Why are Lookups important?

Lookups provide additional context that helps analysts accurately classify alerts.

---

### What is IOC Enrichment?

IOC Enrichment is the process of gathering intelligence about Indicators of Compromise using internal and external resources.

---

### Name three internal lookup resources.

- Active Directory
- CMDB
- Asset Inventory

---

### Name three Threat Intelligence platforms.

- VirusTotal
- AbuseIPDB
- ThreatFox

---

# Key Takeaways

- Documentation standardizes SOC investigations.
- Workbooks guide alert investigations.
- Runbooks guide operational tasks.
- Playbooks coordinate incident response.
- Lookups provide investigation context.
- IOC Enrichment improves investigation accuracy.
- Threat Intelligence supports SOC decision-making.
- Consistent workflows improve SOC efficiency.
