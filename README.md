# 🛡️ SOC Threat Hunting Lab with Splunk  
### Threat Hunting • Detection Engineering • SOC Monitoring

This repository documents my personal SOC and Threat Hunting laboratory built around **Splunk Enterprise** for developing and testing detection logic, monitoring workflows, and security investigations in a realistic enterprise-like environment.

The purpose of this lab is to strengthen practical skills related to:

- Threat Hunting
- Detection Engineering
- Log Analysis
- Security Monitoring
- SOC Investigations
- MITRE ATT&CK mapping
- Endpoint & Network Telemetry Analysis
- SIEM Dashboard Development

Rather than focusing on offensive security or exploitation, this lab is centered on the **defensive side of cybersecurity**, simulating how a SOC analyst or detection engineer investigates suspicious behavior using real telemetry sources.

---

# 🔥 What This Lab Includes

This environment integrates multiple security technologies and log sources to create centralized visibility across endpoints, servers, network traffic, and authentication activity.

The lab includes:

- Splunk dashboards
- Detection logic using SPL
- Threat hunting scenarios
- Authentication monitoring
- Network traffic analysis
- Suricata IDS telemetry
- Sysmon endpoint visibility
- Windows & Linux log analysis
- IOC enrichment workflows
- MITRE ATT&CK aligned detections
- Security investigations and analysis

All dashboards, detections, and searches are developed and tested inside my own SOC lab environment.

---

# 🧪 SOC Lab Environment

| Component | Tool / Platform |
|---|---|
| **SIEM** | Splunk Enterprise (Developer License) |
| **Endpoints** | Windows 10 + Sysmon |
| **Servers** | Ubuntu Web Server, Honeypot, Windows Server AD |
| **Firewall** | Palo Alto NGFW (Syslog → Splunk) |
| **IDS** | Suricata |
| **Threat Intelligence** | MISP, AlienVault OTX, VirusTotal |
| **Analytics** | Splunk MLTK, Zeek, RITA |
| **Enrichment** | DNS tools, CTI modules |

---

# 🌐 Network Topology

## 🔹 Inside Network — 10.1.1.0/24

| Host | Role |
|---|---|
| Windows10 – 10.1.1.10 | Endpoint telemetry |

---

## 🔹 DMZ Network — 10.1.2.0/24

| Host | Role |
|---|---|
| AD-Konoha – 10.1.2.10 | Active Directory |
| WebServer – 10.1.2.11 | Apache Web Services |
| Kali Linux – 10.1.2.100 | Internal testing system |

---

## 🔹 Security Operations Network — 10.1.3.0/24

| Host | Role |
|---|---|
| Splunk – 10.1.3.12 | SIEM & dashboards |


---

# 🎯 Main Focus Areas

- Threat Hunting with Splunk
- Detection Engineering
- SOC Dashboards
- Authentication Monitoring
- Port Scan Detection
- Reconnaissance Detection
- PowerShell Monitoring
- IDS Log Analysis
- MITRE ATT&CK Mapping
- IOC Enrichment
- Endpoint Telemetry Analysis

---

# 🧠 About This Project

This repository reflects my hands-on learning process in defensive cybersecurity and SOC operations.

Every dashboard, search, and detection included here is designed to improve practical visibility into attacker behavior, suspicious activity, and security monitoring workflows using centralized telemetry and SIEM analysis.

The lab continues evolving as I build new detections, dashboards, and hunting methodologies.

---

# 👨‍💻 About Me

I’m a Network Security Engineer with 8+ years of experience focused on:

- Network Security
- Threat Detection
- SIEM Monitoring
- Palo Alto Technologies
- SOC Operations
- Detection Engineering

This project represents my practical work and continuous learning in threat hunting and security monitoring.

🔗 [LinkedIn](https://www.linkedin.com/in/jordan-moran-ab5994108/)  
🔗 [GitHub](https://github.com/jomocasec1990)
