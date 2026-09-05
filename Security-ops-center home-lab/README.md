# 🛡️ SOC Home Lab — Phase 1

### Windows Endpoint Monitoring with Splunk & Sysmon

**Author:** Olayemi Daniel Oluwasegun
**Date:** September 2026

---

## 📌 Project Overview

Phase 1 of my **Security Operations Center (SOC) Home Lab**, focused on building an endpoint monitoring and centralized log analysis environment.

The lab uses a **Windows 10 virtual machine** as the monitored endpoint, **Sysmon** for detailed endpoint telemetry, and **Splunk Enterprise** as the central SIEM.

The environment was built and validated step-by-step to ensure logs were being **generated, collected, forwarded, indexed, and made searchable** rather than simply confirming that each service was running.

### 🏗️ Environment

* **Windows 10 VM** → Monitored endpoint
* **Sysmon** → Endpoint telemetry
* **Splunk Universal Forwarder** → Log collection and forwarding
* **Splunk Enterprise** → Central SIEM
* **Kali Linux VM** → Reserved for attack simulation in Phase 2
* **VMware Workstation** → Virtualization platform

---

## 🎯 Objectives

* Deploy a Windows 10 endpoint in VMware Workstation
* Configure Splunk Enterprise as the central SIEM
* Install and configure the Splunk Universal Forwarder
* Deploy Sysmon using the **SwiftOnSecurity configuration**
* Forward Windows and Sysmon logs to Splunk
* Configure log forwarding over **TCP 9997**
* Validate end-to-end log ingestion
* Investigate and document configuration issues
* Establish the foundation for future detection and incident-response activities

---

## 🧰 Tools & Technologies

| Category             | Technology                 |
| -------------------- | -------------------------- |
| Endpoint             | Windows 10                 |
| SIEM                 | Splunk Enterprise          |
| Log Forwarder        | Splunk Universal Forwarder |
| Endpoint Monitoring  | Sysmon                     |
| Sysmon Configuration | SwiftOnSecurity            |
| Virtualization       | VMware Workstation         |
| Attack Simulation    | Kali Linux                 |
| Query Language       | SPL                        |
| Forwarding Port      | TCP 9997                   |

---

## 🏗️ Lab Architecture

```text
                 ┌──────────────────────┐
                 │     Windows 10 VM    │
                 │     Monitored Host   │
                 │                      │
                 │  ┌────────────────┐  │
                 │  │     Sysmon     │  │
                 │  │ Endpoint Data  │  │
                 │  └───────┬────────┘  │
                 │          │           │
                 │  ┌───────▼────────┐  │
                 │  │ Splunk UF      │  │
                 │  │ Log Forwarder  │  │
                 │  └───────┬────────┘  │
                 └──────────┼───────────┘
                            │
                        TCP 9997
                            │
                            ▼
                 ┌──────────────────────┐
                 │   Splunk Enterprise  │
                 │       Central SIEM   │
                 └──────────┬───────────┘
                            │
                            ▼
                    Log Analysis &
                    Security Monitoring
```

---

## 📂 Project Walkthrough

Each stage of the lab is documented separately with configuration steps, validation, screenshots, and troubleshooting.

| Phase | Documentation                                                                                                                     |
| ----- | --------------------------------------------------------------------------------------------------------------------------------- |
| 01    | [Windows VM Setup](Windows%20VM%20Setup.md)                                                                                       |
| 02    | [Splunk Enterprise Installation](Splunk%20Enterprise%20Installation.md)                                                           |
| 03    | [Splunk Universal Forwarder Installation & Configuration](Splunk%20Universal%20Forwarder%20Installation%20and%20Configuration.md) |
| 04    | [Sysmon Installation & Configuration](Sysmon%20Installation%20and%20Configuration.md)                                             |
| 🔎    | [Troubleshooting: Sysmon Forwarding Issue](Troubleshooting%20-%20Sysmon%20Forwarding%20Issue.md)                                  |

---

## ✅ Results

### Successfully Implemented

* ✅ Windows 10 endpoint deployed
* ✅ Splunk Enterprise configured as the central SIEM
* ✅ Splunk Universal Forwarder installed and configured
* ✅ Endpoint-to-Splunk connectivity established
* ✅ Windows Security and System logs successfully forwarded
* ✅ Windows events indexed and searchable in Splunk
* ✅ Sysmon successfully installed
* ✅ SwiftOnSecurity configuration applied
* ✅ Sysmon confirmed to be generating endpoint telemetry locally

### ⚠️ Issue Identified

During validation, **Sysmon events were being generated successfully on the Windows endpoint but were not appearing in Splunk**.

Since standard Windows logs were already reaching Splunk, the investigation was narrowed to the **Sysmon-specific collection and forwarding configuration**.

Rather than treating the lab as complete because the services were running, the issue was documented and investigated as part of the project.

👉 [View the Sysmon Forwarding Troubleshooting Write-up](Troubleshooting%20-%20Sysmon%20Forwarding%20Issue.md)

---

## 🔐 Skills Demonstrated

* SIEM deployment and configuration
* Windows endpoint monitoring
* Sysmon deployment and configuration
* Splunk Universal Forwarder configuration
* Windows Event Log collection
* Log forwarding architecture
* SPL search fundamentals
* Security event validation
* Endpoint telemetry analysis
* Evidence-based troubleshooting
* Security monitoring
* Technical documentation

---

## 💡 Key Takeaway

A successful installation does not automatically mean a functional monitoring pipeline.

This phase was validated across the complete flow:

**Event Generation → Collection → Forwarding → Ingestion → Searchability**

The troubleshooting process reinforced the importance of validating each stage of a SOC logging pipeline rather than relying only on service status.

---

## 🚀 Next Steps

### Phase 2

* 🔧 Resolve the Sysmon-to-Splunk forwarding issue
* 🔎 Validate additional Sysmon event types
* 🐉 Introduce the Kali Linux VM
* 🎯 Simulate controlled attacks against the Windows endpoint
* 📊 Analyze the resulting telemetry in Splunk
* 🚨 Build detection searches and correlation rules
* 📈 Develop SOC dashboards
* 🔍 Perform alert triage and incident investigation

---

### 🛡️ Project Focus

**Endpoint Visibility → Centralized Logging → Threat Detection → Investigation**

> Building a practical SOC environment through hands-on security monitoring, investigation, and detection.
.
---

## Table of Contents
- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Tools Used](#tools-used)
- [Lab Architecture](#lab-architecture)
- [Walkthrough](#walkthrough)
- [Results (So Far)](#results-so-far)
- [Skills Demonstrated](#skills-demonstrated)
- [Next Steps](#next-steps)

---

## Objectives

- Set up a Windows 10 virtual machine in VMware Workstation to serve as the monitored endpoint
- Install and configure Splunk Enterprise on the host machine to act as the central SIEM
- Install the Splunk Universal Forwarder on the Windows VM to transmit log data to Splunk
- Install Sysmon on the Windows VM with the SwiftOnSecurity configuration for high-quality, low-noise event logging
- Configure log forwarding between the VM and Splunk Enterprise over the standard Splunk-to-Splunk port (9997)
- Verify that logs are actually being generated, forwarded, and searchable — not just that services report as running
- Diagnose and document any issues encountered along the way, rather than only presenting a clean end result

## Tools Used

| Component | Technology |
|----------|------------|
| Monitored Endpoint | Windows 10 (VMware Workstation) |
| SIEM Platform | Splunk Enterprise (host machine) |
| Log Forwarding Agent | Splunk Universal Forwarder |
| Endpoint Telemetry | Sysmon (SwiftOnSecurity configuration) |
| Future Attack Simulation | Kali Linux |
## Lab Architecture

The diagram below shows how the components in this lab relate to one another. The Windows 10 VM sits inside VMware Workstation and runs two things side by side: Sysmon, which watches the operating system and generates detailed telemetry (process creation, file creation, network connections, and more), and the Splunk Universal Forwarder, which is responsible for reading both Sysmon's event log and the standard Windows Event Logs (Security, System, Application) and shipping that data off the VM. The Forwarder sends everything over TCP port 9997 to Splunk Enterprise, which runs on the host machine outside the VM and is responsible for indexing the data and making it searchable.

<p align="center">
  <img src="figure01_architecture.png" width="900" alt="SOC home lab architecture">
</p>

<p align="center"><em>Figure 1. Log flow from the Windows 10 VM to Splunk Enterprise on the host machine.</em></p>
## Walkthrough

This project is documented as a set of linked, focused write-ups rather than one long file. Each one covers a single stage of the pipeline in full detail, with screenshots.

1. [Windows VM Setup](Windows%20VM%20Setup.md) — building the monitored endpoint in VMware Workstation
2. [Splunk Enterprise Installation](Splunk%20Enterprise%20Installation.md) — standing up the SIEM on the host machine
3. [Splunk Universal Forwarder Installation & Configuration](Splunk%20Universal%20Forwarder%20Installation%20and%20Configuration.md) — connecting the VM to Splunk Enterprise
4. [Sysmon Installation & Configuration](Sysmon%20Installation%20and%20Configuration.md) — adding high-quality endpoint telemetry with the SwiftOnSecurity config
5. [Troubleshooting: Sysmon Forwarding Issue](Troubleshooting%20-%20Sysmon%20Forwarding%20Issue.md) — a real configuration issue found and worked through during validation

## Results (So Far)

- Windows VM, Splunk Enterprise, and the Splunk Universal Forwarder were successfully deployed and connected end-to-end
- General Windows Event Log data (Security, System) is confirmed flowing into Splunk and is fully searchable
- Sysmon is confirmed to be correctly installed and actively generating detailed local telemetry (Event ID 11 and others), using the SwiftOnSecurity configuration
Sysmon telemetry is confirmed to be generated locally; however, Sysmon events are not yet being indexed in Splunk despite successful forwarding of standard Windows Event Logs. The investigation and troubleshooting process is documented in the dedicated troubleshooting write-up. — see the [troubleshooting write-up](Troubleshooting%20-%20Sysmon%20Forwarding%20Issue.md) for details

## Skills Demonstrated

- SIEM deployment and configuration (Splunk Enterprise)
- Windows Universal Forwarder setup, configuration, and troubleshooting
- Sysmon deployment using a community-maintained configuration (SwiftOnSecurity)
- Log forwarding architecture and configuration (TCP 9997, inputs.conf)
- SPL (Search Processing Language) search fundamentals for validating data ingestion
- Systematic, evidence-based troubleshooting of a log pipeline issue rather than guesswork
- Clear technical documentation of both successes and unresolved issues

## Next Steps

- Resolve the Sysmon-to-Splunk forwarding issue and confirm Sysmon events are fully searchable in Splunk
- **Phase 2:** introduce the Kali Linux VM to simulate attacks against the Windows endpoint
- Build detection searches, correlation rules, and dashboards in Splunk based on the telemetry captured from simulated attack activity
