# 🛡️ SOC Threat Hunting with Splunk – Labs & Detection Techniques

This repository documents my hands-on threat hunting labs using **Splunk Enterprise** 

The labs simulate real-world attack scenarios and use Splunk to detect and analyze adversary techniques aligned with **MITRE ATT&CK**.

---

## 🔍 Topics Covered

- ✅ Splunk Installation & App Setup (BOTS, Sysmon, etc.)
- ✅ Hunting with SPL: `top`, `rare`, regex, eval, etc.
- ✅ IOC Detection: DNS, SMB, Web Uploads
- ✅ Process Injection, Mimikatz, LSASS, Svchost LOLBAS
- ✅ Lateral Movement: PsExec, WinRM, WMI
- ✅ Credential Attacks: Pass-the-Hash, Pass-the-Ticket, Kerberoasting, DCSync
- ✅ Anomaly Detection with MLTK (Gaussian, Standard Deviation)
- ✅ CTI Enrichment: MISP, AlienVault, VirusTotal, ChatGPT Integration
- ✅ Beaconing & DNS Tunneling with RITA + Zeek
- ✅ Automation & Integration Labs

---

## ⚒️ Lab Environment

| Component         | Tool / Platform                                 |
|------------------|--------------------------------------------------|
| **SIEM**         | Splunk Enterprise (Developer License)            |
| **Endpoints**    | Windows 10 (Sysmon, Atomic Red Team)             |
| **Servers**      | Ubuntu (Web, Honeypot), Windows Server (AD)      |
| **Firewall**     | Palo Alto NGFW (syslog to Splunk)                |
| **Threat Feeds** | MISP, AlienVault OTX, VirusTotal API             |
| **ML/Analytics** | Splunk MLTK, RITA + Zeek + MongoDB               |
| **Enrichment**   | ChatGPT, DNS tools, CTI modules                  |

---

## 🔐 Network Topology – Zones & IP Schema

| Zone             | Subnet            | VM(s)                                             | Notes                              |
|------------------|-------------------|---------------------------------------------------|-------------------------------------|
| Inside Network   | 10.1.1.0/24       | Windows10: 10.1.1.10                              | User/attacker endpoint              |
| DMZ Network      | 10.1.2.0/24       | AD-Konoha: 10.1.2.10, WebServer: 10.1.2.11, Honeypot: 10.1.2.12, Kali: 10.1.2.100 | Public-facing, exposed services     |
| Management Net   | 10.1.3.0/24       | Splunk Server: 10.1.3.12, Wazuh: 10.1.3.11, Docker-Server: 10.1.3.10 | Security tools & backend            |
| Outside Network  | 192.168.0.0/24    | Kali (ext): 192.168.0.100                         | Internet simulation (optional)      |

---


## 🧐 About Me

I’m a Network Security Engineer with 8+ years of experience. This project reflects my applied learning and readiness for real-world detection and incident response roles using Splunk and CTI tools.

🔗 [LinkedIn](https://www.linkedin.com/in/jordan-moran-ab5994108/)  
🔗 [GitHub](https://github.com/jomocasec1990)
