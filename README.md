# Splunk SOC Detection Engineering & Threat Hunting Lab

## Project Overview

This project is a hands-on Security Operations Center (SOC) laboratory built with Splunk Enterprise.

The lab demonstrates an end-to-end security monitoring and detection workflow using Windows Security authentication telemetry.

The project covers:

- Windows Security event telemetry
- Splunk data ingestion and indexing
- SPL-based detection engineering
- Authentication monitoring
- Failed authentication detection
- Multiple failed authentication investigation
- Successful authentication analysis
- Incident investigation
- Source IP investigation
- MITRE ATT&CK mapping
- SOC dashboard development
- Security monitoring and investigation documentation

## Project Objective

The objective of this laboratory is to demonstrate practical SOC analyst and detection engineering capabilities by progressing from raw security telemetry through detection, investigation, analysis, MITRE ATT&CK mapping, and security monitoring.

## Technology Stack

| Technology | Purpose |
|---|---|
| Splunk Enterprise | SIEM and security analytics |
| SPL | Detection and investigation queries |
| Windows Security Events | Authentication telemetry |
| MITRE ATT&CK | Adversary technique mapping |
| Dashboard Studio | SOC monitoring dashboard |
| GitHub | Project documentation and portfolio |

## Project Workflow

```text
Windows Security Telemetry
        ↓
Splunk Index
        ↓
Detection Engineering
        ↓
Authentication Investigation
        ↓
Source IP Investigation
        ↓
MITRE ATT&CK Mapping
        ↓
SOC Dashboard
        ↓
Incident Documentation
        ↓
GitHub Portfolio
```

## Detection Engineering

The project contains three authentication-focused detections:

### DET-001 — Windows Failed Authentication

Detects Windows failed authentication events using EventCode 4625.

### DET-002 — Multiple Failed Authentication Attempts

Identifies repeated failed authentication activity that may require further investigation.

### DET-003 — Successful Authentication After Multiple Failures

Identifies a successful authentication event following multiple failed authentication attempts.

The detections demonstrate how authentication telemetry can be transformed into actionable SOC monitoring logic.

## Incident Investigation

### INC-001 — John Authentication Incident Investigation

The investigation examined authentication activity associated with the user account `John`.

Observed authentication sequence:

```text
4625 → 4625 → 4625 → 4624
```

The investigation identified:

- Three failed authentication attempts
- One successful authentication
- Source IP: `192.168.1.75`
- All four events associated with the `John` account
- Successful authentication occurring after the preceding failed attempts

The available laboratory evidence does not independently establish malicious activity or account compromise.

## MITRE ATT&CK Mapping

The authentication pattern was mapped to:

**Technique:** T1110 — Brute Force

**Tactic:** Credential Access

The mapping represents a relevant detection and investigation context.

It does not by itself establish that a brute-force attack occurred.

## SOC Dashboard

### SOC Authentication Monitoring Dashboard

The project includes a Splunk Dashboard Studio dashboard designed to monitor Windows authentication activity.

Dashboard features include:

- Global time range
- Total authentication events
- Failed versus successful authentication monitoring
- Authentication activity visualization
- Support for SOC detection validation and investigation

The dashboard uses the:

```text
windows_security
```

Splunk index.

## Dataset

The laboratory uses a controlled Windows Security authentication dataset.

Primary dataset:

```text
windows_security_events.csv
```

The dataset is intended for educational and laboratory demonstration purposes.

## Investigation SPL

Example authentication investigation query:

```spl
index=windows_security User=John
| sort 0 _time
| table _time EventCode User Source_IP Action Status
```

Source IP investigation:

```spl
index=windows_security Source_IP=192.168.1.75
| sort 0 _time
| table _time EventCode User Source_IP Action Status
```

## Project Artifacts

The repository contains documentation for:

- Detection Engineering
- Incident Investigation
- MITRE ATT&CK Mapping
- SOC Authentication Monitoring Dashboard
- Windows Security authentication telemetry

## Investigation Limitations

This project uses a controlled laboratory dataset.

The available telemetry is sufficient to demonstrate the SOC detection and investigation workflow but is not sufficient to establish attacker intent or confirm account compromise.

A real-world investigation would normally require additional telemetry such as:

- Endpoint and process telemetry
- Network telemetry
- Account-management events
- Privileged-account activity
- EDR telemetry
- Authentication source and destination information
- Additional security alerts

## Disclaimer

This project is an educational cybersecurity laboratory created for security monitoring, detection engineering, threat hunting, and SOC investigation practice.

All authentication activity represented in this repository is laboratory data.

## Author

**Nzute Joseph Onyekachukwu**

Cybersecurity | IT Infrastructure | SOC Detection Engineering

GitHub: `JonzutCyberTech`
