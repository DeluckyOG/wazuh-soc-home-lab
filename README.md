# wazuh-soc-home-lab
Wazuh SOC home lab for Windows &amp; Linux security monitoring, alert investigation, and threat detection.

# Wazuh SOC Home Lab

A home lab where I deployed **Wazuh** (open-source SIEM/XDR) to collect and analyze security events from a Windows and a Linux endpoint, and to practice SOC analyst workflows such as log review, alert triage, and threat hunting.

## Objectives

- Deploy a working all-in-one Wazuh server (manager, indexer, dashboard)
- Enroll Windows and Linux endpoints as Wazuh agents
- Collect and review endpoint telemetry and security alerts
- Practice investigating events like a SOC analyst

## Lab Architecture

All machines run as virtual machines in **VMware Workstation** on the same virtual network (`192.168.89.0/24`).

| Machine | OS | IP Address | Role |
|---------|----|-----------|------|
| Wazuh-Server | Ubuntu Server | _(add IP)_ | Wazuh manager, indexer, dashboard |
| delucky-windows (Agent 001) | Windows 10 Pro (10.0.19045) | 192.168.89.131 | Monitored endpoint |
| Delucky-Linux (Agent 002) | Ubuntu 24.04.5 LTS | 192.168.89.130 | Monitored endpoint |

**Wazuh version:** 4.14.7

```
 [ Windows 10 Agent ]      [ Ubuntu 24.04 Agent ]
          \                        /
           \                      /
            -->  [ Wazuh Server ] <--
                 manager + indexer
                    + dashboard
                         |
                  Analyst (browser)
```

## Tools Used

- Wazuh 4.14.7 (SIEM/XDR)
- VMware Workstation
- Ubuntu Server (Wazuh server) and Ubuntu 24.04 (endpoint)
- Windows 10 Pro (endpoint)

## Setup Walkthrough

### 1. Wazuh server installation

I created an Ubuntu VM and installed Wazuh using the official `wazuh-install.sh` installation assistant, which deploys the manager, indexer, and dashboard on a single node.
![image alt](https://github.com/DeluckyOG/wazuh-soc-home-lab/blob/b235cd4bc88d8852f9ad1b3689329ed86e9ae6c0/my%20virtual%20machine.png)

### 2. Agent deployment

I enrolled two endpoints using the dashboard's **Deploy new agent** workflow: a Windows 10 machine and an Ubuntu 24.04 machine. Both agents report as **Active** on node `node01`, in the `default` group.

![image alt](https://github.com/DeluckyOG/wazuh-soc-home-lab/blob/9cb6051f63636af18b46411941d35a2d113af417/my%20wazuh%20agent%20dashboard.png)
### 3. Enabling full log archiving

To see all raw events (not only those that trigger alerts), I used the `wazuh-archives*` index in the dashboard's Discover view. This let me inspect the full event stream from each endpoint.

_(Add the setting you changed to enable archiving, e.g. `logall` / `logall_json` in `ossec.conf`, and the config snippet in `configs/`.)_

### 4. Reviewing endpoint data

- **Linux agent:** about 2,900 events in 24 hours, including Security Configuration Assessment (SCA) checks.
- **Windows agent:** about 2,300 events in 24 hours, including Windows event log data such as process activity (image path, process ID, user, GUIDs).

![image alt](https://github.com/DeluckyOG/wazuh-soc-home-lab/blob/7ad64b94a4b0bd0f7775c4cdcb27537a343f469b/my%20wazuh%20linux%20aleart%20dashboad.png)

![image alt](https://github.com/DeluckyOG/wazuh-soc-home-lab/blob/73ad2bc40a76ca0c284318dc8e1d4a5179d21da2/my%20wazuh%20windows%20alert%20dashboard.png)

### 5. Dashboard overview

The Wazuh overview page summarizes agent health and alert severity, with modules for Configuration Assessment, Malware Detection, File Integrity Monitoring, Threat Hunting, Vulnerability Detection, and MITRE ATT&CK.

In the last 24 hours the lab generated **0 critical, 0 high, 1 medium, and 31 low** severity alerts.

![Dashboard overview](screenshots/02-dashboard-overview.png)

## Detection Tests

_(This section is where the project becomes impressive. Add 2 or 3 tests, each with what you did, the alert Wazuh raised, and your analysis.)_

| Test | What I did | Wazuh result | Rule ID / Level | MITRE ATT&CK |
|------|-----------|--------------|-----------------|--------------|
| Failed SSH logins | _(describe)_ | _(alert seen)_ | _(rule)_ | _(technique)_ |
| File integrity change | _(describe)_ | _(alert seen)_ | _(rule)_ | _(technique)_ |
| _(your own test)_ | | | | |

## Key Findings

- _(What the alerts showed and what they mean)_
- _(Anything that surprised you)_

## Challenges and Lessons Learned

- _(Problems you hit, like agent connection, resource limits, or network setup, and how you fixed them)_
- _(What you learned about SIEM operation, log volume, and alert tuning)_

## Next Steps

- Add custom detection rules and decoders
- Enable active response
- Integrate threat intelligence
- Simulate more attack techniques and map them to MITRE ATT&CK

## Repository Structure

```
wazuh-soc-home-lab/
├── README.md
├── configs/        # sanitized config files (no passwords or keys)
└── screenshots/    # lab evidence
```

> **Note:** All credentials, agent keys, and tokens have been removed from this repository.
