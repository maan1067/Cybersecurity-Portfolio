# Splunk: The Basics

<p align="center">
  <img src="images/splunk_logo.png" width="250">
</p>

<p align="center">
An introduction to Splunk Enterprise, Security Information and Event Management (SIEM), log analysis, and Security Operations Center (SOC) investigations.
</p>

---

# Overview

Splunk is one of the world's leading Security Information and Event Management (SIEM) platforms. It enables organizations to collect, index, search, analyze, and visualize machine-generated data from servers, endpoints, firewalls, applications, cloud services, and network devices.

Security Operations Centers (SOCs) rely on Splunk to monitor security events, investigate alerts, detect malicious activities, perform threat hunting, and support incident response operations.

Unlike traditional log management systems, Splunk transforms raw machine data into actionable security intelligence through indexing, powerful search capabilities, dashboards, correlation, and reporting.

---

# Learning Objectives

After completing this room, I was able to:

- Understand Splunk architecture
- Explain how Splunk collects and indexes data
- Navigate the Splunk web interface
- Search logs using Splunk Processing Language (SPL)
- Investigate security events
- Understand dashboards and reports
- Perform basic log analysis
- Build simple SPL queries

---

# What is Splunk?

Splunk is a platform designed to collect, process, search, analyze, and visualize machine-generated data.

It can ingest logs from virtually any source, including:

- Windows Event Logs
- Linux Syslog
- Active Directory
- Firewalls
- IDS/IPS
- DNS Servers
- Web Servers
- VPN Appliances
- Cloud Services
- Endpoint Detection & Response (EDR)
- Databases
- Security Appliances

Instead of manually checking logs on hundreds of devices, analysts use Splunk to search and investigate everything from one centralized interface.

---

# Why is Splunk Important?

Modern organizations generate millions of security events every day.

Examples include:

- User logins
- Failed authentication attempts
- File access
- PowerShell execution
- Firewall connections
- DNS requests
- Malware detections
- Process creation
- Registry modifications

Without SIEM, reviewing these events manually would be impossible.

Splunk automates:

- Log Collection
- Indexing
- Searching
- Correlation
- Visualization
- Alerting
- Reporting

---

# Splunk in a SOC Environment

A SOC Analyst spends most of the day interacting with SIEM platforms.

Typical daily tasks include:

- Reviewing alerts
- Investigating suspicious logins
- Searching Windows Event Logs
- Tracking attacker activity
- Finding Indicators of Compromise (IOCs)
- Correlating multiple events
- Supporting Incident Response
- Creating dashboards
- Building detection rules

Splunk serves as the primary investigation platform for many organizations.

---

# Splunk Architecture

<p align="center">
<img src="images/splunk_architecture.png" width="900">
</p>

*Figure 1 – Splunk Architecture*

A typical Splunk deployment contains several major components working together.

```

---

## Universal Forwarder (UF)

The Universal Forwarder is a lightweight software agent installed on endpoints or servers.

Its purpose is to collect log data and securely forward it to Splunk.

Characteristics:

- Very lightweight
- Low CPU usage
- Low memory consumption
- Does not index data
- Does not parse events

Common log sources:

- Windows Event Logs
- Linux Syslog
- IIS Logs
- Apache Logs
- Application Logs

---

## Heavy Forwarder (HF)

The Heavy Forwarder is a full Splunk instance.

Unlike the Universal Forwarder, it can:

- Parse logs
- Filter events
- Modify events
- Route logs
- Perform indexing operations

Organizations typically deploy Heavy Forwarders when advanced preprocessing is required before logs reach the Indexer.

---

## Indexer

The Indexer is the heart of Splunk.

It receives incoming data from Forwarders and performs several important tasks:

- Parses incoming events
- Extracts searchable fields
- Compresses data
- Creates indexes
- Stores searchable events

Without the Indexer, searching data would not be possible.

---

## Search Head

The Search Head is the component that analysts interact with every day.

It provides:

- Search Interface
- Dashboards
- Reports
- Visualizations
- Alert Management

SOC Analysts spend most of their investigation time using the Search Head.

---

## Deployment Server

The Deployment Server centrally manages Splunk Forwarders.

It allows administrators to:

- Push configurations
- Install applications
- Update Forwarders
- Manage hundreds of endpoints simultaneously

---

## License Manager

Splunk licenses are based on daily data ingestion.

The License Manager:

- Tracks daily license usage
- Prevents license violations
- Monitors data volume

Organizations usually purchase licenses according to the amount of log data generated each day.

---

# Splunk Data Flow

```
+-------------+
| Endpoints   |
+-------------+
       │
       ▼
+----------------------+
| Universal Forwarder  |
+----------------------+
       │
       ▼
+-------------+
| Indexer     |
+-------------+
       │
       ▼
+-------------+
| Search Head |
+-------------+
       │
       ▼
+-------------+
| SOC Analyst |
+-------------+
```

This workflow represents how security events travel from endpoints to the analyst responsible for monitoring and investigating threats.

---

# Data Sources

Splunk can ingest logs from a wide range of technologies, including:

| Category | Examples |
|----------|----------|
| Operating Systems | Windows, Linux |
| Firewalls | Palo Alto, Fortinet, Cisco ASA |
| EDR | Microsoft Defender, CrowdStrike, SentinelOne |
| Cloud | AWS, Azure, GCP |
| Identity | Active Directory, Azure AD |
| Email | Microsoft Exchange, Microsoft 365 |
| Web | Apache, Nginx, IIS |
| Databases | MySQL, SQL Server, Oracle |
| Network | Routers, Switches, VPN |

---

# Key Takeaways (Part 1)

- Splunk is one of the most popular SIEM platforms.
- Universal Forwarders collect logs.
- Indexers store and index data.
- Search Heads provide investigation capabilities.
- Splunk centralizes security monitoring across the enterprise.
