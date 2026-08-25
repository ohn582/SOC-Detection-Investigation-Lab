# 🛡️ SOC Detection & Investigation Lab

## 📌 Overview

This project demonstrates the design and implementation of a virtual Security Operations Center (SOC) lab using **Splunk Enterprise, Windows 10, Ubuntu, Sysmon, and VMware**.

The lab was built to practice centralized log collection, security monitoring, detection engineering, alert creation, endpoint monitoring, and incident investigation in a controlled environment.

---

## 🎯 Project Objectives

* Build a functional SOC lab environment
* Collect Windows security logs using Splunk Universal Forwarder
* Monitor authentication activity in Splunk
* Create SPL-based detection rules
* Configure automated security alerts
* Build a security monitoring dashboard
* Integrate Sysmon for advanced endpoint telemetry
* Investigate suspicious process and command-line activity
* Practice security event classification and incident analysis

---

## 🖥️ Lab Environment

| Component                  | Purpose                                            |
| -------------------------- | -------------------------------------------------- |
| Windows 10                 | Monitored endpoint                                 |
| Ubuntu                     | Splunk Enterprise SIEM server                      |
| Splunk Enterprise          | Log collection, searching, detection, and analysis |
| Splunk Universal Forwarder | Forwards Windows logs to Splunk                    |
| Sysmon                     | Advanced Windows endpoint telemetry                |
| VMware                     | Virtual lab environment                            |
| PowerShell                 | Controlled security testing                        |

### Data Flow

`Windows 10 → Sysmon → Splunk Universal Forwarder → Splunk Enterprise → Detection & Investigation`

---

## 🔎 Project Phases

### Phase 1 — Network & Splunk Setup

Built the virtual lab and configured Splunk Enterprise as the central SIEM server.

### Phase 2 — Windows Log Forwarding

Configured the Splunk Universal Forwarder and TCP port **9997** to send Windows event logs to the Splunk server.

### Phase 3 — Failed Login Investigation

Detected and analyzed **Windows Event ID 4625** to investigate failed interactive login attempts.

### Phase 4 — Repeated Failed Login Detection

Created an SPL detection rule to identify accounts generating multiple failed authentication attempts.

```spl
index=main sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name, host
| where count >= 3
```

### Phase 5 — Alert Creation

Converted the failed-login detection into an automated Splunk alert for potentially suspicious authentication activity.

### Phase 6 — Dashboard Creation

Created a Windows authentication monitoring dashboard displaying failed logins, successful logins, top accounts with failed attempts, and authentication activity over time.

### Phase 7 — Sysmon Endpoint Monitoring

Integrated Sysmon with Splunk to collect advanced endpoint telemetry, including **Event ID 1 — Process Creation**.

### Phase 8 — Security Event Simulation & Incident Analysis

Generated controlled PowerShell activity on the Windows endpoint and investigated the resulting Sysmon telemetry in Splunk.

The investigation included analysis of:

* Process execution
* Command-line activity
* User context
* Parent process
* Process ID
* Process hashes

**Final Classification:** Authorized / Benign Test Activity
**Severity:** Low / Informational
**Containment Required:** No

---

## 🔬 Example Investigation Workflow

`PowerShell Activity → Sysmon → Universal Forwarder → Splunk → Detection → Investigation → Determination`

The PowerShell execution contained characteristics that warranted investigation, including the use of `-ExecutionPolicy Bypass`. After correlating the command-line telemetry with the controlled lab activity, the event was determined to be authorized test activity.

---

## 🧰 Skills Demonstrated

* Splunk Enterprise
* SPL (Search Processing Language)
* SIEM Monitoring
* Windows Event Logs
* Sysmon
* Security Event Analysis
* Alert Triage
* Detection Engineering
* PowerShell Analysis
* Endpoint Monitoring
* Incident Investigation
* Windows & Linux Administration
* VMware Networking
* Technical Troubleshooting

---

## 📄 Full Project Report

For screenshots, detailed configurations, troubleshooting steps, detection results, and investigation evidence:

**[View Full SOC Lab Report](documentation/SOC-Lab-Full-Report.pdf)**

---

## ⚠️ Disclaimer

All security testing and simulated activity documented in this project was performed within a controlled lab environment for educational and cybersecurity training purposes.
