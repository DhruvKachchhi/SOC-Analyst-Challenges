# Detecting and Removing Malicious Cron Jobs

## Objective

The objective of this lab was to understand how attackers can use cron jobs to maintain persistence on Linux systems. The lab simulated a malicious scheduled task, investigated its behavior, and demonstrated the basic incident response process to detect, analyze, contain, and remove the unauthorized cron job.

---

## What is a Cron Job?

A cron job is a scheduled task that automatically executes commands or scripts at predefined intervals on Unix and Linux systems. While cron is commonly used for system administration tasks such as backups, updates, and monitoring, attackers can abuse it to establish persistence by repeatedly executing malicious scripts.

Unauthorized cron jobs should be investigated immediately, as they may indicate a compromised system or an attempt to maintain long-term access.

---

## Lab Environment

| Component           | Details                               |
| ------------------- | ------------------------------------- |
| Operating System    | Ubuntu                                |
| Shell               | Bash                                  |
| Scheduled Task      | Cron Job                              |
| Simulated Script    | `/tmp/malicious.sh`                   |
| Investigation Tools | `crontab`, `grep`, `cat`, `systemctl` |

---

## Commands Used

```bash
echo -e '#!/bin/bash\necho "Ping from attacker server" >> /tmp/.cron.log' > /tmp/malicious.sh

chmod +x /tmp/malicious.sh

echo "* * * * * /tmp/malicious.sh" >> /var/spool/cron/root

sudo systemctl status cron

crontab -l

grep -r "/tmp/" /etc/cron* /var/spool/cron/crontabs

cat /tmp/.cron.log

cat /tmp/malicious.sh

crontab -l | grep -v "malicious.sh" | crontab -

rm -f /tmp/malicious.sh /tmp/.cron.log

sudo systemctl restart cron
```

---

## Lab Procedure

1. Created a simulated malicious Bash script in the `/tmp` directory.
2. Made the script executable.
3. Added a cron job to execute the script automatically every minute.
4. Verified the cron service was running.
5. Investigated scheduled tasks using `crontab` and searched for suspicious cron entries.
6. Reviewed the generated log file and inspected the script contents.
7. Removed the unauthorized cron job.
8. Deleted the malicious script and its associated log file.
9. Restarted the cron service to complete the remediation process.

---

## Observations

* The cron job executed the scheduled Bash script automatically.
* The script generated output in `/tmp/.cron.log`, confirming execution.
* The unauthorized scheduled task was identified through cron configuration inspection.
* Removing the cron entry and deleting the script successfully eliminated the persistence mechanism.

---

## SOC Analyst Perspective

Cron jobs are a common persistence technique used by attackers on Linux systems. During an investigation, SOC analysts should review user and system crontabs, identify unauthorized scheduled tasks, inspect associated scripts, and determine whether additional malicious activity occurred. Timely removal of unauthorized cron jobs helps prevent attackers from maintaining persistent access.

---

## Key Learnings

* Understood how cron jobs function on Linux systems.
* Learned how attackers can abuse scheduled tasks for persistence.
* Investigated cron configurations to identify unauthorized entries.
* Analyzed the behavior of a scheduled Bash script.
* Removed malicious cron entries and associated files.
* Applied the Incident Response lifecycle to a Linux persistence scenario.

---

## Conclusion

This lab demonstrated how malicious cron jobs can be used to maintain persistence on Linux systems. By investigating scheduled tasks, analyzing the associated script, and removing unauthorized entries, the exercise reinforced the importance of monitoring cron configurations as part of Linux incident response and threat hunting activities.
