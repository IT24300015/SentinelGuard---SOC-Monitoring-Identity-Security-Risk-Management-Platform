🛡️ SentinelGuard — SOC Monitoring, Identity Security & Risk Management Platform

📌 Project Overview

SentinelGuard is an end-to-end Security Operations Center (SOC) platform that simulates a real company security environment. The system monitors Windows devices, collects security logs, detects suspicious activities, analyzes employee identities and password risks, generates alerts, investigates incidents, and produces security reports.

The main goal is to detect security threats early and reduce the risk of unauthorized access and cyberattacks.

This project combines three cybersecurity domains into one platform:


🔵 SOC Monitoring — Real-time log collection, SIEM alerting, and threat detection
🟡 Identity Security — Simulated employee accounts, access management, risk scoring
🔴 Risk Management — Password auditing, attack simulation, incident investigation



⭐ This is a strong, complete portfolio project for an entry-level SOC Analyst resume.




🎯 SOC Skills Demonstrated

SkillTool/Method SIEM OperationsSplunk Enterprise Endpoint MonitoringSysmon + Windows Event Logs Log AnalysisSplunk Search & Reporting Threat DetectionCustom Splunk Alerts Alert ManagementScheduled Cron Alerts in Splunk Identity SecuritySimulated Employee Dataset + Local Accounts Password SecurityJohn the Ripper + OpenSSL SHA-512 Attack SimulationKali Linux + netexec SMB Brute-Force Incident InvestigationIOC Analysis + Timeline Reconstruction Risk AssessmentPer-Account Risk Scoring (Low/Medium/High/Critical) Security ReportingFull SOC Final Report (PDF + DOCX)


🏗️ System Architecture

               Kali Linux
         (Attack Simulation)
                  │
                  │  SMB Brute-Force (port 445)
                  ▼
    Windows 11 Machine + Sysmon
                  │
                  │  Windows Event Logs
                  ▼
         Splunk Enterprise
                  │
    ┌─────────────┼─────────────┐
    │             │             │
    ▼             ▼             ▼
Threat        Identity      Password
Detection     Audit         Audit
    │             │             │
    └─────────────┼─────────────┘
                  │
                  ▼
          Risk Assessment
                  │
                  ▼
          Alert Generation
                  │
                  ▼
       Incident Investigation
                  │
                  ▼
         Security Reports


🛠️ Tools & Technologies

ToolVersionPurposeLocationSplunk Enterprise10.xSIEM — Log ingestion, search, alertingWindows HostSysmonLatestEndpoint telemetry (process, network, file)Windows HostWindows 1122H2+Target endpoint machineReal Host MachineKali Linux2024.xAttack simulation platformVirtualBox VMnetexecv1.xSMB brute-force attack simulationKali LinuxJohn the RipperLatestPassword hash cracking auditKali LinuxOpenSSLLatestSHA-512 password hash generationKali LinuxVirtualBox7.xVirtual machine environmentHost MachinePython3.xAutomation scriptsBoth


📋 Project Phases

PhaseTitleDescriptionStatus1Project PlanningScope, objectives, architecture design Complete2Environment SetupVirtualBox, Windows VM, Kali VM, Splunk, Sysmon Complete3Endpoint MonitoringSysmon config, Windows auditing, Splunk log ingestion Complete4Identity & Access ManagementEmployee dataset, local Windows accounts Complete5Password Security AuditHash generation, John the Ripper cracking, audit report Complete6Threat DetectionSplunk alerts — brute force, privilege escalation, off-hours Complete7Attack SimulationSMB brute-force via netexec from Kali Linux Complete8Incident InvestigationIOC analysis, timeline reconstruction, incident report Complete9Risk AssessmentPer-account risk scoring (Low/Medium/High/Critical) Complete10Security Report GenerationFull SOC final report with evidence and recommendations Complete


🔑 Key Findings

Password Security Audit

AccountPasswordLengthCracked?ReasonjcarterPassword12311 YESDictionary word + number suffixrwilson1234566 YESMost common password globallymlopezSummer2024!11 NoSeasonal pattern but not in top wordlistsjohnsonTr0ub4dor&3xQp9!16 NoLong, complex, high entropycleeK7#mP9$vL2qX12 NoRandom, no dictionary basis


2 of 5 accounts (40%) cracked within seconds using rockyou.txt wordlist



Attack Simulation Results

MetricValueAttack TypeSMB Brute-Force Authentication AttackToolnetexec (Kali Linux)TargetDESKTOP-16UFKJN — 192.168.56.1Total Attempts35 (5 accounts × 7 passwords)Total Failed Login Events in Splunk120Successful Unauthorized Logins0 — No breach confirmedOverall Risk RatingHIGH

Splunk Alerts Configured

Alert NameEvent IDSeverityScheduleBrute Force Detection4625 — 5+ failures in 5 min🔴 HIGHEvery 15 minPrivilege Escalation Detection4672 — non-system accounts🔴 HIGHEvery 15 minOff-Hours Login Detection4624 — outside 09:00–18:00🟡 MEDIUMEvery 15 min


📊 Risk Assessment Summary

AccountDepartmentFailed LoginsPwd CrackedBreachPriv EscRiskrwilsonHR24YES (123456)NoNo🔴 CRITICALjcarterIT24YES (Pwd123)NoNo🔴 HIGHmlopezIT23NoNoNo🟡 MEDIUMsjohnsonFinance23NoNoNo🟡 MEDIUMcleeOperations22NoNoNo🟡 MEDIUM


📁 Repository Structure

SentinelGuard/
│
├── 📂 data/
│   └── employees.csv              # 12 simulated employee accounts dataset
│
├── 📂 reports/
│   ├── SentinelGuard_SOC_Report.pdf   # Final SOC security report (PDF)
│   └── SentinelGuard_SOC_Report.docx  # Final SOC security report (DOCX)
│
├── 📂 screenshots/
│   ├── 01_failed_login_count.png
│   ├── 02_virtualbox_network.png
│   ├── 03_splunk_sourcetypes.png
│   ├── 04_event_viewer_sysmon.png
│   ├── 05_john_ripper_result.png
│   ├── 06_splunk_alerts_page.png
│   ├── 07_brute_force_search.png
│   ├── 08_netexec_attack_output.png
│   ├── 09_attack_events_splunk.png
│   ├── 10_timeline_search.png
│   ├── 11_no_breach_confirmed.png
│   └── 12_employees_csv.png
│
├── 📂 scripts/
│   └── (Python automation scripts)
│
├── 📂 docs/
│   └── (Phase documentation and notes)
│
└── README.md


🔍 Key Splunk Searches Used

splunk# Failed login count by account
index=winlogs sourcetype=WinEventLog:Security EventCode=4625
| stats count by Account_Name | sort -count

# Brute force detection (5+ failures in 5-min window)
index=winlogs sourcetype=WinEventLog:Security EventCode=4625
| bucket _time span=5m
| stats count by Account_Name, _time
| where count >= 5

# Privilege escalation detection (excluding system accounts)
index=winlogs sourcetype=WinEventLog:Security EventCode=4672
| search NOT (Account_Name="SYSTEM" OR Account_Name="LOCAL SERVICE"
  OR Account_Name="NETWORK SERVICE")
| stats count by Account_Name

# Off-hours login detection (outside 09:00-18:00)
index=winlogs sourcetype=WinEventLog:Security EventCode=4624
| eval hour=strftime(_time, "%H")
| where (hour < 9 OR hour > 18)
  AND Account_Name!="DESKTOP-16UFKJN$"
  AND Account_Name!="SYSTEM"
| table _time, Account_Name, hour

# Attack timeline reconstruction
index=winlogs sourcetype=WinEventLog:Security
  (EventCode=4625 OR EventCode=4624 OR EventCode=4672)
| table _time, EventCode, Account_Name | sort _time


🔐 Key Event IDs Monitored

Event IDDescriptionUse Case4624Successful logonOff-hours detection, breach confirmation4625Failed logon attemptBrute-force detection4672Special privileges assignedPrivilege escalation detectionSysmon 1Process creationMalicious process detectionSysmon 3Network connectionLateral movement detection


🚨 Recommendations (from Final Report)

Immediate Actions


🔴 Force password reset for rwilson and jcarter — both cracked in under 20 seconds
🔴 Enable account lockout: lock after 5 failed attempts, 15-minute lockout duration
🔴 Enforce minimum password length of 14 characters
🔴 Restrict SMB access (port 445) via Windows Firewall


Short-Term (Within 30 Days)


🟡 Deploy Multi-Factor Authentication (MFA) for all employee accounts
🟡 Implement password complexity policy banning dictionary words and sequential numbers
🟡 Conduct monthly password audits using John the Ripper


Long-Term


🟢 Expand Splunk monitoring to include network-level events (DNS, firewall logs)
🟢 Implement Privileged Access Management (PAM) solution
🟢 Add anomaly-based detection (baseline normal behaviour, alert on deviations)
🟢 Schedule quarterly red team exercises
🟢 Deploy EDR solution for deeper endpoint visibility



📄 Final Report

The complete SOC Final Security Report is available in the /reports/ folder:


Covers all 10 phases with evidence screenshots
Includes executive summary, findings, IOC analysis, risk ratings, and recommendations
Incident ID: INC-2026-001
Overall Risk Rating: HIGH



🌐 Lab Environment

Host Machine:   Windows 11 (real host) — 192.168.56.1
                Running: Splunk Enterprise, Sysmon, Windows Security Auditing

Attack Machine: Kali Linux (VirtualBox VM) — 192.168.56.x
                Running: netexec, John the Ripper, OpenSSL

Network:        VirtualBox Host-Only Adapter
                Isolated — no exposure to home/external network


👤 Author

Nimesh Nilakshan
SOC Analyst — Portfolio Project


⚠️ Disclaimer

This project was conducted in an isolated, controlled lab environment for educational and portfolio purposes only. All attack simulations were performed against systems owned and controlled by the author. No real systems, networks, or data were harmed or accessed without authorization.
