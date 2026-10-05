# 🛡️ Wazuh SOC Home Lab

> **A hands-on SOC environment for endpoint monitoring, security telemetry analysis, alert triage, threat detection, and investigation.**

I built this home lab to develop practical **Security Operations Center (SOC)** and Blue Team skills using **Wazuh**.

The environment consists of a centralized Wazuh server monitoring both **Windows and Linux endpoints**. I use the lab to generate and investigate security telemetry, analyze Windows security events, correlate related activity, perform alert triage, and document findings using a SOC-style investigation workflow.

Rather than only deploying Wazuh, this project focuses on **using the platform to investigate security activity and turn raw telemetry into an analyst conclusion**.

---

# 🎯 Project Objectives

The main objectives of this project were to:

* Deploy an all-in-one **Wazuh Manager, Indexer, and Dashboard**
* Configure Windows and Linux endpoints as Wazuh agents
* Collect and analyze endpoint security telemetry
* Monitor Windows Security Events and endpoint activity
* Investigate Wazuh alerts and security events
* Practice SOC alert triage and investigation workflows
* Correlate multiple events to understand attack activity
* Map investigated activity to **MITRE ATT&CK**
* Practice threat hunting using Wazuh Discover
* Document investigations as repeatable SOC case studies
* Build practical cybersecurity evidence for a SOC Analyst portfolio

---

# 🏗️ Lab Architecture

All systems run as virtual machines using **VMware Workstation** and communicate over the same virtual network.

## Environment

| Machine                     | Operating System          | IP Address       | Role                               |
| --------------------------- | ------------------------- | ---------------- | ---------------------------------- |
| Wazuh-Server                | Ubuntu Server             | Wazuh Server IP  | Wazuh Manager, Indexer & Dashboard |
| delucky-windows — Agent 001 | Windows 10 Pro 10.0.19045 | `192.168.89.131` | Monitored Windows endpoint         |
| Delucky-Linux — Agent 002   | Ubuntu 24.04.5 LTS        | `192.168.89.130` | Monitored Linux endpoint           |

**Wazuh Version:** `4.14.7`
**Virtualization:** VMware Workstation
**Network:** `192.168.89.0/24`

## Architecture Overview

```text
                         ┌───────────────────────┐
                         │      SOC Analyst      │
                         │       Browser         │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │   Wazuh Dashboard    │
                         │                       │
                         │  Alert Triage         │
                         │  Threat Hunting       │
                         │  Log Investigation    │
                         └───────────┬───────────┘
                                     │
                                     ▼
                 ┌────────────────────────────────────┐
                 │            Wazuh Server             │
                 │                                    │
                 │  Wazuh Manager                     │
                 │  Wazuh Indexer                     │
                 │  Wazuh Dashboard                   │
                 └─────────────────┬──────────────────┘
                                   │
                     ┌─────────────┴─────────────┐
                     │                           │
                     ▼                           ▼
          ┌─────────────────────┐     ┌─────────────────────┐
          │    Windows Agent    │     │     Linux Agent     │
          │                     │     │                     │
          │ Windows 10 Pro      │     │ Ubuntu 24.04        │
          │ Agent 001           │     │ Agent 002           │
          └─────────────────────┘     └─────────────────────┘
```

### Virtual Machine Environment

![VMware Virtual Machine Environment](https://github.com/DeluckyOG/wazuh-soc-home-lab/blob/b235cd4bc88d8852f9ad1b3689329ed86e9ae6c0/my%20virtual%20machine.png)

> **Figure 1 — VMware Workstation environment used to host the Wazuh server and monitored endpoints.**

---

# 🧰 Tools & Technologies

| Technology             | Purpose                                                |
| ---------------------- | ------------------------------------------------------ |
| **Wazuh 4.14.7**       | Security monitoring, detection and endpoint visibility |
| **Wazuh Manager**      | Event processing and analysis                          |
| **Wazuh Indexer**      | Security telemetry storage and search                  |
| **Wazuh Dashboard**    | Alert monitoring and investigation                     |
| **Windows 10 Pro**     | Monitored Windows endpoint                             |
| **Ubuntu 24.04 LTS**   | Monitored Linux endpoint                               |
| **Ubuntu Server**      | Wazuh server                                           |
| **VMware Workstation** | Virtualization                                         |
| **Windows Event Logs** | Windows security telemetry                             |
| **SCA**                | Security Configuration Assessment                      |
| **FIM**                | File Integrity Monitoring                              |
| **MITRE ATT&CK**       | Adversary behavior and technique mapping               |

---

# ⚙️ Lab Deployment

## 1. Wazuh Server

I created an Ubuntu Server virtual machine and deployed Wazuh as an all-in-one environment.

The server provides:

* Wazuh Manager
* Wazuh Indexer
* Wazuh Dashboard
* Security event processing
* Alert generation
* Endpoint monitoring
* Security telemetry search and analysis

This provided a centralized platform for monitoring the endpoints in the lab.

---

## 2. Endpoint Enrollment

I enrolled two endpoints into the Wazuh environment:

* **Windows 10 Pro — Agent 001**
* **Ubuntu 24.04 — Agent 002**

![Wazuh Agent Dashboard](https://github.com/DeluckyOG/wazuh-soc-home-lab/blob/9cb6051f63636af18b46411941d35a2d113af417/my%20wazuh%20agent%20dashboard.png)

> **Figure 2 — Wazuh agent dashboard showing the Windows and Linux endpoints connected to the monitoring environment.**

The endpoints provide centralized visibility into operating-system activity and security telemetry.

---

# 📊 Security Telemetry

After onboarding the endpoints, I monitored the telemetry generated by the Windows and Linux systems.

During one observation period, the environment generated approximately:

* **~2,900 Linux events over 24 hours**
* **~2,300 Windows events over 24 hours**

The telemetry included system activity, security events, configuration information, process-related information, and Windows event logs.

This helped me understand an important SOC concept:

> **High event volume does not automatically mean high severity.**

A SOC analyst must identify which events require investigation and which represent normal system activity.

---

# 🐧 Linux Endpoint Monitoring

The Ubuntu endpoint generated security telemetry that could be reviewed centrally through the Wazuh Dashboard.

The environment also provided **Security Configuration Assessment (SCA)** visibility, allowing me to review aspects of the endpoint's security configuration and posture.

![Linux Wazuh Alerts](https://github.com/DeluckyOG/wazuh-soc-home-lab/blob/7ad64b94a4b0bd0f7775c4cdcb27537a343f469b/my%20wazuh%20linux%20aleart%20dashboad.png)

> **Figure 3 — Wazuh Dashboard displaying telemetry and alerts from the Linux endpoint.**

This gave me practical experience monitoring Linux security telemetry from a centralized SOC platform.

---

# 🪟 Windows Endpoint Monitoring

The Windows endpoint generated approximately **2,300 events over 24 hours** during the documented observation period.

The telemetry included Windows security events and process-related information such as:

* Process paths
* Process IDs
* User information
* Process GUIDs
* Windows Security Event IDs

![Windows Wazuh Alerts](https://github.com/DeluckyOG/wazuh-soc-home-lab/blob/73ad2bc40a76ca0c284318dc8e1d4a5179d21da2/my%20wazuh%20windows%20alert%20dashboard.png)

> **Figure 4 — Wazuh Dashboard displaying Windows endpoint security events and alerts.**

This telemetry became the foundation for the Windows detection investigations documented below.

---

# 🔎 Detection & Investigation

The primary purpose of this lab is not simply to collect logs.

I use the telemetry to practice a SOC investigation process:

```text
Endpoint Activity
       ↓
Security Telemetry
       ↓
Detection / Alert
       ↓
Initial Triage
       ↓
Event Analysis
       ↓
Context Gathering
       ↓
Event Correlation
       ↓
Threat Assessment
       ↓
Analyst Verdict
       ↓
Document Findings
```

This process helps me move from:

> **"An event occurred."**

to:

> **"I understand what happened, who performed it, what was affected, how the events relate to each other, and whether the activity requires escalation."**

---

# 🕵️ SOC Investigation Case Studies

## Case Study 1 — Unauthorized Local Admin Account

### Create → Privilege Escalation → Delete

I performed a controlled simulation on the Windows endpoint to reproduce a suspicious account-management sequence:

1. Create a new local user
2. Add the account to the local Administrators group
3. Verify the privilege assignment
4. Delete the account

The simulation was performed in my own isolated lab environment.

### Simulated Activity

```powershell
net user Student1 /add
net localgroup administrators Student1 /add
net localgroup administrators
net user Student1 /delete
```

The activity generated Windows Security telemetry that could then be investigated through Wazuh.

---

## 🔍 Step 1 — Local Account Creation

**Windows Event ID:** `4720`

**Wazuh Discover query:**

```text
data.win.system.eventID: 4720
```

The event recorded the creation of the `Student1` account.

The event identified:

* **Actor:** `Gboy`
* **Target:** `Student1`
* **Logon ID:** `0x164095`
* **Target SID:** SID ending in `-1004`

This established the first stage of the activity.

---

## 🔍 Step 2 — Account Added to Administrators

**Windows Event ID:** `4732`

**Wazuh Discover query:**

```text
data.win.system.eventID: 4732
```

The event indicated that a member was added to a security-enabled local group.

The targeted group was:

```text
Administrators
S-1-5-32-544
```

The member was represented by its SID rather than directly displaying the username.

I correlated the member SID with the SID recorded during the `4720` account-creation event to identify the account as `Student1`.

This demonstrates an important investigation technique:

> **When an event does not provide a useful username, related events and unique identifiers such as SIDs can be used to establish context.**

---

## 🔍 Step 3 — Account Deletion

**Windows Event ID:** `4726`

**Wazuh Discover query:**

```text
data.win.system.eventID: 4726
```

The event showed that the `Student1` account was deleted.

The event identified:

* **Target:** `Student1`
* **Actor:** `Gboy`

This completed the sequence:

```text
4720
Account Created
     ↓
4732
Added to Administrators
     ↓
4726
Account Deleted
```
![image alt](https://github.com/DeluckyOG/wazuh-soc-home-lab/blob/08174da8339fa682d7b67f3a76d56c3037e76b66/powershell.png)
---

# 🧩 Event Correlation

The individual events become more meaningful when correlated.

### Pivot 1 — Actor and Logon ID

The events were associated with:

```text
Actor: Gboy
Logon ID: 0x164095
```

The shared Logon ID provided a pivot for investigating activity associated with the same logon session.

### Pivot 2 — Target SID

The `Student1` account could be correlated across the events using its SID, including the `4732` event where the account name was not directly displayed.

### Pivot 3 — Timeline

The events occurred within a short period, creating a sequence consistent with deliberate hands-on-keyboard or scripted account-management activity.

---

# 📋 Investigation Timeline

| Stage | Event ID | Activity                            | Actor | Target                 |
| ----- | -------: | ----------------------------------- | ----- | ---------------------- |
| 1     |     4720 | Local account created               | Gboy  | Student1               |
| 2     |     4732 | Added to local Administrators group | Gboy  | Student1 / SID `-1004` |
| 3     |     4726 | Local account deleted               | Gboy  | Student1               |

> **Note:** Exact timestamps and Wazuh rule IDs should be recorded directly from the corresponding Wazuh events.

---

# 🧠 MITRE ATT&CK Mapping

The simulated activity can be associated with the following ATT&CK techniques:

| Technique                     | ID            | Relevance                                |
| ----------------------------- | ------------- | ---------------------------------------- |
| Create Account: Local Account | **T1136.001** | Creation of the `Student1` local account |
| Account Manipulation          | **T1098**     | Adding the account to a privileged group |

The mapping should be validated against the exact Wazuh/MITRE information associated with the alerts before treating the mapping as authoritative.

---

# 🚨 Analyst Verdict

### **Verdict: Suspicious — Escalate for Validation**

In a production environment, the sequence would warrant investigation because a local account was:

1. Created
2. Added to a privileged Administrators group
3. Deleted shortly afterward

This behavior could represent unauthorized account creation, privilege escalation, or cleanup activity.

Because this was a controlled simulation in my own lab, the activity was authorized. However, I investigated it using the same reasoning I would apply to a potentially suspicious production alert.

### Recommended SOC Actions

If the same activity occurred unexpectedly on a production endpoint:

1. Validate the activity with the system owner or change records.
2. Pivot on the associated Logon ID.
3. Review additional activity performed by the actor account.
4. Determine whether the temporary account was used for authentication.
5. Search for additional persistence or privilege changes.
6. If unauthorized, follow the organization's containment and credential-reset procedures.

---

# 🛠️ Detection Engineering Opportunities

The investigation also identified opportunities for improving detection coverage.

### 1. Monitor privileged group membership changes

Create a Wazuh detection that gives increased attention to Event ID `4732` when the target group is:

```text
S-1-5-32-544
```

which corresponds to the local Administrators group.

### 2. Correlate account creation with privilege assignment

A stronger detection could correlate:

```text
4720 → 4732
```

for the same newly created account.

### 3. Detect rapid account creation and deletion

A short-lived account that is created, privileged, and deleted may warrant additional investigation.

A potential correlation sequence is:

```text
4720 → 4732 → 4726
```

---

# 📊 Wazuh Dashboard & Security Monitoring

The Wazuh Dashboard provided centralized visibility into the monitored environment.

During the project I worked with capabilities including:

* Security alerts
* Security Configuration Assessment
* File Integrity Monitoring
* Endpoint monitoring
* Windows security telemetry
* Linux security telemetry
* Threat hunting
* MITRE ATT&CK visibility

![Wazuh Security Dashboard](https://github.com/DeluckyOG/wazuh-soc-home-lab/blob/e38e26e8dcdc460f8be56c441246601db96f6a4b/my%20wazuh%20dash%20board.png)

> **Figure 5 — Wazuh overview dashboard providing centralized visibility into endpoint health, alerts, and security monitoring capabilities.**

At the time of documentation, the environment displayed:

| Severity | Alerts |
| -------- | -----: |
| Critical |      0 |
| High     |      0 |
| Medium   |      1 |
| Low      |     31 |

These values represent the state of the dashboard at the time the screenshot was captured and are not intended to represent the total volume of telemetry collected by the environment.

---

# 🧪 Investigation Skills Practiced

Through this lab I have practiced:

### SIEM & Monitoring

* Wazuh deployment
* Agent enrollment
* Centralized security monitoring
* Security telemetry collection
* Alert triage
* Log analysis

### Windows Security Investigation

* Windows Security Event analysis
* Event ID investigation
* Account-management investigation
* Privileged group membership investigation
* Process telemetry analysis
* SID correlation
* Logon ID correlation

### Linux Monitoring

* Linux endpoint monitoring
* Linux security telemetry analysis
* Security Configuration Assessment

### SOC Investigation

* Initial triage
* Event correlation
* Timeline construction
* Pivoting using unique identifiers
* Threat assessment
* Analyst verdicts
* Detection improvement

---

# 🧠 Key Lessons Learned

## 1. Telemetry must be interpreted in context

An individual security event does not always provide enough information to determine whether activity is malicious.

Correlating multiple events provides a much stronger picture.

## 2. Unique identifiers are valuable investigation pivots

SIDs and Logon IDs can connect events even when usernames or other descriptive fields are missing.

## 3. Event volume and severity are different things

An endpoint may generate thousands of events while only a small number require immediate investigation.

SOC analysts therefore need to prioritize activity based on context and risk.

## 4. Detection is only the beginning

A useful SOC workflow does not stop when an alert appears.

The analyst must determine:

```text
What happened?
Who performed it?
What was affected?
When did it happen?
What happened before and after?
Is the activity expected?
What should happen next?
```

## 5. Documentation is part of the investigation

Recording the evidence, investigation steps, correlation logic, and final verdict makes an investigation repeatable and easier for another analyst to understand.

---

# 🧩 Challenges & Problem Solving

Building this environment required troubleshooting several areas, including:

* Virtual machine networking
* Wazuh server deployment
* Agent enrollment
* Endpoint connectivity
* Understanding event collection
* Navigating the Wazuh Dashboard
* Working with large volumes of telemetry
* Understanding the difference between events and alerts
* Investigating Windows Security Event data

These challenges helped me move beyond simply installing a security platform and begin understanding how endpoint telemetry is collected, processed, searched, and investigated.

---

# 📂 Repository Structure

```text
wazuh-soc-home-lab/
│
├── README.md
│
├── case-studies/
│   │
│   ├── case-01-unauthorized-local-admin/
│   │   ├── README.md
│   │   └── screenshots/
│   │       ├── 01-commands-run.png
│   │       ├── 02-event-4720.png
│   │       ├── 03-event-4732.png
│   │       └── 04-event-4726.png
│   │
│   └── case-02/
│       └── README.md
│
├── configs/
│   └── sanitized/
│
└── screenshots/
    └── architecture/
```

The repository structure separates the main project documentation from detailed investigation evidence.

---

# 🔐 Security & Privacy

This repository does **not** intentionally contain:

* Passwords
* API keys
* Agent authentication keys
* Access tokens
* Private credentials
* Sensitive personal information

Any configuration files published to the repository should be sanitized before committing them.

---

# 🚀 Future Improvements

Planned improvements include:

* Develop custom Wazuh detection rules
* Develop custom decoders where appropriate
* Create additional controlled attack simulations
* Expand MITRE ATT&CK detection coverage
* Configure and test Active Response
* Integrate threat intelligence
* Develop additional Windows detections
* Develop additional Linux detections
* Create more SOC investigation case studies
* Improve event correlation
* Build a larger SOC-style detection environment
* Document detection engineering decisions

---

# 🎯 Project Goal

The long-term goal of this project is to continuously develop practical **SOC Analyst and Blue Team skills** through hands-on monitoring, detection, investigation, and documentation.

Instead of learning cybersecurity only through theory, I am using this lab to practice the complete security-monitoring lifecycle:

```text
Collect
  ↓
Detect
  ↓
Triage
  ↓
Investigate
  ↓
Correlate
  ↓
Assess
  ↓
Document
  ↓
Improve Detection
```

This project will continue to evolve as I build additional detections and investigation scenarios.

---

# 👨‍💻 Author

**Okechukwu Goodluck Chinemerem**

**Cybersecurity Student | Aspiring SOC Analyst | Blue Team Enthusiast**

This project represents my ongoing development of practical cybersecurity skills through hands-on security monitoring, investigation, detection engineering, and continuous learning.
