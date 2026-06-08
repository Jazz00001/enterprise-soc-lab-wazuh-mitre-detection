<div align="center">

<!-- Animated Header Banner -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1a1b27,100:00d4ff&height=200&section=header&text=Enterprise%20SOC%20Lab&fontSize=48&fontColor=00d4ff&fontAlignY=38&desc=Wazuh%20SIEM%2FXDR%20%E2%80%A2%20MITRE%20ATT%26CK%20%E2%80%A2%20Threat%20Detection&descAlignY=60&descSize=16&descColor=a0aec0&animation=fadeIn" width="100%"/>

<!-- Status Badges -->
<p>
  <img src="https://img.shields.io/badge/Status-Active-00d4ff?style=for-the-badge&logo=statuspage&logoColor=white"/>
  <img src="https://img.shields.io/badge/Wazuh-4.7.5-005571?style=for-the-badge&logo=elastic&logoColor=white"/>
  <img src="https://img.shields.io/badge/MITRE%20ATT%26CK-Mapped-e63946?style=for-the-badge&logo=target&logoColor=white"/>
  <img src="https://img.shields.io/badge/Detections-6%20Scenarios-2d9a27?style=for-the-badge&logo=shield&logoColor=white"/>
</p>

<p>
  <img src="https://img.shields.io/badge/Platform-VirtualBox-183A61?style=for-the-badge&logo=virtualbox&logoColor=white"/>
  <img src="https://img.shields.io/badge/Windows%2010-Sysmon-0078d4?style=for-the-badge&logo=windows&logoColor=white"/>
  <img src="https://img.shields.io/badge/Ubuntu-22.04.5-E95420?style=for-the-badge&logo=ubuntu&logoColor=white"/>
  <img src="https://img.shields.io/badge/Reports-6%20IRs%20%2B%201%20Full%20Triage-9b5de5?style=for-the-badge&logo=read-the-docs&logoColor=white"/>
</p>

<!-- Typing animation -->
<a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=18&duration=3000&pause=800&color=00D4FF&center=true&vCenter=true&multiline=false&width=700&lines=Simulating+Real-World+Attacks+%E2%86%92+Detecting+%E2%86%92+Investigating;SOC+Operations%3A+Triage+%7C+MITRE+Mapping+%7C+Incident+Reports;Built+for+Junior+SOC+Analyst+Portfolio+%F0%9F%9B%A1%EF%B8%8F" alt="Typing SVG" /></a>

</div>

---

## 📋 Table of Contents

<div align="center">

| Section | Description |
|:-------:|:-----------|
| [🧭 Overview](#-overview) | Project summary and goals |
| [🏗️ Architecture](#%EF%B8%8F-lab-architecture) | Network layout and components |
| [⚙️ Setup Guide](#%EF%B8%8F-how-to-reproduce-this-lab) | Full reproduction steps |
| [⚔️ Attack Simulations](#%EF%B8%8F-attack-simulations) | All 6 simulated attack scenarios |
| [🎯 MITRE Detections](#-detections--mitre-attck-mapping) | Detection table with ATT&CK mapping |
| [📄 Incident Reports](#-incident-reports) | Formal IR documentation |
| [📊 Screenshots](#-screenshots) | Dashboard and alert screenshots |
| [🧠 Skills & Lessons](#-key-skills-demonstrated) | SOC skills demonstrated |
| [🚀 Future Roadmap](#-future-improvements) | Planned improvements |

</div>

---

## 🧭 Overview

> **A fully functional mini enterprise Security Operations Centre (SOC) lab**, built from scratch using open-source tools. This project mirrors the real-world daily workflow of a **Junior SOC Analyst** — from agent deployment and attack simulation, through alert triage, MITRE ATT&CK mapping, and formal incident report writing.

<table>
<tr>
<td width="50%">

### 🎯 What This Lab Does
- ✅ Collects security logs from **Windows & Linux** endpoints
- ✅ Detects **6 real attack techniques** in near real-time
- ✅ Maps every detection to the **MITRE ATT&CK framework**
- ✅ Monitors file changes via **File Integrity Monitoring (FIM)**
- ✅ Scans for known **CVE vulnerabilities**
- ✅ Produces **formal Incident Response reports**

</td>
<td width="50%">

### 🛠️ Core Stack

| Component | Tool |
|-----------|------|
| **SIEM / XDR** | Wazuh 4.7.5 |
| **Process Visibility** | Sysmon (Sysinternals) |
| **Endpoints** | Windows 10, Ubuntu 22.04.5 |
| **Virtualisation** | VirtualBox 7.x |
| **Framework** | MITRE ATT&CK |

</td>
</tr>
</table>

---

## 🏗️ Lab Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                  HOST-ONLY NETWORK  192.168.56.0/24             │
│                                                                  │
│  ┌───────────────────┐        ┌──────────────────────────────┐  │
│  │   WAZUH SERVER    │◄──────►│      WINDOWS 10 ENDPOINT     │  │
│  │   192.168.56.102  │  Agent │       192.168.56.101          │  │
│  │                   │        │    + Sysmon (process logs)    │  │
│  │  • Manager        │        └──────────────────────────────┘  │
│  │  • Dashboard      │                                          │
│  │  • Indexer        │        ┌──────────────────────────────┐  │
│  │  • Alerting       │◄──────►│     UBUNTU 22.04 ENDPOINT    │  │
│  │  • FIM/Syscheck   │  Agent │       192.168.56.103          │  │
│  │  • Vuln Detector  │        │    + auth.log + FIM active    │  │
│  └───────────────────┘        └──────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

| Component | Tool / OS | Role | IP Address |
|-----------|-----------|------|------------|
| 🖥️ **SIEM/XDR** | Wazuh 4.7.5 | Manager · Dashboard · Indexer · Alerting · FIM | `192.168.56.102` |
| 💻 **Endpoint 1** | Windows 10 + Sysmon | Windows event logs · Process monitoring · PowerShell detection | `192.168.56.101` |
| 🐧 **Endpoint 2** | Ubuntu 22.04.5 | Linux auth logs · SSH monitoring · Sudo monitoring · FIM | `192.168.56.103` |
| ☁️ **Virtualisation** | VirtualBox 7.x | Host-only isolated lab network | `192.168.56.0/24` |

> 📸 *See [Screenshots](#-screenshots) section for live dashboard and alert images.*

---

## ⚙️ How to Reproduce This Lab

<details>
<summary><b>📋 Prerequisites</b></summary>
<br>

| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| **RAM** | 8 GB | 16 GB |
| **Disk** | 80 GB free | 120 GB free |
| **Software** | VirtualBox 7.x | VirtualBox 7.x |
| **OS** | Any host OS | Windows / Linux |

</details>

---

### Step 1 — Deploy Wazuh Server (SIEM)

```bash
# 1. Create Ubuntu 22.04 VM: 4GB RAM | 2 vCPU | 50GB disk | Host-Only adapter

# 2. Run the Wazuh all-in-one installer
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a

# 3. Access the dashboard
# URL:  https://192.168.56.102
# User: admin
# Pass: (shown at end of install output — save it!)
```

> 💡 **Tip:** The installer deploys the Wazuh Manager, Dashboard, and Indexer in a single step. Installation takes ~10 minutes.

---

### Step 2 — Deploy Windows 10 Agent + Sysmon

```powershell
# VM Spec: 2GB RAM | Host-Only adapter | Static IP: 192.168.56.101

# Install Wazuh agent:
# Dashboard → Agents → Deploy new agent → Windows → download & run MSI
# Set manager IP: 192.168.56.102 during install

# Install Sysmon for deep process visibility:
sysmon64.exe -accepteula -i sysmonconfig.xml

# Verify agent is running:
Get-Service WazuhSvc
```

> 💡 **Tip:** Use the [SwiftOnSecurity Sysmon config](https://github.com/SwiftOnSecurity/sysmon-config) for production-grade process monitoring rules.

---

### Step 3 — Deploy Ubuntu 22.04 Linux Agent

```bash
# VM Spec: 1GB RAM | Host-Only adapter | Static IP: 192.168.56.103

# Download and install the Wazuh agent
curl -sO https://packages.wazuh.com/4.7/wazuh-agent-install.sh
sudo WAZUH_MANAGER='192.168.56.102' bash wazuh-agent-install.sh

# Enable and start the agent
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

# Verify agent status
sudo systemctl status wazuh-agent
```

> ✅ After completing all 3 steps, both agents should appear as **Active** in the Wazuh Dashboard under **Agents**.

---

## ⚔️ Attack Simulations

All 6 attack scenarios were manually simulated to generate real alerts in the Wazuh dashboard.

| # | Attack / Detection | Platform | Tactic | Status |
|:-:|-------------------|:--------:|--------|:------:|
| 1 | 🔑 Brute force failed logins | Windows | Credential Access | ✅ Completed |
| 2 | 💻 Suspicious PowerShell execution | Windows | Execution / Defense Evasion | ✅ Completed |
| 3 | 👤 New local user creation | Windows | Persistence | ✅ Completed |
| 4 | 🔐 SSH brute force | Linux | Credential Access | ✅ Completed |
| 5 | 📝 File Integrity — `/etc/hosts` modified | Linux | Impact | ✅ Completed |
| 6 | 🔓 Privilege escalation via sudo | Linux | Privilege Escalation | ✅ Completed |

---

## 🎯 Detections & MITRE ATT&CK Mapping

<div align="center">

| Detection | Log Source | MITRE ID | Technique | Tactic | Severity |
|-----------|-----------|:--------:|-----------|--------|:--------:|
| Windows failed logins | Windows Security Log | [T1110.001](https://attack.mitre.org/techniques/T1110/001/) | Brute Force: Password Guessing | Credential Access | 🔴 High |
| Suspicious PowerShell | Sysmon / WinEvent | [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | Command & Scripting: PowerShell | Execution / Defense Evasion | 🔴 High |
| New local user created | Windows Security Log | [T1136.001](https://attack.mitre.org/techniques/T1136/001/) | Create Account: Local Account | Persistence | 🟡 Medium |
| SSH brute force | `/var/log/auth.log` | [T1110.001](https://attack.mitre.org/techniques/T1110/001/) | Brute Force: Password Guessing | Credential Access | 🔴 High |
| `/etc/hosts` modified | Wazuh FIM / Syscheck | [T1565.001](https://attack.mitre.org/techniques/T1565/001/) | Stored Data Manipulation | Impact | 🟡 Medium |
| Sudo privilege escalation | `/var/log/auth.log` | [T1548.003](https://attack.mitre.org/techniques/T1548/003/) | Sudo and Sudo Caching | Privilege Escalation | 🔴 High |
| Vulnerability detection | Wazuh Vuln Detector | CVE Exposure | CVE / Vulnerability Management | Risk Management | 🔴 High |

</div>

---

## 📄 Incident Reports

Each detection produced a formal, structured Incident Response document — mirroring real SOC analyst deliverables.

<div align="center">

| Report | Title | Severity |
|:------:|-------|:--------:|
| [IR-001](./Incident-Reports/IR-001-Windows-Brute-Force.pdf) | Windows Brute Force Failed Logins | 🔴 High |
| [IR-002](./Incident-Reports/IR-002-PowerShell-Execution.pdf) | Suspicious PowerShell Execution | 🔴 High |
| [IR-003](./Incident-Reports/IR-003-New-Local-User.pdf) | New Local User Creation — Windows | 🟡 Medium |
| [IR-004](./Incident-Reports/IR-004-SSH-Brute-Force.pdf) | Linux SSH Brute Force | 🔴 High |
| [IR-005](./Incident-Reports/IR-005-FIM-Hosts-Modified.pdf) | File Integrity Monitoring — Hosts File Modified | 🟡 Medium |
| [IR-006](./Incident-Reports/IR-006-Sudo-Escalation.pdf) | Linux Sudo Privilege Escalation | 🔴 High |
| [📋 Full Triage](./Full-SOC-Triage-Report.pdf) | **Complete SOC Triage Report** | All |

</div>

> Each report follows the standard IR structure: **Summary → Timeline → Evidence → Impact Analysis → Containment → Recommendations.**

---

## 🔧 Detection Rules

This lab relies on **Wazuh built-in rules** for all detections, with custom rule examples provided in the [`Rules/`](./Rules/) directory.

<details>
<summary><b>📜 View Active Built-in Rule IDs</b></summary>

<br>

| Rule ID | Description | Platform |
|:-------:|-------------|:--------:|
| `92057` | PowerShell encoded command detected | 🪟 Windows |
| `92027` | PowerShell process spawned a PowerShell child instance | 🪟 Windows |
| `5710` | SSH login attempt using non-existent user | 🐧 Linux |
| `2502` | User failed password authentication (multiple times) | 🐧 Linux |
| `5402` | Successful `sudo` escalation to ROOT | 🐧 Linux |
| `5404` | Three consecutive failed `sudo` attempts | 🐧 Linux |
| `550` | FIM: Integrity checksum changed on monitored file | 🐧 Linux / 🪟 Windows |

</details>

<details>
<summary><b>📝 Custom Rule Example (XML)</b></summary>

```xml
<!-- Custom rule: Detect new local user creation via net user command -->
<group name="custom_windows,">
  <rule id="100001" level="10">
    <if_sid>4720</if_sid>
    <description>Custom: New local Windows account created</description>
    <mitre>
      <id>T1136.001</id>
    </mitre>
  </rule>
</group>
```

> See [`Rules/custom_rules.xml`](./Rules/custom_rules.xml) for the full custom ruleset.

</details>

---

## 📊 Screenshots

<details>
<summary><b>🖥️ View All Dashboard & Alert Screenshots</b></summary>

<br>

**Wazuh Main Dashboard**
![Wazuh Dashboard](./screenshots/wazuh-dashboard.png)

**Both Agents Active**
![Agents Connected](./screenshots/agents-connected.png)

**Windows Brute Force Alert**
![Brute Force Alert](./screenshots/windows-brute-force.png)

**Suspicious PowerShell Execution**
![PowerShell Alert](./screenshots/powershell-alert.png)

**New Local User Creation**
![New User Alert](./screenshots/new-user-alert.png)

**Linux SSH Brute Force**
![SSH Brute Force](./screenshots/linux-ssh-brute-force.png)

**File Integrity Monitoring Alert**
![FIM Alert](./screenshots/fim-alert.png)

**Linux Sudo Privilege Escalation**
![Sudo Escalation](./screenshots/sudo-privilege-escalation.png)

**MITRE ATT&CK Dashboard**
![MITRE Dashboard](./screenshots/mitre-dashboard.png)

**Vulnerability Detection**
![Vulnerability Scan](./screenshots/vulnerability-detection.png)

</details>

---

## 🧠 Key Skills Demonstrated

<div align="center">

```
╔═══════════════════════════════════════════════════════════════════╗
║              SOC ANALYST SKILL MATRIX COVERED IN THIS LAB        ║
╠══════════════════════════╦════════════════════════════════════════╣
║  SIEM Deployment         ║  Wazuh all-in-one install + config    ║
║  Agent Management        ║  Windows + Linux agent deployment      ║
║  Log Collection          ║  Multi-endpoint telemetry ingestion    ║
║  Sysmon Tuning           ║  Process creation + PS detection       ║
║  Alert Triage            ║  Severity assessment + investigation   ║
║  MITRE ATT&CK Mapping    ║  Tactic/Technique identification       ║
║  File Integrity Mon.     ║  FIM / Syscheck configuration          ║
║  Vulnerability Mgmt      ║  CVE scanning and exposure reporting   ║
║  Incident Reporting      ║  Formal IR doc creation (6 reports)   ║
║  Full Triage Report      ║  End-to-end SOC triage documentation  ║
╚══════════════════════════╩════════════════════════════════════════╝
```

</div>

---

## 📚 Lessons Learned

- 🔍 **SIEM fundamentals** — how a SIEM aggregates logs from multiple endpoints and transforms raw events into actionable security alerts
- 🪟 **Windows visibility** — how Sysmon dramatically improves process creation and PowerShell activity visibility beyond default Windows logs
- 🐧 **Linux monitoring** — how `/var/log/auth.log` exposes SSH brute-force patterns and sudo escalation behaviour in detail
- 🎯 **MITRE ATT&CK** — how to use the framework to categorise attacker behaviour by Tactic, Technique, and Sub-technique
- 📝 **Documentation matters** — a SOC analyst's value is not just in detecting threats, but in clearly communicating *what happened*, *why it matters*, and *how to respond*

---

## 🚀 Future Improvements

| Priority | Improvement | Benefit |
|:--------:|-------------|---------|
| 🔴 High | Add a dedicated **Kali Linux attacker VM** | Realistic offensive simulation |
| 🔴 High | Implement **Wazuh Active Response** | Auto-block brute-force source IPs |
| 🟡 Medium | Build and test **custom Wazuh rule IDs** | Tailored detection logic |
| 🟡 Medium | Add **auditd** on the Ubuntu endpoint | Deeper Linux syscall visibility |
| 🟢 Low | Configure **Slack / email alerting** | Real-time high-severity notifications |
| 🟢 Low | Export **raw JSON alert evidence** | Forensic-grade artefact preservation |

### 🗺️ Planned Future Architecture

```
┌──────────────────────────────────────────────────────────────────────┐
│                  FUTURE LAB  192.168.56.0/24                        │
│                                                                      │
│  ┌────────────┐   ┌────────────┐   ┌────────────┐   ┌────────────┐ │
│  │  WAZUH     │   │ WINDOWS 10 │   │ UBUNTU 22  │   │   KALI     │ │
│  │  SERVER    │◄─►│ + Sysmon   │   │ + auditd   │◄──│  ATTACKER  │ │
│  │  .102      │◄─►│   .101     │   │   .103     │   │   .104     │ │
│  └────────────┘   └────────────┘   └────────────┘   └────────────┘ │
│        │                                                             │
│        ▼  Active Response                                            │
│  [ Auto-block IPs ] [ Slack Alerts ] [ JSON Evidence Export ]       │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 💼 Resume Bullet

> *"Built a mini enterprise SOC lab using Wazuh SIEM/XDR with Windows Sysmon and Ubuntu Linux endpoints. Configured multi-endpoint log collection, simulated 6 real-world attack scenarios, mapped all detections to the MITRE ATT&CK framework, enabled File Integrity Monitoring and CVE vulnerability detection, and produced 6 formal Incident Response reports plus a full SOC triage document."*

---

<div align="center">

<!-- Footer wave -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:00d4ff,100:0d1117&height=120&section=footer" width="100%"/>

<p>
  <img src="https://img.shields.io/badge/Built%20with-Wazuh%20SIEM-005571?style=flat-square&logo=elastic"/>
  <img src="https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-e63946?style=flat-square"/>
  <img src="https://img.shields.io/badge/Lab%20Type-SOC%20%2F%20Blue%20Team-2d9a27?style=flat-square"/>
  <img src="https://img.shields.io/badge/Level-Junior%20SOC%20Analyst-9b5de5?style=flat-square"/>
</p>

<sub>⭐ If this project helped you, consider giving it a star!</sub>

</div>
