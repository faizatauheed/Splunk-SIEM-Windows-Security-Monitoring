**Splunk SIEM — Windows Security Monitoring & Brute-Force Detection
Overview
**
This project demonstrates a hands-on Security Information and Event Management (SIEM) lab using Splunk Enterprise and Windows Security Event Logs.

The project focuses on collecting, searching, and investigating Windows authentication activity and developing a detection for repeated failed login attempts that may indicate a brute-force attack.

The lab was developed as part of a cybersecurity/cloud security academic project and demonstrates practical SOC-style log analysis and detection engineering.

Objectives
Analyze Windows Security Event Logs using Splunk.
Investigate successful and failed authentication events.
Understand Windows Event IDs 4624 and 4625.
Develop SPL-based security detection logic.
Identify repeated failed authentication attempts.
Demonstrate a basic SOC investigation workflow.
Document findings and security monitoring methodology.
Technologies & Tools
Splunk Enterprise
Windows Event Logs
SPL (Search Processing Language)
Windows
SIEM and SOC concepts
SIEM Workflow

Windows Security Logs → Log Collection → Splunk Enterprise → Event Search & Analysis → Detection Logic → Security Investigation

Windows Authentication Events
Event ID 4624 — Successful Logon

Windows Event ID 4624 represents a successful authentication event.

These events were investigated to understand normal authentication activity and establish context for suspicious login behavior.

Event ID 4625 — Failed Logon

Windows Event ID 4625 represents a failed authentication attempt.

Repeated 4625 events can indicate suspicious activity such as password guessing or brute-force attempts.

Brute-Force Detection

A threshold-based SPL query was developed to identify repeated failed authentication attempts within a five-minute window.

index=test075 EventCode=4625
| bin _time span=5m
| stats count by _time Account_Name
| where count > 5
Detection Logic

The query:

Searches for Windows failed logon events using EventCode 4625.
Groups events into five-minute time windows.
Counts failed attempts by account.
Flags activity when more than five failed attempts occur within the same window.

This can help identify potential password-guessing or brute-force activity.

Investigation Workflow
Search Windows events.
Identify authentication events.
Analyze Event ID 4624.
Analyze Event ID 4625.
Aggregate failed authentication attempts.
Apply the detection threshold.
Investigate suspicious activity.

The analysis focused on fields such as account name, event ID, timestamp, host, and authentication activity.

Key Learning Outcomes

Through this project, I gained practical experience in:

SIEM-based security monitoring
Windows authentication log analysis
Splunk event investigation
SPL query development
Detection logic development
Authentication activity analysis
Basic SOC investigation workflows
Security documentation and evidence analysis
Limitations

This project focuses primarily on Windows authentication event analysis and threshold-based detection.

The brute-force detection can produce false positives in environments where users frequently enter incorrect credentials. In a production SOC environment, additional context such as source IP, host, user behavior, account privilege level, and historical activity would improve detection accuracy.

Future Improvements
Additional authentication detection rules
Source IP-based correlation
Privileged account monitoring
Suspicious login behavior detection
Splunk dashboards
Automated alerting
MITRE ATT&CK technique mapping
Integration with additional endpoint/security telemetry

These are future improvements and are not claimed as implemented in the current lab.

Documentation

The complete project report contains the project background, SIEM architecture, implementation methodology, investigation process, screenshots, results, limitations, and future work.

Author

Faiza Tauheed
Cybersecurity Undergraduate | Aspiring SOC Analyst
