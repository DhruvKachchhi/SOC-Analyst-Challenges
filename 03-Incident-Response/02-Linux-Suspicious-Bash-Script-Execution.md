# Linux Suspicious Bash Script Execution

## Objective

The objective of this lab was to understand the fundamentals of Incident Response on Linux by simulating the execution of a suspicious Bash script, investigating the running process, and learning the basic steps required to detect, analyze, and contain potential script-based threats.

---

## What is Incident Response?

Incident Response (IR) is a structured process used to detect, analyze, contain, eradicate, and recover from cybersecurity incidents. On Linux systems, suspicious scripts can be used to establish persistence, execute malicious commands, or download additional payloads. Identifying and responding to these activities is an essential responsibility of a SOC Analyst.

The Incident Response lifecycle consists of:

* Preparation
* Detection and Analysis
* Containment, Eradication, and Recovery
* Post-Incident Activity

---

## Lab Environment

| Component           | Details                          |
| ------------------- | -------------------------------- |
| Operating System    | Ubuntu                           |
| Terminal            | Bash                             |
| Editor              | Nano                             |
| Simulated File      | `fakebackup.sh`                  |
| Investigation Tools | `ps`, `grep`, `find`, `pkill`    |
| Attack Simulation   | Suspicious Bash Script Execution |

---

## Commands Used

```bash
mkdir ~/script-lab
cd ~/script-lab

nano fakebackup.sh

chmod +x fakebackup.sh

./fakebackup.sh &

ps aux | grep fakebackup.sh

find /tmp -name "*.sh"

pkill curl

rm -f /tmp/payload.sh
```

---

## Lab Procedure

1. Created a dedicated working directory for the simulation.
2. Created a Bash script named `fakebackup.sh`.
3. Added a simple script that simulated a long-running backup process.
4. Made the script executable using `chmod`.
5. Executed the script in the background.
6. Investigated running processes using Linux process monitoring commands.
7. Searched the system for suspicious shell scripts.
8. Reviewed containment actions such as terminating malicious processes and removing suspicious files.

---

## Observations

* A Bash script was successfully created and executed in the background.
* Running processes can be identified using `ps` and filtered with `grep`.
* File system searches can help locate suspicious shell scripts.
* Basic Linux utilities provide valuable information during the initial stages of an incident investigation.
* Containment actions include terminating suspicious processes and removing malicious files.

---

## SOC Analyst Perspective

Suspicious Bash scripts are commonly used by attackers to execute unauthorized commands, establish persistence, or automate malicious activities. During an investigation, SOC analysts verify the legitimacy of running scripts, determine how they were executed, identify the responsible user, and evaluate whether additional malicious activity has occurred. Quick detection and containment reduce the risk of further system compromise.

---

## Key Learnings

* Understood the Incident Response lifecycle for Linux environments.
* Created and executed a simulated Bash script.
* Investigated running processes using Linux command-line tools.
* Learned techniques for locating suspicious shell scripts.
* Reviewed basic containment procedures for suspicious processes and files.
* Recognized the importance of documenting findings during an incident investigation.

---

## Conclusion

This lab introduced the basic Incident Response workflow for Linux systems by simulating the execution of a suspicious Bash script. Through process investigation and file analysis, the exercise demonstrated how SOC analysts can identify potentially malicious activity, perform initial containment actions, and follow a structured response process to minimize security risks.
