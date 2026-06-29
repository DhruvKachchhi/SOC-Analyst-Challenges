# Introduction to Phishing Analysis

## Objective

The objective of this lab was to understand the fundamentals of phishing analysis by learning how to identify suspicious emails, examine common phishing techniques, recognize malicious indicators, and understand the process of investigating phishing attempts.

---

## What is Phishing Analysis?

Phishing analysis is the process of examining suspicious emails to determine whether they are designed to deceive recipients into revealing sensitive information, downloading malware, or performing unauthorized actions. Analysts review email headers, sender information, embedded URLs, attachments, and message content to identify malicious characteristics and extract Indicators of Compromise (IOCs).

---

## Lab Environment

| Component           | Details                                             |
| ------------------- | --------------------------------------------------- |
| Operating System    | Windows                                             |
| Investigation Focus | Email Phishing                                      |
| Sample Scenario     | Lookalike Domain Email                              |
| Analysis Techniques | Header Analysis, URL Inspection, IOC Identification |
| Supporting Tools    | VirusTotal, CyberChef, Whois, Email Header Analyzer |

---

## Analysis Process

1. Collected the suspicious email sample for analysis.
2. Reviewed sender information and compared the displayed sender with the actual email address.
3. Examined the email body for urgency, branding, and social engineering techniques.
4. Inspected embedded links and verified destination URLs.
5. Reviewed potential attachments for suspicious characteristics.
6. Identified possible Indicators of Compromise (IOCs).
7. Documented findings and recommended appropriate response actions.

---

## Indicators Observed

### Suspicious Sender Address

```text id="4zj6ci"
noreply@secure-paypai.com
```

**Observation:**

The sender uses a **lookalike domain** (`paypai.com`) that impersonates the legitimate **paypal.com** domain by replacing the letter **l** with **i**, a common phishing technique known as **typosquatting**.

---

## Observations

* The sender address closely resembles a legitimate PayPal email but uses a deceptive domain.
* The scenario demonstrates a lookalike domain attack designed to trick recipients into trusting the email.
* Such attacks often encourage users to click malicious links or provide sensitive information.
* Careful verification of sender domains is essential before interacting with unexpected emails.

---

## SOC Analyst Perspective

Phishing remains one of the most common initial access techniques used by attackers. During an investigation, SOC analysts verify sender legitimacy, inspect email headers, analyze embedded URLs and attachments, identify Indicators of Compromise (IOCs), and determine whether similar emails have been delivered to other users. Prompt reporting and blocking of malicious domains help reduce organizational risk.

---

## Key Learnings

* Understood the purpose of phishing analysis.
* Learned the characteristics of common phishing attacks.
* Identified how lookalike domains are used to impersonate trusted organizations.
* Reviewed the standard workflow for investigating suspicious emails.
* Recognized the importance of extracting Indicators of Compromise (IOCs) during email investigations.
* Understood the role of phishing analysis in incident response and threat intelligence.

---

## Conclusion

This lab introduced the fundamentals of phishing analysis by examining a suspicious email using a lookalike domain. The exercise demonstrated how attackers exploit visually similar domain names to impersonate trusted organizations and highlighted the importance of verifying sender identities, identifying phishing indicators, and following a structured investigation process to protect users from email-based attacks.

