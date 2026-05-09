# 🚨 Incident Report – SSH Brute Force Attack

---

## 📌 Executive Summary

**Incident ID:** IR-SSH-001  
**Severity:** High (P2)  
**Status:** Confirmed Compromise  

### 🧾 Overview

On May 5th, 2026, multiple failed SSH authentication attempts were detected on server **Uchiha**. The activity originated from IP **185.220.101.1**, later identified as a **TOR exit node** with a high abuse score.

After multiple failed attempts, a **successful login to the `admin` account** was observed, confirming unauthorized access.

---

## 🔍 Key Findings

- 136 failed SSH login attempts detected  
- Attack originated from TOR node (anonymous attacker)  
- Targeted valid usernames (`admin`, `root`, `mysql`)  
- Successful authentication achieved  
- Confirmed brute force compromise  

---

## 🧪 Technical Analysis

### 📡 Detection Query

```spl
index=linux_auth host=Uchiha sourcetype=linux_secure app=ssh action=failure
| stats count by src
| sort - count
```

### 📸 Evidence

![Brute Force Attempts](./Screenshots/Investigation01.png)

### 🧾 Result

- **Source IP:** 185.220.101.1  
- **Failed attempts:** 136  

---

### 👤 Username Enumeration

```spl
index=linux_auth host=Uchiha sourcetype=linux_secure app=ssh action=failure src=185.220.101.1
| eval username=if(match(_raw,"invalid user"),"invalid_user",user)
| stats count by username
| sort - count
```

### 📸 Evidence

![Username Enumeration](./Screenshots/Investigation03.png)

### 🧾 Result

Targeted users:

- admin  
- root  
- mysql  
- invalid users  

---

### ⏱ Timeline Analysis

```spl
index=linux_auth host=Uchiha sourcetype=linux_secure src=185.220.101.1
| eval "Date and Time" = strftime(_time,"%Y-%m-%d %H:%M:%S")
| table "Date and Time" action user src
| sort "Date and Time"
```

### 📸 Evidence

![Timeline](./Screenshots/Investigation04.png)

### 🧾 Findings

- High-frequency attempts within seconds  
- Automated attack behavior (likely brute force tool)  

---

### 🔐 Successful Login Detection

```spl
index=linux_auth host=Uchiha sourcetype=linux_secure "Accepted password" src=185.220.101.1
| table _time action user src
```

### 📸 Evidence

![Successful Login](./Screnshots/Investigation05.png)

### 🧾 Result

- Successful login detected  
- **Compromised account:** `admin`  

---

## 🌍 Indicators of Compromise (IoCs)

- **IP Address:** 185.220.101.1  
- **Type:** TOR Exit Node  
- **Abuse Score:** 100%  
- **Behavior:** SSH brute force + successful authentication  

### 📸 Threat Intelligence Evidence

![AbuseIPDB](./Screenshots/Investigation02.png)

---

## 🧠 Root Cause Analysis

- There was a weak or guessable password for `admin`  
- SSH was exposed to external network
- There wasn o brute force protection such fail2ban, rate limiting, etc.  
- No MFA or key-based authentication enforced on the server

---

## ⏱ Technical Timeline

| Time       | Event                              |
|-----------|------------------------------------|
| 07:37:xx  | Multiple failed SSH attempts       |
| 07:37:47  | Successful login detected          |
| Post-login| Unauthorized access confirmed      |

---

## ⚠️ Impact Analysis

- There has been a compromise of valid credentials  
- There has unauthorized SSH access  

### Potential Impact:

- Privilege escalation  
- Persistence  
- Lateral movement  

---

## 🛡️ Response Actions

- Identified compromised account (`admin`)  
- Validated source IP reputation  
- Confirmed successful login event  
- Analyzed authentication logs  

---

## 🔄 Recommendations

- Reset compromised credentials immediately  
- Disable SSH password authentication  
- Enable SSH key-based authentication  
- Implement brute force protection (fail2ban)  
- Restrict SSH access via firewall  
- Monitor for post-compromise activity  

---

## 📚 Lessons Learned

- Brute force attacks can escalate quickly to compromise  
- Exposure of SSH without controls is high risk  
- Threat intelligence enrichment adds critical context  
- Detection must include both failure AND success correlation  
