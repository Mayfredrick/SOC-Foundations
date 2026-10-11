#  Day 7: SOC Investigation 

## Project Overview

The objective of this lab was to investigate a Suricata alert using Security Onion 2.4.170. I reviewed the alert details, searched for related records in Hunt, and accessed packet capture (PCAP) data to examine the network communication. This exercise brought together the network monitoring and investigation skills practiced throughout Week 8.

## Lab Environment

- Platform: Security Onion 2.4.170
- Node: soc
- Detection Tool: Suricata
- Investigation Interface: Security Onion Alerts and Hunt
- Packet Analysis: Security Onion PCAP

## 1. Alert Selected

I investigated a Suricata alert with the following signature ID:

| Field | Observed Value |
|---|---|
| Alert signature ID (SID) | 2102466 |
| Alert name | GPL_NETBIOS SMB-DSIPC$ Unicode share access |
| Priority | 3 |
| Source IP | 192.168.10.125 |
| Destination IP | 192.168.1.101 |
| Destination port | 445 |

The detection rule identifies SMB-related activity involving an IPC$ share. A signature match indicates that the traffic matched a detection rule; it does not, by itself, prove that unauthorized access occurred.

## 2. Investigation in Hunt

I searched for the alert in Hunt and reviewed additional information about the IP addresses, alert severity, and rule that detected the traffic.

The information was consistent with the alert I had investigated during the earlier PCAP replay test. This supported the interpretation that I was reviewing the same test activity.

## 3. Zeek and Network Metadata

I compared the source and destination information with related network records. I also reviewed TCP connection information, including the handshake and connection completion details.

The records helped me understand how network metadata can provide context for a Suricata alert. I did not establish that all the records were related solely from their protocol information; the IP addresses and timestamps are important when correlating events.

## 4. PCAP Investigation

I was able to access the PCAP associated with the event. The packet information displayed the TCP three-way handshake from beginning to completion.

The handshake helped me understand how a TCP connection is established and how packet-level evidence can be used to examine network communication in more detail.

## 5. TCP PSH Flag Observation

While reviewing the PCAP, I noticed a TCP PSH flag in addition to the more familiar SYN, ACK, and FIN flags.

I researched the flag and learned that PSH stands for Push. It is a TCP control flag associated with requesting prompt delivery of received data to the application rather than waiting for additional data to arrive.

The presence of PSH is normal in TCP communication and does not independently indicate malicious activity.

## 6. Assessment and Decision

The evidence I reviewed did not confirm malicious activity. The alert appeared consistent with the earlier test PCAP replay, and the PCAP allowed me to inspect the TCP handshake.

Based on the evidence available, I chose to close the alert. In a real SOC environment, I would first verify the event source and confirm that no additional evidence or related activity requires investigation before closing an alert.

## 7. Roles of the Investigation Tools

- Suricata: Identified network activity that matched a detection rule.
- Zeek: Provided network connection and protocol metadata.
- Hunt: Allowed me to search for related records and review event details.
- PCAP: Allowed me to inspect individual packets and observe the TCP handshake.

Using these tools together helped me narrow down the activity and evaluate the alert using more than the detection signature alone.

## 8. Technical Challenges and Lessons Learned

I did not encounter technical issues during this capstone.

The most interesting finding was the TCP PSH flag in the PCAP. Researching it helped me understand another TCP control flag and recognize that packet details must be interpreted in context rather than automatically treated as suspicious.

## Skills Practiced

- Investigating Suricata alerts.
- Searching and correlating records in Security Onion Hunt.
- Reviewing Zeek network metadata.
- Accessing and examining PCAP data.
- Understanding TCP handshake behavior and flags.
- Assessing an alert using supporting evidence.
- Documenting findings and investigation decisions.

## Conclusion

I handled this lab as single network security investigation.Here I reviewed a Suricata alert, searched for related network records, inspected packet capture data, and evaluated whether the evidence supported a malicious interpretation.

The exercise reinforced the importance of correlating multiple sources of evidence and understanding network protocols before making an alert-handling decision.
