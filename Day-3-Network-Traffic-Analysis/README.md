# Day-3 Network Traffic Analysis

## Overview

The purpose of this lab was to practice network traffic analysis using Security Onion, Zeek, and Wireshark. I examined network communications, reviewed connection and DNS information, and followed the TCP three-way handshake to understand how devices establish connections.

This lab helped me understand how SOC analysts use network data to investigate activity and identify potential security threats.

## Lab Objectives

- Understand the purpose of network traffic analysis.
- Review Zeek connection and DNS logs.
- Use Wireshark to capture and analyze packets.
- Understand TCP, UDP, DNS, HTTP, and HTTPS.
- Identify the steps in the TCP three-way handshake.
- Distinguish normal traffic from potentially suspicious activity.

## 1. What Is Network Traffic Analysis?

Network traffic analysis is the process of collecting and examining network packets and connection records to understand communications between devices and identify potentially malicious activity or unusual communication patterns.

It is important in a Security Operations Center (SOC) because analysts use network evidence to investigate alerts, understand suspicious behavior, and support incident response.

## 2. Zeek Network Logs

I reviewed network information available through Security Onion, including Zeek connection data.

### Zeek conn.log

Connection logs can provide information such as:

- Source and destination IP addresses
- Source and destination ports
- Network protocol
- Connection duration
- Connection state
- Traffic volume and timestamps

These fields help analysts understand which devices communicated and how the connection behaved.

### Zeek dns.log

DNS logs can provide information such as:

- Timestamp
- Source and destination addresses
- DNS query name
- Query type
- Response information

DNS analysis helps analysts investigate domain lookups and determine whether requested domains require further review.

## 3. Understanding DNS, TCP, and UDP

DNS: The Domain Name System translates domain names, such as google.com, into IP addresses that computers use to communicate.

TCP: Transmission Control Protocol establishes a connection and provides reliable, ordered delivery of data.

UDP: User Datagram Protocol sends datagrams without establishing a TCP-style connection. It is commonly used for DNS queries and other applications that benefit from lower overhead.

### Common Ports Reviewed

| Port | Common use |
|---|---|
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |

Port 53 can use both UDP and TCP. HTTP traffic on port 80 is generally unencrypted, while HTTPS commonly uses TLS to protect communications.

## 4. TCP Three-Way Handshake

One of the most interesting parts of this lab was observing a connection from my device to Google-related services using Wireshark.

The TCP three-way handshake establishes a TCP connection through three steps:

1. SYN: The client requests to establish a connection.
2. SYN-ACK: The server acknowledges the request and responds with its own synchronization information.
3. ACK: The client acknowledges the server's response, completing the handshake.

I observed the handshake packets and examined their sequence and acknowledgment numbers. This helped me understand how TCP connection establishment appears in a packet capture.

I also examined the subsequent traffic. The application-layer request must be interpreted according to the protocol: a readable HTTP GET request may be visible over unencrypted HTTP, but HTTPS request contents are normally encrypted.

## 5. Wireshark vs. Zeek

| Tool | Primary purpose |
| Wireshark | Captures and analyzes individual network packets and protocol details. |
| Zeek | Monitors network traffic and produces structured logs containing connection and protocol metadata. |
| Security Onion | Brings together network visibility, alerts, logs, packet capture, and investigation tools. |

Using these tools together provides different levels of visibility. Wireshark helps examine packet-level evidence, while Zeek makes it easier to search and review network activity through structured logs. Security Onion provides a central place to investigate available data.

## 6. Lab Findings

| Investigation area | Result |
| Network traffic analysis | Traffic was captured and examined successfully. |
| Zeek connection data | Used to review network connection information. |
| DNS activity | Examined domain-related communication. |
| TCP handshake | Observed SYN, SYN-ACK, and ACK packets. |
| Google-related traffic | Followed a connection and examined packet details. |
| Unusual traffic | No unusual traffic identified during this lab. |
| Suspicious domains or IP addresses | None identified in the traffic reviewed. |
| Technical issues | None encountered. |

These findings describe the traffic I examined during this exercise; they do not establish that all traffic in the environment is threat-free.

## 7. Lab Reflection

### What I Learned

I improved my understanding of network traffic analysis and how SOC analysts use network evidence during an investigation. I learned how to review Zeek connection information, examine DNS activity, and use Wireshark to inspect packets in greater detail.

Following the TCP three-way handshake was particularly useful because I could see the SYN, SYN-ACK, and ACK exchange rather than only reading about it.

### Most Interesting Part

The most interesting part was analyzing traffic associated with Google and following the TCP handshake, including the sequence and acknowledgment numbers. This helped me connect networking concepts to real packet-level observations.

### Challenges

I did not encounter any technical problems during this lab. My connections and packet captures worked as expected.

### Skills Practiced

- Network traffic analysis
- Zeek connection-log investigation
- DNS traffic review
- Wireshark packet capture and analysis
- TCP handshake analysis
- Protocol and port identification
- Basic security investigation and evidence review






