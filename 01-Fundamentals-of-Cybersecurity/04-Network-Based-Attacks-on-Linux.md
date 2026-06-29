# Network-Based Attack Detection Using UFW

## Objective

The objective of this lab is to understand how network-based reconnaissance attacks, such as port scanning, can be detected using the Uncomplicated Firewall (UFW) on Linux. This exercise demonstrates how firewall logs help SOC analysts identify and investigate suspicious network activity.

---

## What is a Network Port Scan?

A port scan is a reconnaissance technique used to discover open ports and services on a target system. Attackers commonly perform port scans before attempting exploitation to identify potential attack vectors.

---

## What is Nmap?

Nmap (Network Mapper) is a widely used open-source network scanning tool that helps identify:

* Active hosts
* Open ports
* Running services
* Operating system information

Common scan types include:

* SYN Scan (`-sS`)
* TCP Connect Scan (`-sT`)
* UDP Scan (`-sU`)
* Ping Scan (`-sn`)

---

## What is UFW?

UFW (Uncomplicated Firewall) is a user-friendly interface for managing Linux firewall rules. It allows administrators to control inbound and outbound traffic while logging blocked connections for security monitoring.

Firewall logs are stored in:

```text
/var/log/ufw.log
```

---

## Lab Environment

| Component        | Details            |
| ---------------- | ------------------ |
| Attacker Machine | Kali Linux         |
| Target Machine   | Ubuntu Linux       |
| Tool             | Nmap               |
| Firewall         | UFW                |
| Log File         | `/var/log/ufw.log` |

---

## Commands Executed

```bash
sudo apt install ufw
sudo ufw enable
sudo ufw logging on
sudo ufw logging high

sudo ufw deny from <ATTACKER-IP> to any port 80 proto tcp

sudo ufw reload
```

Attack simulation:

```bash
nmap -p80 <TARGET-IP>
```

Monitor firewall logs:

```bash
sudo tail -f /var/log/ufw.log
```

---

## Activities Performed

During this lab, I:

* Configured UFW on the Ubuntu system.
* Enabled firewall logging.
* Created a firewall rule to block HTTP traffic.
* Simulated a port scan from a Kali Linux attacker machine using Nmap.
* Monitored `ufw.log` to observe blocked network connections.

---

## SOC Analyst Perspective

Firewall logs are valuable for detecting reconnaissance activities before an attacker attempts exploitation.

SOC analysts use UFW logs to:

* Detect unauthorized scanning
* Identify suspicious source IP addresses
* Monitor blocked connections
* Investigate potential intrusion attempts
* Improve network security monitoring

---

## Key Learnings

* Understood how UFW records blocked network traffic.
* Learned how Nmap scans appear in firewall logs.
* Gained experience monitoring Linux firewall events.
* Recognized reconnaissance activity from a defender's perspective.

---

## Conclusion

UFW logs provide valuable visibility into blocked network traffic and early-stage reconnaissance attempts. Monitoring these logs helps SOC analysts detect suspicious behavior and respond before attackers can exploit exposed services.

