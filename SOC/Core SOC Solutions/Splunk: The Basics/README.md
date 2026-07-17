# Splunk: The Basics

## Overview

Splunk is one of the most widely used Security Information and Event Management (SIEM) platforms. It enables organizations to collect, index, search, monitor, and analyze machine-generated data from different sources in real time.

In this lab, I explored the core architecture of Splunk, learned how logs are ingested into the platform, and performed basic investigations using the Search Processing Language (SPL).

---

## Learning Objectives

After completing this lab, I was able to:

- Understand the Splunk architecture.
- Identify the role of each Splunk component.
- Navigate the Splunk interface.
- Upload log files into Splunk.
- Create custom indexes.
- Search and analyze logs using SPL.
- Perform simple SOC investigations.

---

# Lab Environment

Platform: TryHackMe

Room: Splunk: The Basics

Category: SIEM

Difficulty: Easy

---

# Splunk Architecture

Splunk consists of three primary components.

## Splunk Forwarder

The Forwarder is a lightweight agent installed on endpoints. Its purpose is to collect logs and securely forward them to the Splunk Indexer.

Typical log sources include:

- Windows Event Logs
- Sysmon Logs
- Linux Logs
- Web Server Logs
- Database Logs

### Responsibilities

- Collect logs
- Compress data
- Forward logs
- Consume minimal system resources

---

## Splunk Indexer

The Indexer receives raw logs from Forwarders.

Its responsibilities include:

- Parsing logs
- Normalizing data
- Creating searchable events
- Storing indexed data

The Indexer transforms raw machine data into searchable information.

---

## Splunk Search Head

The Search Head provides the interface analysts use to investigate security events.

Using SPL (Search Processing Language), analysts can:

- Search logs
- Filter events
- Create reports
- Build dashboards
- Investigate incidents

---

# Splunk Interface

The Splunk Home page contains several important sections.

## Splunk Bar

Provides access to:

- Messages
- Settings
- Activity
- Help
- Search

---

## Apps Panel

Displays installed Splunk applications.

The default application is:

- Search & Reporting

---

## Explore Splunk

Quick shortcuts for:

- Add Data
- Install Apps
- Documentation

---

## Dashboards

Dashboards provide visual representations of security events.

They help SOC analysts monitor activity using charts and statistics.

---

# Data Ingestion

Splunk supports collecting data from multiple sources including:

- Windows Event Logs
- Linux Logs
- Firewall Logs
- VPN Logs
- Web Server Logs
- JSON Files
- Syslog

During this lab, a VPN log file was uploaded.

The ingestion process consisted of:

1. Selecting the source file.
2. Selecting the source type (JSON).
3. Configuring the host value.
4. Creating a new index named VPN_Logs.
5. Reviewing the configuration.
6. Uploading the logs.

---

# Practical Investigation

## Total Events

After uploading the VPN log file:

**Total Events:** 2862

---

## User Investigation

Query

```spl
source="VPNlogs.json" host="VPN_Connections" index="vpn_logs" sourcetype="_json" UserName=Maleena
```

Result

- 60 Events

---

## Source IP Investigation

Query

```spl
source="VPNlogs.json" host="VPN_Connections" index="vpn_logs" sourcetype="_json" Source_ip="107.14.182.38"
```

Result

- Username: Smith

---

## Country Investigation

Query

```spl
source="VPNlogs.json" host="VPN_Connections" index="vpn_logs" sourcetype="_json" Source_Country!=France
```

Result

- 2814 Events

---

## VPN Events by IP

Query

```spl
source="VPNlogs.json" host="VPN_Connections" index="vpn_logs" sourcetype="_json" Source_ip="107.3.206.58"
```

Result

- 14 Events

---

# Skills Gained

- Splunk Navigation
- Log Ingestion
- Index Management
- SPL Fundamentals
- Log Investigation
- Event Filtering
- Basic SIEM Operations

---

# Key Takeaways

- Learned the basic architecture of Splunk.
- Understood how data flows from endpoints to searchable events.
- Practiced uploading logs into Splunk.
- Used SPL queries to investigate VPN logs.
- Performed basic SOC analyst tasks within a SIEM platform.
