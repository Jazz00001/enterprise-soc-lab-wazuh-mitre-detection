<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:060D14,30:0A1628,60:0D2137,100:00B4D8&height=220&section=header&text=Enterprise%20SOC%20Lab&fontSize=52&fontColor=ffffff&fontAlignY=40&desc=Wazuh%20SIEM%2FXDR%20%E2%80%A2%20MITRE%20ATT%26CK%20%E2%80%A2%20Threat%20Detection%20%E2%80%A2%20Incident%20Response&descAlignY=62&descSize=15&descColor=90CAF9&animation=fadeIn" width="100%"/>

<br/>

<!-- Live status dot + title line -->
<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=15&duration=2800&pause=1000&color=00B4D8&center=true&vCenter=true&width=750&lines=%E2%97%8F+ACTIVE+LAB+%E2%80%94+Wazuh+4.7.5+%7C+2+Agents+Online+%7C+6+Detections+Live;Simulating+Real-World+Attacks+%E2%86%92+Detecting+%E2%86%92+Triaging+%E2%86%92+Reporting;SOC+Analyst+Workflow%3A+Log+Collection+%7C+Alert+Triage+%7C+MITRE+Mapping;Built+end-to-end+from+scratch+%E2%80%94+deployment+to+incident+reports" alt="Typing SVG"/>

<br/><br/>

<!-- Primary badges -->
[![Wazuh](https://img.shields.io/badge/Wazuh-4.7.5-005571?style=for-the-badge&logo=elastic&logoColor=white)](https://wazuh.com)
[![MITRE ATT&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-Covered-CC2200?style=for-the-badge&logo=target&logoColor=white)](https://attack.mitre.org)
[![Detections](https://img.shields.io/badge/Detections-6%20Scenarios-1a7a4a?style=for-the-badge&logo=checkmarx&logoColor=white)](./Incident-Reports/)
[![Reports](https://img.shields.io/badge/IR%20Reports-6%20%2B%201%20Full%20Triage-6A0DAD?style=for-the-badge&logo=googledocs&logoColor=white)](./Incident-Reports/)

<!-- Secondary badges -->
[![Platform](https://img.shields.io/badge/VirtualBox-7.x-183A61?style=for-the-badge&logo=virtualbox&logoColor=white)](https://www.virtualbox.org)
[![Windows](https://img.shields.io/badge/Windows%2010-Sysmon-0078D4?style=for-the-badge&logo=windows&logoColor=white)](#)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04.5%20LTS-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](#)
[![Status](https://img.shields.io/badge/Status-Active-00B4D8?style=for-the-badge&logo=statuspage&logoColor=white)](#)

<br/>

> **A complete, end-to-end mini enterprise Security Operations Centre — built from scratch using 100% open-source tools.**
> Mirrors the real daily workflow of a Junior SOC Analyst: agent deployment, attack simulation, alert triage, MITRE ATT&CK mapping, and formal incident documentation.

</div>

---

## 🗂 Table of Contents

<details open>
<summary><b>Click to expand / collapse</b></summary>

<br/>

```
📌 Overview ·········· What this lab does and why
🏗 Architecture ······ Network layout, components, IPs
⚙️  Setup Guide ······ Step-by-step reproduction guide
⚔️  Simulations ······ 6 attack scenarios executed
🎯 Detections ········ MITRE ATT&CK full mapping table
📄 Incident Reports ·· 6 IRs + 1 full SOC triage report
🔧 Detection Rules ··· Built-in + custom Wazuh rules
📊 Screenshots ······· Dashboard, alerts, and FIM visuals
🧠 Skills ············ Analyst capabilities demonstrated
📚 Lessons Learned ··· Key takeaways from building this lab
🚀 Roadmap ·········· Future improvements and architecture
💼 Resume Bullet ····· Copy-paste ready bullet point
```

</details>

---

## 📌 Overview

<table>
<tr>
<td width="55%" valign="top">

### What this lab does

This project is a **fully operational mini enterprise SOC lab** using Wazuh SIEM/XDR as its detection engine.

The lab **simulates, detects, investigates, and documents** 6 real-world attack techniques across Windows and Linux endpoints — mapping every detection to the [MITRE ATT&CK framework](https://attack.mitre.org) and writing formal Incident Response reports for each one.

**Every component was built from scratch:**
- Deployed Wazuh all-in-one on a dedicated Ubuntu server VM
- Configured Sysmon on a Windows 10 endpoint for deep process visibility
- Enrolled an Ubuntu 22.04 endpoint for Linux log monitoring and FIM
- Manually simulated each attack, triaged the resulting alerts, and wrote structured incident reports

</td>
<td width="45%" valign="top">

### Core stack

| Layer | Component |
|-------|-----------|
| **SIEM / XDR** | Wazuh 4.7.5 |
| **Dashboard** | Wazuh / OpenSearch |
| **Process Telemetry** | Sysmon (Sysinternals) |
| **Windows Endpoint** | Windows 10 Pro |
| **Linux Endpoint** | Ubuntu 22.04.5 LTS |
| **Virtualisation** | VirtualBox 7.x |
| **Detection Framework** | MITRE ATT&CK |
| **FIM** | Wazuh Syscheck |
| **Vuln Scanning** | Wazuh Vuln Detector |

</td>
</tr>
</table>

---

## 🏗 Lab Architecture

```
╔══════════════════════════════════════════════════════════════════════╗
║               HOST-ONLY NETWORK  —  192.168.56.0/24                 ║
║                                                                      ║
║  ┌──────────────────────┐     ┌────────────────────────────────────┐ ║
║  │    WAZUH SERVER       │◄───►│         WINDOWS 10 ENDPOINT        │ ║
║  │    192.168.56.102     │     │          192.168.56.101            │ ║
║  │                       │     │   Sysmon · PowerShell logs         │ ║
║  │  ● Manager            │     │   Windows Security Events          │ ║
║  │  ● Dashboard          │     └────────────────────────────────────┘ ║
║  │  ● Indexer            │                                            ║
║  │  ● Alerting           │     ┌────────────────────────────────────┐ ║
║  │  ● FIM / Syscheck     │◄───►│         UBUNTU 22.04 ENDPOINT      │ ║
║  │  ● Vuln Detector      │     │          192.168.56.103            │ ║
║  └──────────────────────┘     │   auth.log · FIM · sudo logs       │ ║
║                                └────────────────────────────────────┘ ║
╚══════════════════════════════════════════════════════════════════════╝
```

<div align="center">

| Component | Tool / OS | Role | IP |
|:---------:|-----------|------|----|
| 🖥 **SIEM / XDR** | Wazuh 4.7.5 | Manager · Dashboard · Indexer · Alerting · FIM | `192.168.56.102` |
| 💻 **Endpoint 1** | Windows 10 + Sysmon | Event logs · Process telemetry · PowerShell detection | `192.168.56.101` |
| 🐧 **Endpoint 2** | Ubuntu 22.04.5 | Auth logs · SSH monitoring · Sudo monitoring · FIM | `192.168.56.103` |
| 📦 **Hypervisor** | VirtualBox 7.x | Host-only isolated lab network | `192.168.56.0/24` |

</div>

---

## ⚙️ How to Reproduce This Lab

<details>
<summary><b>📋 System requirements before you start</b></summary>

<br/>

| Resource | Minimum | Recommended |
|----------|:-------:|:-----------:|
| RAM | 8 GB | 16 GB |
| Free disk | 80 GB | 120 GB |
| CPU cores | 4 | 6+ |
| Hypervisor | VirtualBox 7.x | VirtualBox 7.x |
| Host OS | Windows / Linux / macOS | Any |

</details>

---

### 🔷 Step 1 — Deploy Wazuh Server

```
VM spec: Ubuntu 22.04 · 4 GB RAM · 2 vCPU · 50 GB disk · Host-Only adapter
Static IP: 192.168.56.102
```

```bash
# Download and run the Wazuh all-in-one installer
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a

# Installer deploys: Manager + Dashboard + Indexer in one pass (~10 min)
# Save the admin password printed at the end of installation

# Access dashboard
# URL  → https://192.168.56.102
# User → admin
# Pass → (from install output)
```

> **Tip:** The `-a` flag deploys all components automatically. Make a snapshot of your VM immediately after installation succeeds — it saves a lot of time if you need to reset.

---

### 🔷 Step 2 — Deploy Windows 10 Agent + Sysmon

```
VM spec: Windows 10 · 2 GB RAM · Host-Only adapter
Static IP: 192.168.56.101
```

```powershell
# 1. In Wazuh Dashboard → Agents → Deploy new agent → Windows
#    Set manager IP: 192.168.56.102
#    Download the generated MSI and run it as Administrator

# 2. Install Sysmon for deep process and PowerShell visibility
#    Download: https://docs.microsoft.com/sysinternals/downloads/sysmon
sysmon64.exe -accepteula -i sysmonconfig.xml

# 3. Verify the Wazuh agent service is running
Get-Service WazuhSvc

# Expected output:
# Status   Name      DisplayName
# -------  ----      -----------
# Running  WazuhSvc  Wazuh
```

> **Tip:** Use the [SwiftOnSecurity sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config) for a production-quality Sysmon ruleset that detects most ATT&CK techniques out of the box.

---

### 🔷 Step 3 — Deploy Ubuntu 22.04 Linux Agent

```
VM spec: Ubuntu 22.04 · 1 GB RAM · Host-Only adapter
Static IP: 192.168.56.103
```

```bash
# Download and install the Wazuh agent (manager IP injected at install time)
curl -sO https://packages.wazuh.com/4.7/wazuh-agent-install.sh
sudo WAZUH_MANAGER='192.168.56.102' bash wazuh-agent-install.sh

# Enable and start the agent
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

# Verify the agent is running and connected
sudo systemctl status wazuh-agent
```

> ✅ Once all three steps are complete, both agents will appear as **Active** in the Wazuh Dashboard under **Agents → Overview**. You are ready to begin attack simulations.

---

## ⚔️ Attack Simulations

All 6 attack scenarios were **manually executed** against the lab endpoints to generate authentic, real alerts in the Wazuh dashboard. No synthetic log injection was used.

<div align="center">

| # | Scenario | Platform | Tactic | Severity | Status |
|:-:|---------|:--------:|--------|:--------:|:------:|
| 01 | 🔑 Brute force failed logins | Windows | Credential Access | 🔴 High | ✅ Done |
| 02 | 💻 Suspicious PowerShell execution | Windows | Execution · Defense Evasion | 🔴 High | ✅ Done |
| 03 | 👤 New local user creation | Windows | Persistence | 🟡 Medium | ✅ Done |
| 04 | 🔐 SSH brute force | Linux | Credential Access | 🔴 High | ✅ Done |
| 05 | 📝 FIM — `/etc/hosts` modified | Linux | Impact | 🟡 Medium | ✅ Done |
| 06 | 🔓 Privilege escalation via `sudo` | Linux | Privilege Escalation | 🔴 High | ✅ Done |

</div>

---

## 🎯 Detections & MITRE ATT&CK Mapping

<div align="center">

| Detection | Log Source | MITRE ID | Technique | Tactic | Severity |
|-----------|:----------:|:--------:|-----------|:------:|:--------:|
| Windows failed logins | Windows Security Log | [T1110.001](https://attack.mitre.org/techniques/T1110/001/) | Brute Force: Password Guessing | Credential Access | 🔴 High |
| Suspicious PowerShell | Sysmon · WinEvent | [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | Command & Scripting: PowerShell | Execution / Defense Evasion | 🔴 High |
| New local user | Windows Security Log | [T1136.001](https://attack.mitre.org/techniques/T1136/001/) | Create Account: Local Account | Persistence | 🟡 Medium |
| SSH brute force | `/var/log/auth.log` | [T1110.001](https://attack.mitre.org/techniques/T1110/001/) | Brute Force: Password Guessing | Credential Access | 🔴 High |
| `/etc/hosts` modified | Wazuh FIM / Syscheck | [T1565.001](https://attack.mitre.org/techniques/T1565/001/) | Stored Data Manipulation | Impact | 🟡 Medium |
| Sudo privilege escalation | `/var/log/auth.log` | [T1548.003](https://attack.mitre.org/techniques/T1548/003/) | Abuse Elevation: Sudo Caching | Privilege Escalation | 🔴 High |
| CVE exposure | Wazuh Vuln Detector | CVE Scan | Vulnerability Management | Risk Management | 🔴 High |

</div>

---

## 📄 Incident Reports

Every detection was documented as a **formal Incident Response report** — the same deliverable expected from a junior analyst in a real SOC environment.

<div align="center">

| ID | Title | Severity | Link |
|:--:|-------|:--------:|:----:|
| IR-001 | Windows Brute Force Failed Logins | 🔴 High | [View →](./Incident-Reports/IR-001-Windows-Brute-Force.pdf) |
| IR-002 | Suspicious PowerShell Execution | 🔴 High | [View →](./Incident-Reports/IR-002-PowerShell-Execution.pdf) |
| IR-003 | New Local User Creation — Windows | 🟡 Medium | [View →](./Incident-Reports/IR-003-New-Local-User.pdf) |
| IR-004 | Linux SSH Brute Force | 🔴 High | [View →](./Incident-Reports/IR-004-SSH-Brute-Force.pdf) |
| IR-005 | File Integrity — `/etc/hosts` Modified | 🟡 Medium | [View →](./Incident-Reports/IR-005-FIM-Hosts-Modified.pdf) |
| IR-006 | Linux Sudo Privilege Escalation | 🔴 High | [View →](./Incident-Reports/IR-006-Sudo-Escalation.pdf) |
| **Triage** | **Full SOC Triage Report — All Incidents** | All | [**View →**](./Full-SOC-Triage-Report.pdf) |

</div>

> Each report follows the standard IR structure: **Executive Summary → Detection Timeline → Evidence → Impact Assessment → Containment Steps → Recommendations**

---

## 🔧 Detection Rules

The lab uses **Wazuh built-in rules** for all production detections, with additional custom rule examples in [`Rules/`](./Rules/).

<details>
<summary><b>📋 Active built-in rule reference</b></summary>

<br/>

| Rule ID | Description | Platform |
|:-------:|-------------|:--------:|
| `92057` | PowerShell encoded command detected | 🪟 Windows |
| `92027` | PowerShell spawned a child PowerShell process | 🪟 Windows |
| `5710` | SSH login attempted with non-existent user | 🐧 Linux |
| `2502` | User failed password authentication (multiple) | 🐧 Linux |
| `5402` | Successful `sudo` to ROOT executed | 🐧 Linux |
| `5404` | Three consecutive failed `sudo` attempts | 🐧 Linux |
| `550` | FIM: Integrity checksum changed on monitored file | 🐧🪟 Both |

</details>

<details>
<summary><b>🛠 Custom rule example — <code>Rules/custom_rules.xml</code></b></summary>

<br/>

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!-- ============================================================
     Custom Wazuh Rules — Enterprise SOC Lab
     File: /var/ossec/etc/rules/local_rules.xml
     ============================================================ -->

<group name="custom_lab,">

  <!-- Rule 100001: New local Windows user created (event 4720) -->
  <rule id="100001" level="10">
    <if_sid>4720</if_sid>
    <description>New local Windows account created — possible persistence (T1136.001)</description>
    <mitre>
      <id>T1136.001</id>
    </mitre>
  </rule>

  <!-- Rule 100002: Multiple failed sudo attempts — possible escalation attempt -->
  <rule id="100002" level="10" frequency="3" timeframe="60">
    <if_matched_sid>5404</if_matched_sid>
    <description>Three+ failed sudo attempts in 60 seconds — possible privilege escalation (T1548.003)</description>
    <mitre>
      <id>T1548.003</id>
    </mitre>
  </rule>

  <!-- Rule 100003: PowerShell with encoded command — likely obfuscation -->
  <rule id="100003" level="12">
    <if_sid>92057</if_sid>
    <description>Encoded PowerShell command detected — possible defense evasion (T1059.001)</description>
    <mitre>
      <id>T1059.001</id>
    </mitre>
  </rule>

</group>
```

</details>

---

## 📊 Screenshots

<details>
<summary><b>🖼 Expand to view all dashboard and alert screenshots</b></summary>

<br/>

### Wazuh Main Dashboard
![Wazuh Dashboard](./screenshots/wazuh-dashboard.png)

---

### Both Agents Active and Connected
![Agents Connected](./screenshots/agents-connected.png)

---

### Windows Brute Force Alert — IR-001
![Brute Force Alert](./screenshots/windows-brute-force.png)

---

### Suspicious PowerShell Execution — IR-002
![PowerShell Alert](./screenshots/powershell-alert.png)

---

### New Local User Creation — IR-003
![New User Alert](./screenshots/new-user-alert.png)

---

### Linux SSH Brute Force — IR-004
![SSH Brute Force](./screenshots/linux-ssh-brute-force.png)

---

### File Integrity Monitoring Alert — IR-005
![FIM Alert](./screenshots/fim-alert.png)

---

### Linux Sudo Privilege Escalation — IR-006
![Sudo Escalation](./screenshots/sudo-privilege-escalation.png)

---

### MITRE ATT&CK Dashboard
![MITRE Dashboard](./screenshots/mitre-dashboard.png)

---

### Vulnerability Detection Scan
![Vulnerability Scan](./screenshots/vulnerability-detection.png)

</details>

---

## 🧠 Key Skills Demonstrated

<div align="center">

```
╔══════════════════════════════════════════════════════════════════════╗
║                  SOC ANALYST SKILL MATRIX — THIS LAB                ║
╠═══════════════════════════╦══════════════════════════════════════════╣
║  SIEM Deployment          ║  Wazuh all-in-one install and config    ║
║  Agent Enrollment         ║  Windows + Linux agents deployed         ║
║  Multi-source Log Ingest  ║  Unified telemetry from 2 platforms      ║
║  Sysmon Configuration     ║  Process creation + PowerShell logging  ║
║  Alert Triage             ║  Severity assessment + prioritisation    ║
║  Root Cause Analysis      ║  Tracing each alert back to its origin  ║
║  MITRE ATT&CK Mapping     ║  6 techniques across 4 tactics mapped   ║
║  File Integrity Monitor   ║  FIM + Syscheck on sensitive paths      ║
║  Vulnerability Management ║  CVE scanning and exposure reporting     ║
║  Incident Documentation   ║  6 formal IRs + full triage report      ║
║  Custom Detection Rules   ║  Wazuh XML rule authoring                ║
╚═══════════════════════════╩══════════════════════════════════════════╝
```

</div>

---

## 📚 Lessons Learned

- **SIEM log pipeline** — how a SIEM ingests raw events from multiple endpoints and enriches them into structured, actionable alerts in near real-time
- **Sysmon value** — default Windows event logs miss the detail that makes PowerShell and process-spawn attacks visible; Sysmon is non-negotiable for Windows endpoints
- **Linux auth log patterns** — `/var/log/auth.log` tells a complete story about brute-force SSH attempts and privilege escalation; learning to read it manually first made triage faster
- **MITRE ATT&CK as a language** — using Tactic → Technique → Sub-technique as a shared vocabulary makes alert communication precise and unambiguous across teams
- **Documentation is the job** — detecting an attack is only half the work; a SOC analyst must clearly communicate *what happened*, *what was affected*, *how confident they are*, and *what should happen next*
- **Snapshots save hours** — taking VirtualBox snapshots after each major configuration step prevented full rebuilds when configuration errors occurred

---

## 🚀 Future Improvements

<div align="center">

| Priority | Improvement | Expected Benefit |
|:--------:|-------------|-----------------|
| 🔴 **High** | Add dedicated **Kali Linux attacker VM** (`.104`) | Realistic offensive simulation with real tooling |
| 🔴 **High** | Enable **Wazuh Active Response** | Auto-block brute-force source IPs in real time |
| 🟡 **Medium** | Deploy **`auditd`** on the Ubuntu endpoint | Syscall-level Linux telemetry for deeper visibility |
| 🟡 **Medium** | Write and validate **full custom rule library** | Lab-specific detection logic with tuned thresholds |
| 🟢 **Low** | Configure **Slack / email alerting** pipeline | Immediate notification on high-severity events |
| 🟢 **Low** | Export **raw JSON alert artefacts** per incident | Forensic-grade evidence preservation |
| 🟢 **Low** | Add **Atomic Red Team** integration for simulation | Standardised, repeatable attack test library |

</div>

### 🗺 Planned Future Architecture

```
╔═══════════════════════════════════════════════════════════════════════╗
║                FUTURE LAB  —  192.168.56.0/24                        ║
║                                                                       ║
║  ┌─────────────┐  ┌──────────────┐  ┌──────────────┐  ┌───────────┐ ║
║  │ WAZUH 4.7.5 │  │ WINDOWS 10   │  │ UBUNTU 22.04 │  │   KALI    │ ║
║  │  .102       │◄►│  + Sysmon    │  │  + auditd    │◄─│  .104     │ ║
║  │  + Active   │◄►│  .101        │  │  .103        │  │ ATTACKER  │ ║
║  │  Response   │  └──────────────┘  └──────────────┘  └───────────┘ ║
║  └──────┬──────┘                                                      ║
║         │                                                             ║
║         ▼  Automated Response Pipeline                                ║
║  ┌──────────────────────────────────────────────────────────────┐    ║
║  │  Auto-block IPs · Slack alerts · JSON evidence export        │    ║
║  └──────────────────────────────────────────────────────────────┘    ║
╚═══════════════════════════════════════════════════════════════════════╝
```

---

## 💼 Resume Bullet

> *Built a mini enterprise SOC lab using Wazuh SIEM/XDR with Windows Sysmon and Ubuntu Linux endpoints. Deployed all infrastructure from scratch in VirtualBox, configured multi-endpoint log collection, manually simulated 6 real-world attack scenarios, mapped every detection to the MITRE ATT&CK framework (4 tactics, 6 techniques), enabled File Integrity Monitoring and CVE vulnerability detection, and authored 6 structured Incident Response reports plus a full SOC triage document.*

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:00B4D8,50:0D2137,100:060D14&height=130&section=footer&animation=fadeIn" width="100%"/>

<br/>

[![Wazuh SIEM](https://img.shields.io/badge/Built%20with-Wazuh%20SIEM-005571?style=flat-square&logo=elastic)](https://wazuh.com)
[![MITRE ATT&CK](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-CC2200?style=flat-square)](https://attack.mitre.org)
[![Lab Type](https://img.shields.io/badge/Lab%20Type-SOC%20%2F%20Blue%20Team-1a7a4a?style=flat-square)](#)
[![Level](https://img.shields.io/badge/Level-Junior%20SOC%20Analyst-6A0DAD?style=flat-square)](#)
[![VirtualBox](https://img.shields.io/badge/Virtualised%20on-VirtualBox-183A61?style=flat-square&logo=virtualbox)](https://www.virtualbox.org)

<br/>

**⭐ If this lab helped your own SOC journey, a star is always appreciated.**

<sub>Built with open-source tools · 100% reproducible · Portfolio-ready</sub>

</div>
