# SSH Brute Force Detection Lab (Wazuh SIEM)

![Security](https://img.shields.io/badge/Category-Cybersecurity-red) ![SIEM](https://img.shields.io/badge/SIEM-Wazuh-blue) ![MITRE](https://img.shields.io/badge/MITRE-T1110%20Brute%20Force-orange) ![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

## Overview

This project simulates a brute force attack against an SSH service and demonstrates detection, analysis, and response using Wazuh SIEM. The objective was to replicate a real-world SOC scenario involving credential access attempts and log-based detection.
Brute force attacks are one of the most common techniques used to gain unauthorized access to systems. This lab demonstrates how SOC analysts detect and respond to such attacks using SIEM tools and log analysis.

This project reflects real-world SOC operations, including alert triage, investigation, and incident response.

---

## Lab Architecture

| Role     | System             | Tool  |
|----------|--------------------|-------|
| Attacker | Kali Linux         | Hydra |
| Target   | Ubuntu Server      | SSH   |
| SIEM     | Wazuh              | —     |

---

## SOC Workflow

1. Attack Simulation (Hydra brute force)
2. Log Generation (/var/log/auth.log)
3. Log Ingestion (Wazuh Agent → Manager)
4. Alert Generation (SIEM rules triggered)
5. Investigation (log correlation + IP analysis)
6. Response (IP blocking + SSH hardening)

---

## Attack Simulation

A brute force attack was launched using **Hydra**:

```bash
hydra -l user -P rockyou.txt ssh://<target-ip>
```

This generated multiple failed authentication attempts against the SSH service.

---

## Detection (Wazuh SIEM)

Wazuh detected the activity and generated the following alerts:

- 🔴 Multiple authentication failures
- 🔴 Maximum authentication attempts exceeded
- 🔴 PAM: User login failed

**MITRE ATT&CK Mapping:**

| Technique ID | Name        |
|--------------|-------------|
| [T1110](https://attack.mitre.org/techniques/T1110/) | Brute Force |

---

## Log Analysis

Relevant logs were observed in:

```
/var/log/auth.log
```

**Example log entry:**

```
Failed password for user from 192.168.x.x port xxxx ssh2
```

This confirmed repeated unauthorized access attempts from the attacker machine.

---

## Response Actions

1. **Identified** attacker IP address from logs
2. **Simulated** blocking via firewall rules
3. **Recommended** SSH hardening measures:
   - Disable password authentication
   - Enforce key-based login only

---

## Screenshots

### Attack — Hydra
<img width="917" height="397" alt="Hydra Attacks" src="https://github.com/user-attachments/assets/68c03c96-d74a-4cdb-8157-141135353088" />


### Wazuh Alerts
<img width="1875" height="807" alt="Wazuh Alerts" src="https://github.com/user-attachments/assets/be3ce0a8-0e82-48b3-ac12-8dffdc8e7224" />

<img width="1880" height="344" alt="charts" src="https://github.com/user-attachments/assets/458bd325-4153-4a52-94f2-96bfdf0202c1" />


### Authentication Logs
<img width="1229" height="521" alt="Logs" src="https://github.com/user-attachments/assets/4e351abf-2581-4075-bbcf-c213b6e13522" />


---

## Tools Used

| Tool          | Purpose                        |
|---------------|--------------------------------|
| Wazuh SIEM    | Alert generation & log analysis |
| Kali Linux    | Attacker machine               |
| Hydra         | Brute force tool               |
| Ubuntu Server | Target machine (SSH)           |

---

## Key Learnings

- SIEM-based detection of brute force attacks
- Log correlation and alert analysis
- Mapping events to MITRE ATT&CK framework
- Incident response workflow in a SOC context

---

## Future Improvements

- Add privilege escalation detection
- Implement automated response (SOAR integration)
- Extend to multi-attack scenarios

---

> ⚠️ **Disclaimer:** This lab was conducted in a controlled, isolated environment for educational purposes only. Do not attempt to replicate these techniques on systems you do not own or have explicit permission to test.
