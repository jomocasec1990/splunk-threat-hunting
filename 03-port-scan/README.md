# Linux Port Scanning Detection Lab using Auditd and Splunk

This lab demonstrates how to detect port scanning activity on a Linux system (Uzumaki) using `auditd` and visualize the behavior in Splunk.

## 🧱 Environment

- **Victim machine (Uzumaki)**: Ubuntu-based server with `auditd` and Splunk Universal Forwarder.
- **Attacker machine**: Kali Linux performing the scan.
- **Monitoring platform**: Splunk.

---

## 🛠️ Configuration Steps

### 1. Install common services on the victim machine
```bash
sudo apt update && sudo apt install -y apache2 vsftpd openssh-server samba nfs-kernel-server
```

### 2. Configure audit rules

Edit the file `/etc/audit/rules.d/audit.rules`:
```bash
## Reset and buffer configuration
-D
-b 8192
--backlog_wait_time 60000
-f 1

## Monitor sensitive files
-w /etc/passwd -p rwa -k passwd_monitoring
-w /etc/shadow -p rwa -k shadow_monitoring

## Monitor network syscall activity
-a always,exit -F arch=b64 -S connect,sendto,recvfrom -F key=netmon
-a always,exit -F arch=b32 -S connect,sendto,recvfrom -F key=netmon

## Monitor command execution
-a always,exit -F arch=b64 -S execve -k exec_logging
-a always,exit -F arch=b32 -S execve -k exec_logging
```

Apply the rules and restart auditd:
```bash
sudo augenrules --load
sudo systemctl restart auditd
```

---

## 🔎 Attack Simulation

From the Kali Linux machine, execute:
```bash
nmap -sS -T4 --top-ports 1000 10.1.2.12
```

This will trigger `connect` syscalls logged by auditd on the target system.

---

## 📥 Data In Splunk

Ensure the Splunk Universal Forwarder is configured and logs from `/var/log/audit/audit.log` are being sent with:

- `sourcetype="linux:auditd"`
- `index=linux_audit`

---

## 🔍 SPL Query

The following SPL query identifies potential scanning behavior:
```spl
index=linux_audit sourcetype="linux:auditd" type=SOCKADDR
| eval exact_time=_time
| bucket _time span=1h
| stats values(lport) as ports_scanned values(rhost) as targets_scanned dc(lport) as num_ports dc(rhost) as num_ips min(exact_time) as first_seen_time max(exact_time) as last_seen_time by _time laddr
| where num_ports > 10 OR num_ips > 10
| rename laddr as src_ip
| eval first_seen_time = strftime(first_seen_time, "%Y-%m-%d %H:%M:%S")
| eval last_seen_time = strftime(last_seen_time, "%Y-%m-%d %H:%M:%S")
| table _time first_seen_time last_seen_time src_ip ports_scanned targets_scanned num_ports num_ips
| sort - _time
```

---



## 📸 Screenshot

> ![Splunk Search Result](./screenshots/splunk_search.png)

