# HTTP Log Analysis Using Splunk

## Objective

The objective of this lab was to ingest HTTP logs into Splunk and analyze web traffic using Search Processing Language (SPL). The lab focused on identifying the most active client IP addresses, detecting HTTP server errors, investigating suspicious User-Agent strings, and identifying large file transfers.

---

## What is HTTP Log Analysis?

HTTP log analysis involves examining web traffic to understand client-server interactions and identify potential security threats. HTTP logs provide visibility into requests, responses, status codes, User-Agent strings, and transferred data, making them valuable for threat hunting, incident response, and web application monitoring.

SOC analysts use HTTP logs to detect scanning activity, malicious automation tools, abnormal file transfers, and web-based attacks.

---

## Lab Environment

| Component     | Details           |
| ------------- | ----------------- |
| SIEM Platform | Splunk Enterprise |
| Data Source   | Zeek HTTP Logs    |
| Log Format    | JSON              |
| Index         | `http_lab`        |
| Sourcetype    | `json`            |

---

## SPL Queries Used

### Task 1 – Top 10 Endpoints Generating Web Traffic

```spl
index=http_lab sourcetype="json"
| stats count by "id.orig_h"
| sort -count
| head 10
```

### Task 2 – Count HTTP Server Errors (5xx)

```spl
index=http_lab sourcetype="json" status_code>=500 status_code<600
| stats count as server_errors
```

### Task 3 – Identify Suspicious User-Agent Strings

```spl
index=http_lab sourcetype="json" user_agent IN ("sqlmap/1.5.1", "curl/7.68.0", "python-requests/2.25.1", "botnet-checker/1.0")
| stats count by user_agent
```

### Task 4 – Identify Large File Transfers

```spl
index=http_lab sourcetype="json" resp_body_len>500000
| table ts "id.orig_h" "id.resp_h" uri resp_body_len
| sort -resp_body_len
```

---

## Lab Procedure

1. Uploaded the Zeek HTTP log file into Splunk.
2. Indexed the data using the `http_lab` index with the `json` sourcetype.
3. Verified successful log ingestion.
4. Executed SPL queries to analyze HTTP activity.
5. Identified the top source IP addresses generating web traffic.
6. Counted HTTP server errors using status code filtering.
7. Investigated suspicious User-Agent strings commonly associated with automated tools.
8. Identified HTTP responses involving large file transfers.

---

## Observations

* HTTP logs were successfully ingested into Splunk.
* Source IP addresses generating the highest volume of web traffic were identified.
* HTTP 5xx status codes highlighted server-side errors.
* Suspicious User-Agent strings were detected using targeted SPL queries.
* Large HTTP responses were identified by filtering response body size.

---

## SOC Analyst Perspective

HTTP log analysis plays a critical role in detecting web-based attacks and abnormal user behavior. Monitoring source IP addresses, HTTP status codes, User-Agent strings, and file transfer sizes helps SOC analysts identify vulnerability scanners, automated attack tools, suspicious downloads, and potential data exfiltration attempts.

---

## Key Learnings

* Learned how to ingest Zeek HTTP logs into Splunk.
* Used SPL queries to analyze web traffic efficiently.
* Identified the most active client IP addresses.
* Detected HTTP server errors using response status codes.
* Investigated suspicious User-Agent strings associated with automated tools.
* Identified large file transfers that may require further investigation.

---

## Conclusion

This lab demonstrated how Splunk can be used to investigate HTTP activity using Zeek HTTP logs. By analyzing client activity, server errors, User-Agent strings, and file transfer sizes, the exercise reinforced practical SIEM techniques used by SOC analysts to monitor and investigate web-based security events.

---

## 📸 Screenshots

### 1. Top 10 Endpoints Generating Web Traffic

The SPL query identified the client IP addresses generating the highest volume of HTTP requests.

![Top 10 Endpoints](../Screenshots/04-SIEM/03.1-top-10-endpoints-generating-web-traffic.png)

---

### 2. HTTP Server Errors (5xx)

The query counted HTTP server errors by filtering response status codes in the 5xx range.

![HTTP Server Errors](../Screenshots/04-SIEM/03.2-http-server-errors.png)

---

### 3. Suspicious User-Agent Analysis

The SPL query identified User-Agent strings commonly associated with automated tools and scripted activity.

![Suspicious User-Agent Analysis](../Screenshots/04-SIEM/03.3-suspicious-user-agent-analysis.png)

---

### 4. Large File Transfer Analysis

The query identified HTTP responses with payload sizes greater than 500 KB to highlight potentially significant file transfers.

![Large File Transfer Analysis](../Screenshots/04-SIEM/03.4-large-file-transfer-analysis.png)
