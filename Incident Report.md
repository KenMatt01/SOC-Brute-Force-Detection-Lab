# Incident Report: SSH Brute Force Attack Detection

![Type](https://img.shields.io/badge/Incident%20Type-Brute%20Force-red) ![Severity](https://img.shields.io/badge/Severity-Medium--High-orange) ![Status](https://img.shields.io/badge/Status-Resolved-brightgreen) ![MITRE](https://img.shields.io/badge/MITRE-T1110%20Brute%20Force-blue)

---

## 1. Executive Summary

A brute force attack targeting the SSH service was simulated and successfully detected using **Wazuh SIEM**. The attack involved multiple failed authentication attempts from a single source IP address within a short time frame. The activity was identified, analyzed, and mitigated following standard SOC procedures.

---

## 2. Incident Details

| Field                  | Details                          |
|------------------------|----------------------------------|
| **Incident Type**      | Brute Force Attack (Credential Access) |
| **MITRE ATT&CK**       | [T1110 – Brute Force](https://attack.mitre.org/techniques/T1110/) |
| **Severity Level**     | Medium–High                      |
| **Detection Source**   | Wazuh SIEM                       |
| **Log Source**         | `/var/log/auth.log`              |

---

## 3. Timeline of Events

| Time (UTC) | Event Description                                      |
|------------|--------------------------------------------------------|
| **T0**     | Multiple failed SSH login attempts initiated           |
| **T1**     | Wazuh generated alerts for authentication failures     |
| **T2**     | Alert escalation due to repeated failed attempts       |
| **T3**     | Analyst investigation initiated                        |
| **T4**     | Attack pattern confirmed as brute force activity       |
| **T5**     | Mitigation actions applied                             |

---

## 4. Detection & Analysis

### Detection

The attack was detected through **Wazuh SIEM**, which generated alerts indicating:

- Multiple authentication failures
- Repeated login attempts from a single source IP
- Maximum authentication attempts exceeded

### Log Evidence

The following entries were observed in `/var/log/auth.log`:

```
Failed password for user from 192.168.1.119 port 60066 ssh2
Failed password for user from 192.168.1.119 port 60078 ssh2
Failed password for user from 192.168.1.119 port 57266 ssh2
```

### Analysis

| Field              | Details                                         |
|--------------------|-------------------------------------------------|
| **Source IP**      | `192.168.1.119` (Attacker machine)              |
| **Target Service** | SSH (port 22)                                   |
| **Attack Pattern** | High-frequency failed login attempts            |
| **Behavior**       | Consistent with automated brute force (e.g., Hydra) |

The repeated authentication failures within a short time window confirmed brute force activity.

---

## 5. Impact Assessment

| Area                   | Status                  |
|------------------------|-------------------------|
| Successful Login       | ❌ None observed        |
| Unauthorized Access    | ❌ Not gained           |
| System Integrity       | ✅ Remained intact      |

> ⚠️ The attack highlights the risk of weak authentication mechanisms and potential exposure to credential compromise.

---

## 6. Response Actions

The following actions were taken:

1. **Identified** and analyzed the source IP address (`192.168.1.119`)
2. **Simulated** blocking of attacker IP using firewall rules
3. **Recommended** SSH hardening measures:
   - Disable password-based authentication
   - Enforce SSH key-based login
   - Implement rate limiting or Fail2Ban

---

## 7. Lessons Learned

- SIEM solutions are effective in detecting brute force attempts through log correlation
- Monitoring authentication logs is critical for early detection
- Weak authentication configurations increase attack surface
- Rapid response can prevent escalation and compromise

---

## 8. Recommendations

| Priority | Recommendation                                          |
|----------|---------------------------------------------------------|
| 🔴 High  | Implement multi-factor authentication (MFA)             |
| 🔴 High  | Enforce SSH key-based login, disable password auth      |
| 🟠 Medium | Deploy intrusion prevention mechanisms (e.g., Fail2Ban) |
| 🟠 Medium | Enforce strong password policies                        |
| 🟡 Low   | Continuously monitor and tune SIEM alert rules          |

---

## 9. Conclusion

The simulated brute force attack was successfully detected and analyzed using **Wazuh SIEM**. The exercise demonstrated the importance of log monitoring, alert correlation, and timely response in identifying credential-based attacks. This scenario reflects real-world SOC operations and reinforces best practices in threat detection and incident response.
