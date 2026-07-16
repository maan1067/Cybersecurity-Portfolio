# SOC L1 Alert Triage

## Overview

Security Operations Centers (SOCs) rely on alert triage to efficiently identify and respond to potential security incidents. Since enterprise environments generate millions of security events every day, analysts cannot manually review every log. Security monitoring solutions transform relevant events into alerts, enabling analysts to focus on suspicious activities that may indicate malicious behavior.

---

## From Events to Alerts

An **event** is any observable activity occurring within a system, endpoint, application, or network. Examples include:

- User authentication
- Process execution
- File creation or deletion
- Network connections
- Configuration changes

These events are recorded as logs by operating systems, applications, firewalls, cloud platforms, and security tools.

Security monitoring platforms collect these logs and analyze them using detection rules. When suspicious activity matches predefined conditions, the system generates an **alert** for analyst review.

### Event Flow

```text
System Activity
      │
      ▼
Security Event
      │
      ▼
Log Generation
      │
      ▼
Log Collection
      │
      ▼
SIEM / EDR Analysis
      │
      ▼
Alert Generation
      │
      ▼
SOC Analyst Investigation
```

---

## Alert Management Platforms

Several security platforms can generate and manage alerts depending on the organization's architecture.

| Platform | Purpose | Example Technologies |
|----------|---------|----------------------|
| SIEM | Centralized log collection, correlation, and alert management | Splunk Enterprise Security, Elastic Security |
| EDR / NDR | Endpoint and network threat detection | Microsoft Defender, CrowdStrike |
| SOAR | Security orchestration and automated incident response | Splunk SOAR, Cortex XSOAR |
| ITSM | Incident and ticket management | Jira, TheHive |

---

## SOC L1 Analyst Responsibilities

SOC Level 1 analysts are responsible for the initial investigation of security alerts. Their primary objective is to determine whether an alert represents legitimate malicious activity or a benign event.

Typical responsibilities include:

- Reviewing newly generated alerts
- Validating detection accuracy
- Identifying false positives
- Collecting initial evidence
- Escalating confirmed incidents to SOC Level 2 analysts
- Documenting investigation findings

---

## SOC Team Responsibilities

| Role | Responsibility |
|------|----------------|
| SOC L1 Analyst | Monitor, validate, and triage security alerts |
| SOC L2 Analyst | Perform detailed investigations and incident response |
| SOC Engineer | Develop and maintain detection rules and monitoring infrastructure |
| SOC Manager | Monitor operational performance and ensure effective incident handling |

---

## Key Takeaways

- Security events are continuously generated across enterprise systems.
- Logs provide the raw data used for security monitoring.
- SIEM, EDR, and SOAR platforms convert suspicious events into actionable alerts.
- Alert triage reduces analyst workload by prioritizing high-risk activities.
- SOC L1 analysts serve as the first line of defense by identifying and escalating genuine security incidents.
