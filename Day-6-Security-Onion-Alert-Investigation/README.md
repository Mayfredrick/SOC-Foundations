# Day 6: Security Onion Alert Investigation

## Project Overview

The objective of this lab was to investigate a Suricata alert in Security Onion 2.4.170. I reviewed the alert details, searched for related records in Hunt, and compared the findings with an alert from an earlier PCAP replay test. This exercise helped me practice reviewing security alerts and making decisions based on available evidence.

## Lab Environment

- Platform: Security Onion 2.4.170
- Node: soc
- Detection Tool: Suricata
- Investigation Interface: Security Onion Alerts and Hunt

## Alert Details

I investigated the following Suricata alert:

| Field | Observed Value |
|---|---|
| Alert name | GPL_NETBIOS SMB-DSIPC$ Unicode share access |
| Signature ID (SID) | 2102466 |
| Severity / Priority | 3 |
| Source IP | 192.168.10.125 |
| Destination IP | 192.168.10.101 |
| Destination port | 445 |
| Protocol | TCP |

The detection rule identifies SMB-related activity involving an IPC$ share. The signature indicates that the traffic matched a detection rule, but it does not independently prove that unauthorized access occurred.

## Investigation Process

### 1. Reviewed the Alert

I opened the Suricata alert in Security Onion and recorded its signature ID, severity, IP addresses, and destination port.

### 2. Searched Hunt for Related Records

I found the corresponding record in Hunt and compared it with the alert details. The information matched what I had observed during the earlier test.

### 3. Checked the Event Source

The alert appeared consistent with the earlier PCAP replay test using sudo so-test. The source information showed that the traffic was associated with either wire or PCAP data. This supported my understanding that the alert was related to the earlier test, although the exact event source should be verified from the event details when necessary.

The source and destination IP addresses did not match the subnet used by my virtual machines.

### 4. Evaluated the Evidence

The information I reviewed was consistent with the earlier test. I did not find additional evidence that confirmed unauthorized access or established that the event was malicious.

I therefore treated the alert as an event requiring contextual interpretation rather than proof of a confirmed security incident.

## Alert vs. Security Incident

- Alert: A notification generated when activity matches a detection rule or other security condition. It requires review and may turn out to be benign.
- Security incident: An event or series of events assessed to have caused, or to pose a credible risk of causing, harm and requiring an appropriate response.

An alert does not automatically represent a confirmed incident.

## Alert Handling Decision

My initial decision was to close the alert because the evidence did not establish malicious activity. A careful SOC workflow should first verify that the alert belongs to the expected test data and that no additional evidence requires investigation.

Based on the available findings, I did not identify a confirmed malicious incident. If the event source or context were uncertain, I would continue investigating before closing it.

## Technical Challenges

I did not encounter technical issues during this lab.

## Skills Practiced

- Reviewing Suricata alert details.
- Identifying alert signatures and severity values.
- Searching for related records in Security Onion Hunt.
- Comparing current findings with earlier test results.
- Distinguishing a detection alert from a confirmed security incident.
- Using evidence and context to guide alert-handling decisions.

## Conclusion

This lab provided practical experience investigating a Suricata alert in Security Onion. I reviewed the detection details, found the corresponding record in Hunt, and compared the findings with an earlier PCAP replay test. The exercise reinforced the importance of validating alerts and considering their source and context before deciding whether further investigation is necessary.
