# 🚨 SSH Brute Force Detection Lab (Wazuh SIEM)

## 📌 Overview
This project simulates a brute force attack against an SSH service and demonstrates detection, analysis, and response using Wazuh SIEM.

The objective was to replicate a real-world SOC scenario involving credential access attempts and log-based detection.


## 🧠 Lab Architecture

- **Attacker:** Kali Linux (Hydra)
- **Target:** Ubuntu Server (SSH enabled)
- **SIEM:** Wazuh


## ⚔️ Attack Simulation

A brute force attack was launched using Hydra:

```bash
hydra -l user -P /usr/share/wordlists/rockyou.txt ssh://<target-ip>
