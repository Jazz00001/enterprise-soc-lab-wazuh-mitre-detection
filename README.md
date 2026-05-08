# enterprise-soc-lab-wazuh-mitre-detection
Mini enterprise SOC lab using Wazuh SIEM/XDR with Windows and Linux endpoints, MITRE ATT&amp;CK mapping, vulnerability detection, and incident reports.

![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Wazuh%204.7.5-blue?style=flat-square&logo=linux)
![OS](https://img.shields.io/badge/Endpoints-Windows%2010%20%7C%20Ubuntu%2022.04-orange?style=flat-square)
![MITRE](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-red?style=flat-square)
![Reports](https://img.shields.io/badge/Incident%20Reports-6-purple?style=flat-square)
![Detections](https://img.shields.io/badge/Detections-7-yellow?style=flat-square)
# Enterprise SOC Lab — Wazuh SIEM/XDR with MITRE ATT&CK Detection

## Table of Contents
- [Overview](#overview)
- [Lab Architecture](#lab-architecture)
- [Attack Simulations](#attack-simulations)
- [Detections and MITRE ATT&CK Mapping](#detections-and-mitre-attck-mapping)
- [Incident Reports](#incident-reports)
- [Full SOC Triage Report](#full-soc-triage-report)
- [Detection Rules](#detection-rules)
- [Screenshots](#screenshots)
- [Key Skills Demonstrated](#key-skills-demonstrated)
- [Lessons Learned](#lessons-learned)
- [Future Improvements](#future-improvements)
- [Resume Bullet](#resume-bullet)

## Overview
This project is a mini enterprise SOC lab built using Wazuh SIEM/XDR. The lab simulates, detects, and investigates real-world attack techniques across Windows and Linux endpoints.

The environment includes a Wazuh 4.7.5 all-in-one server, a Windows 10 endpoint with Sysmon, and an Ubuntu 22.04.5 endpoint. The project demonstrates log collection, alert triage, MITRE ATT&CK mapping, File Integrity Monitoring, vulnerability detection, and formal incident report writing.

## Lab Architecture

![Lab](architecture/Lab.png)

| Component | Tool / OS | Role | IP Address |
|---|---|---|---|
| SIEM/XDR | Wazuh 4.7.5 | Manager, Dashboard, Indexer, alerting, FIM | 192.168.56.102 |
| Endpoint 1 | Windows 10 + Sysmon | Windows logs, process monitoring, PowerShell detection | 192.168.56.101 |
| Endpoint 2 | Ubuntu 22.04.5 | Linux auth logs, SSH monitoring, sudo monitoring, FIM | 192.168.56.103 |
| Virtualisation | VirtualBox | Host-only lab network | 192.168.56.0/24 |

## Attack Simulations

| # | Attack / Detection | Platform | Status |
|---|---|---|---|
| 1 | Brute force failed logins | Windows | Completed |
| 2 | Suspicious PowerShell execution | Windows | Completed |
| 3 | New local user creation | Windows | Completed |
| 4 | SSH brute force | Linux | Completed |
| 5 | File Integrity Monitoring — `/etc/hosts` modified | Linux | Completed |
| 6 | Privilege escalation using sudo | Linux | Completed |

## Detections and MITRE ATT&CK Mapping

| Detection | Log Source | MITRE ID | Technique | Tactic | Severity |
|---|---|---|---|---|---|
| Windows failed logins | Windows Security Log | T1110.001 | Brute Force: Password Guessing | Credential Access | High |
| Suspicious PowerShell execution | Sysmon / Windows Event Logs | T1059.001 | Command and Scripting Interpreter: PowerShell | Execution / Defense Evasion | High |
| New local user created | Windows Security Log | T1136.001 | Create Account: Local Account | Persistence | Medium |
| SSH brute force | Linux `/var/log/auth.log` | T1110.001 | Brute Force: Password Guessing | Credential Access | High |
| File `/etc/hosts` modified | Wazuh FIM / Syscheck | T1565.001 | Stored Data Manipulation | Impact | Medium |
| Sudo privilege escalation | Linux `/var/log/auth.log` | T1548.003 | Sudo and Sudo Caching | Privilege Escalation | High |
| Vulnerability detection | Wazuh Vulnerability Detector | N/A | CVE exposure / vulnerability management | Risk Management | High |
## Screenshots
### Wazuh Dashboard

![Wazuh Dashboard](screenshots/Wazuh-dashboard.png)

### Both Agents Active

![Agents Connected](screenshots/agents-connected)

### Brute Force Alert

![Windows Brute Force Alert](screenshots/brute-force-alert)

### Suspicious PowerShell Execution

![PowerShell Alert](screenshots/powershell-alert)

### New Local User Creation

![New User Alert](screenshots/new-user-alert)

### Linux SSH Brute Force

![Linux SSH Brute Force](screenshots/linux-ssh-brute-force-alert)

### File Integrity Monitoring

![FIM Alert](screenshots/fim-alert)

### Linux Sudo Privilege Escalation

![Sudo Privilege Escalation](screenshots/sudo-privilege-escalation-alert)

### MITRE ATT&CK Dashboard

![MITRE Dashboard](screenshots/mitre-dashboard)

### Vulnerability Detection 

![Vulnerability Scan](screenshots/vulnerability-scan-ubuntu)


## Incident Reports

- [IR-001: Windows Brute Force Failed Logins](Reports/IR-001-Windows-Brute-Force-Failed-Logins.pdf)
- [IR-002: Suspicious PowerShell Execution](Reports/IR-002-Suspicious-PowerShell-Execution.pdf)
- [IR-003: New Local User Creation — Windows](Reports/IR-003-New-Local-User-Creation-Windows.pdf)
- [IR-004: Linux SSH Brute Force](Reports/IR-004-Linux-SSH-Brute-Force.pdf)
- [IR-005: File Integrity Monitoring — Hosts File Modified](Reports/IR-005-File-Integrity-Monitoring-Hosts-Modified.pdf)
- [IR-006: Linux Sudo Privilege Escalation](Reports/IR-006-Linux-Sudo-Privilege-Escalation.pdf)

## Full SOC Triage Report

- [Full SOC Triage Report](SOC-Lab-Full-Triage-Report.pdf)

## Detection Rules

This lab relied on Wazuh built-in rules for detections. Custom rule examples demonstrating additional detection logic are provided in the Rules/ folder.

- [Custom Rules XML](Rules/custom-rules.xml)

Confirmed built-in rules included:

| Rule ID | Description | Area |
|---|---|---|
| 92057 | PowerShell encoded command | Windows suspicious execution |
| 92027 | PowerShell process spawned PowerShell instance | Windows process behavior |
| 5710 | SSH login using non-existent user | Linux SSH authentication |
| 2502 | User missed the password more than one time | Linux authentication failure |
| 5402 | Successful sudo to ROOT executed | Linux sudo monitoring |
| 5404 | Three failed attempts to run sudo | Linux sudo failed attempts |
| 550 | Integrity checksum changed | FIM / Syscheck |

## Key Skills Demonstrated

- Wazuh SIEM/XDR deployment and configuration
- Windows and Linux agent setup
- Sysmon deployment and Windows event collection
- Linux authentication log monitoring
- SSH brute-force detection
- PowerShell suspicious execution detection
- Windows account activity monitoring
- File Integrity Monitoring
- Linux sudo privilege escalation detection
- MITRE ATT&CK mapping
- Vulnerability detection and CVE review
- SOC alert triage and incident report writing
- GitHub project documentation

## Lessons Learned

1. I learned how a SIEM collects logs from multiple endpoints and turns raw events into useful security alerts.
2. I learned how Windows Sysmon improves visibility into process creation and suspicious PowerShell activity.
3. I learned how Linux authentication logs reveal SSH brute-force attempts and sudo privilege escalation behavior.
4. I learned how MITRE ATT&CK helps explain attacker behavior in a structured way.
5. I learned that documentation is a major part of SOC work because an analyst must explain what happened, why it matters, and how to respond.

## Future Improvements

- Add a dedicated Kali attacker VM.
- Fully implement and test custom Wazuh rules with custom rule IDs.
- Enable Wazuh Active Response to automatically block brute-force source IPs.
- Add Slack or email alerting for high-severity alerts.
- Export raw JSON evidence for important alerts.
- Create a cleaner network diagram using draw.io or Canva.
  ![Lab Network Architecture](architecture/Network.png)

## Resume Bullet

Built a mini enterprise SOC lab using Wazuh SIEM/XDR with Windows Sysmon and Ubuntu Linux endpoints. Configured log collection, simulated 6 attack scenarios, mapped detections to the MITRE ATT&CK framework, enabled FIM and vulnerability detection, and documented formal incident investigation reports.
