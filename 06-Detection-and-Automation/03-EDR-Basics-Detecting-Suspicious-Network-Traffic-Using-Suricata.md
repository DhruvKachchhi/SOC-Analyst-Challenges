# Day #29: EDR Basics – Detecting Suspicious Network Traffic Using Suricata

## 🎯 Objective

The objective of this lab was to detect suspicious network traffic by integrating **Suricata IDS** with **Wazuh SIEM**. A simulated reconnaissance attack was performed using **Nmap** from a Kali Linux machine, and the generated alerts were monitored and analyzed through the Wazuh Dashboard.

---

# 🛠️ Lab Environment

| Component | Details |
|-----------|---------|
| Wazuh Server | Ubuntu Server with Wazuh Manager & Dashboard |
| Wazuh Agent | Ubuntu 24.04 LTS |
| IDS | Suricata |
| Attacker Machine | Kali Linux |
| Attack Tool | Nmap |
| Detection Platform | Wazuh Dashboard |

---

# 📌 Implementation Steps

## Step 1 – Verify Suricata & Wazuh Agent

- Verified that the **Suricata IDS** service was running successfully.
- Confirmed the **Wazuh Agent** was active and forwarding logs.

**Screenshot**

![03.1-Suricata-and-Wazuh-Agent-Service-Status](../Screenshots/Day-29/03.1-Suricata-and-Wazuh-Agent-Service-Status.png)

---

## Step 2 – Simulate Network Reconnaissance

From the Kali Linux attacker machine, multiple Nmap scans were performed against the Ubuntu endpoint.

Example commands used:

```bash
nmap -sS -T4 192.168.56.103
```

During the scan, Suricata monitored the traffic and generated network events in the **eve.json** log.

**Screenshot**

![03.2-Nmap-Port-Scan-and-Suricata-Logs](../Screenshots/Day-29/03.2-Nmap-Port-Scan-and-Suricata-Logs.png)

---

## Step 3 – Analyze Alerts in Wazuh

After the scan, Wazuh successfully parsed the Suricata logs and generated multiple security alerts.

Detected events included:

- ET SCAN Potential VNC Scan
- ET SCAN Suspicious inbound MySQL Port
- ET SCAN Suspicious inbound PostgreSQL Port
- ET SCAN Suspicious inbound MSSQL Port
- ET SCAN Suspicious inbound Oracle SQL Port

**Screenshot**

![03.3-Wazuh-Suricata-Alerts](../Screenshots/Day-29/03.3-Wazuh-Suricata-Alerts.png)

---

## Step 4 – Investigate Alert Details

The generated alert was opened to inspect detailed information including:

- Source IP Address
- Destination IP Address
- Destination Port
- Alert Signature
- Alert Severity
- Event Type
- Network Flow Information

This demonstrates how security analysts investigate suspicious network activity using Wazuh.

**Screenshot**

![03.4-Suricata-Alert-Details](../Screenshots/Day-29/03.4-Suricata-Alert-Details.png)

---

# 🔍 Detection Summary

| Event | Status |
|--------|--------|
| Suricata Installed | ✅ |
| Wazuh Agent Connected | ✅ |
| Nmap Scan Executed | ✅ |
| Suricata Generated Alerts | ✅ |
| Wazuh Parsed Alerts | ✅ |
| Alert Investigation Completed | ✅ |

---

# 🧠 Key Learnings

- Learned how **Suricata IDS** detects suspicious network traffic.
- Understood how **Nmap reconnaissance** generates IDS alerts.
- Integrated Suricata logs with the **Wazuh Agent**.
- Investigated alerts using the **Wazuh Dashboard**.
- Gained hands-on experience with network threat detection and basic EDR monitoring.

---

# ✅ Conclusion

Successfully configured **Suricata IDS** with **Wazuh SIEM** to monitor network traffic and detect suspicious reconnaissance activity. By performing an Nmap scan from a Kali Linux system, Suricata generated multiple IDS alerts which were collected and visualized in the Wazuh Dashboard. This lab provided practical experience in integrating IDS with a SIEM platform and analyzing network-based security events from a SOC analyst's perspective.
