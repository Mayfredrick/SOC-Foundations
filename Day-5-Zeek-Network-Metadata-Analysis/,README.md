# Day 5: Zeek Network Metadata Analysis

## Project Overview

The objective of this lab was to investigate network traffic using Zeek in Security Onion. I reviewed connection records, DNS activity, and protocol metadata in Hunt. I also learned how Zeek helps security analysts understand network communication and investigate potentially suspicious activity.

## Lab Environment

- Platform: Security Onion 2.4.170
- Node: soc
- Analysis Tool: Zeek
- Investigation Interface: Security Onion Hunt

## Activities Completed

- Accessed Zeek connection records in Hunt.
- Reviewed DNS query information and response codes.
- Examined connection IP addresses, destination ports, and protocol information.
- Reviewed network protocol metadata.
- Compared Zeek's network metadata with Suricata's security alerts.
- Confirmed that the records were accessible after troubleshooting the initial search issue.

## Findings

### 1. Connection Analysis

One connection record contained the following information:

| Field | Observed Value |
|---|---|
| Source IP | 192.168.96.1 |
| Destination IP | 224.0.0.32 |
| Destination port | 5355 |
| Protocol classification shown | DNS |

The destination is an IPv4 multicast address, and port 5355 is commonly associated with Link-Local Multicast Name Resolution (LLMNR). This may represent local name-resolution activity. The record alone does not confirm malicious activity.

### 2. DNS Analysis

I reviewed a DNS record with these values:

| Field | Observed Value |
|---|---|
| Queried domain | bc.us.yahoo-ht1.akadns.net |
| Query type | 1 (A record) |
| Response code | 0 (NOERROR) |

The query type indicates an IPv4 address lookup. The response code indicates that the DNS response did not report a DNS error. I did not record a specific returned IP address for this query.

### 3. HTTP/TLS-Related Traffic

I found a network record with the following information:

| Field | Observed Value |
|---|---|
| Destination IP | 188.72.243.72 |
| Protocol metadata | TCP |

The record showed TCP metadata. I did not confirm whether this specific connection had a matching HTTP request or TLS handshake record.

### 4. Overall Traffic Assessment

The traffic I reviewed appeared normal based on the information available. I did not identify activity that I considered unusual during this exercise. This assessment is limited to the records examined and does not establish that all network activity was safe.

## Zeek vs. Suricata

- Zeek: Records network connections and protocol metadata that analysts can use to investigate communication between systems.
- Suricata: Generates network security alerts when traffic matches configured detection rules.

Both tools provide useful information for network monitoring and security investigations.

## Challenges and Resolution

Initially, I could not find the Zeek connection and DNS records in Hunt. I checked the local Zeek log files and confirmed that both conn.log and dns.log contained records. I then continued troubleshooting the search in Hunt and successfully accessed the records.

No further technical issues were encountered during the lab.

## Skills Practiced

- Searching network records in Security Onion Hunt.
- Reading Zeek connection metadata.
- Interpreting DNS query types and response codes.
- Reviewing IP addresses, ports, and protocol information.
- Distinguishing network metadata from IDS alerts.
- Documenting findings without assuming that an unfamiliar connection is malicious.

## Conclusion

This lab provided practical experience using Zeek to investigate network activity in Security Onion. I learned how connection and DNS records help explain communication between systems and how network metadata can support a security investigation. I also practiced troubleshooting missing search results and documenting findings based on the available evidence.
