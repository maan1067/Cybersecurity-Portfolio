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


## Alert Properties

Before investigating any alert, SOC analysts must understand the information presented within it. Although the appearance of alerts varies between SIEM, EDR, and SOAR platforms, most security alerts share a common set of properties that help analysts prioritize, investigate, and document security incidents.

### Alert Time

Indicates when the alert was generated. The alert creation time is usually slightly later than the actual event because logs require time to be collected, processed, correlated, and analyzed before the alert is triggered.

### Alert Name

Provides a concise summary of the detected activity. The alert name is usually based on the detection rule that generated the alert and gives analysts an immediate understanding of the suspicious behavior.

Examples include:

- Unusual Login Location
- Email Marked as Phishing
- Windows RDP Brute Force
- Potential Data Exfiltration

### Alert Severity

Represents the estimated impact or urgency of the alert. Severity levels are typically assigned by detection engineers but may be adjusted during the investigation if additional evidence changes the risk assessment.

Typical severity levels include:

- Informational
- Low
- Medium
- High
- Critical

### Alert Status

Tracks the current state of the investigation and indicates whether an analyst is actively working on the alert or if the investigation has been completed.

Common status values include:

- New
- In Progress
- Pending
- Closed
- Resolved

### Alert Verdict

Represents the analyst's final classification after completing the investigation.

Common verdicts include:

- True Positive
- False Positive

Some organizations also classify alerts as Benign Positive or Suspicious depending on internal procedures.

### Alert Assignee

Identifies the SOC analyst responsible for investigating and documenting the alert. Assigning ownership ensures accountability throughout the investigation process.

### Alert Description

Provides detailed information about the alert, including:

- Detection logic
- Security rationale
- Recommended investigation steps

This section helps analysts understand why the alert was generated and how it should be investigated.

### Alert Fields

Contain the evidence collected when the alert was triggered. These fields vary depending on the detection source but commonly include:

- Hostname
- Username
- IP Address
- Process Name
- Command Line
- File Hash
- Parent Process
- Destination Domain

---

## Alert Prioritization

SOC environments often generate a large number of alerts simultaneously, making it impossible to investigate every alert immediately. Alert prioritization is the process of determining which alerts should be investigated first based on their potential impact and urgency.

An effective prioritization strategy helps SOC analysts focus on the most critical threats, reducing response time and minimizing the risk of overlooking active security incidents.

### Alert Prioritization Workflow

The following approach is commonly used by SOC teams:

1. **Filter Alerts**
   - Exclude alerts that are already assigned, under investigation, or resolved.
   - Focus only on new and unassigned alerts.

2. **Sort by Severity**
   - Investigate Critical alerts first.
   - Continue with High, Medium, and finally Low severity alerts.
   - Higher severity alerts typically indicate a greater potential business impact.

3. **Sort by Time**
   - Prioritize older alerts before newer ones.
   - Older alerts may represent threats that have remained active for a longer period, increasing the likelihood of attacker progression.

### Priority Order

```text
Critical
    ↓
High
    ↓
Medium
    ↓
Low
```

### Investigation Order

```text
New Alerts
      │
      ▼
Filter Assigned & Closed Alerts
      │
      ▼
Sort by Severity
      │
      ▼
Sort by Time
      │
      ▼
Start Investigation
```

### Key Takeaways

- Investigate only new and unassigned alerts.
- Always prioritize higher severity alerts.
- If alerts have the same severity, investigate the oldest alert first.
- Proper prioritization improves incident response efficiency and reduces attacker dwell time.

---

## Alert Triage

Alert triage is the structured process of reviewing, validating, investigating, and classifying security alerts. Its primary objective is to determine whether an alert represents a genuine security incident or normal system activity.

Although terminology varies between organizations, the following terms generally refer to the same operational process:

- Alert Triage
- Alert Investigation
- Alert Analysis
- Alert Handling
- Alert Processing

### Alert Triage Workflow

```text
Receive Alert
      │
      ▼
Assign Alert
      │
      ▼
Change Status to "In Progress"
      │
      ▼
Review Alert Details
      │
      ▼
Perform Investigation
      │
      ▼
Determine Verdict
      │
      ▼
Document Findings
      │
      ▼
Close Alert
```

---

### Phase 1 — Initial Actions

Before beginning the investigation, analysts should:

- Assign the alert to themselves.
- Change the alert status to **In Progress**.
- Review the alert name, description, severity, and available evidence.
- Identify the affected assets and key indicators.

These actions establish ownership and prevent multiple analysts from investigating the same alert simultaneously.

---

### Phase 2 — Investigation

The investigation phase focuses on validating the alert by collecting additional evidence and determining whether malicious activity has occurred.

Typical investigation activities include:

- Identifying the affected user, endpoint, or system.
- Understanding the suspicious activity described by the alert.
- Reviewing related events before and after the alert.
- Correlating additional logs from SIEM or EDR.
- Validating indicators using threat intelligence sources.
- Following internal playbooks or investigation procedures when available.

---

### Phase 3 — Final Actions

After completing the investigation, analysts should:

- Classify the alert as **True Positive** or **False Positive**.
- Document all investigation findings.
- Explain the reasoning behind the final verdict.
- Update the alert status to **Closed**.
- Escalate confirmed security incidents when required.

---

### Key Takeaways

- Alert triage follows a structured and repeatable workflow.
- Proper ownership prevents duplicated investigations.
- Evidence collection is essential before reaching conclusions.
- Every investigation must be documented.
- Confirmed threats should be escalated according to organizational procedures.

---

## Conclusion

Alert triage is a fundamental responsibility of SOC Level 1 analysts and serves as the first stage of incident detection and response. A structured triage process enables analysts to efficiently identify genuine security threats while minimizing the impact of false positives.

Throughout this room, the following core concepts were covered:

- Understanding the difference between events, logs, and alerts.
- Reviewing the essential properties of a security alert.
- Prioritizing alerts based on severity and time.
- Following a structured alert triage workflow.
- Performing investigations using available evidence and threat intelligence.
- Classifying alerts and documenting investigation results.

Mastering these concepts establishes a strong foundation for more advanced SOC activities, including case reporting, incident escalation, threat hunting, and digital forensics.

---

## Skills Gained

- Alert triage fundamentals
- Security event analysis
- Alert prioritization
- SIEM workflow understanding
- Initial incident investigation
- Security documentation
- Evidence-based decision making
- SOC Level 1 operational workflow

---

## Next Learning Objectives

The next stage of SOC analyst training focuses on:

- Writing professional investigation comments
- Case documentation and reporting
- Escalation procedures
- Incident handling by SOC Level 2 analysts
- Advanced investigation techniques
