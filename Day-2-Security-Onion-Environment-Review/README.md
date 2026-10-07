# Day 2 – Security Onion Environment Review

## Overview

This lab focused on reviewing the existing Security Onion environment before beginning detailed security monitoring and alert investigation.

The goal was to verify the Security Onion version, network configuration, system status, Security Onion Console, Grid connection, Elasticsearch health, Suricata, Zeek, and network traffic.

The Security Onion installation used for this lab is an Evaluation deployment, which is appropriate for a home lab environment. Security Onion documentation describes Evaluation mode as suitable for classroom and small lab environments.

## Lab Environment

| Component              | Result                 |
| ---------------------- | ---------------------- |
| Security Onion Version | 2.4.170                |
| Hostname               | soc                  |
| Node Role              | Evaluation             |
| Management Interface   | ens160               |
| Management IP          | 192.168.114.123      |
| Default Gateway        | 192.168.114.2        |
| VM Network Interfaces  | Host-only and NAT      |
| Interface Status       | UP                     |
| Security Onion Console | Accessible             |
| Grid Connection        | Connected              |
| Elasticsearch          | OK                     |
| Suricata Alerts        | None visible           |
| Zeek Metadata          | Visible                |
| Network Traffic        | Visible with tcpdump |

# 1. Security Onion Version
The installed Security Onion version was verified as: 2.4.170
This confirms that the lab is currently running Security Onion 2.4.

# 2. Hostname
The hostname of the Security Onion system is: soc
Using a clear hostname makes it easier to identify the Security Onion system when working with multiple virtual machines.

# 3. Network Configuration
The Security Onion management interface is: ens160
Management IP address: 192.168.114.123
Default gateway: 192.168.114.2

The Security Onion VM has two network interfaces configured through VMware:
* Host-only
* NAT

Both interfaces were reported as UP.
The network configuration is important because Security Onion must be able to communicate with the management network and receive the network traffic that it is expected to monitor.

# 4. Security Onion Service Status
The following command was used: sudo so-status
No errors were displayed.
This indicates that the enabled Security Onion services appeared to be running correctly at the time of the assessment.
Security Onion documents so-status as a method for checking the status of enabled services. A successful status indicates that the system appears to be running correctly.

# 5. Security Onion Console
The Security Onion Console (SOC) was accessible successfully.
The SOC provides access to several security monitoring and management functions, including:
* Alerts
* Dashboards
* Hunt
* Cases
* Detections
* PCAP
* Grid
* Administration

These interfaces will be used in later SOC labs for network monitoring, alert investigation, and threat hunting.

# 6. Security Onion Grid
The Security Onion node was visible in the Grid and was connected successfully.
The node role was: Evaluation
The Grid showed that the node was connected and operational.
Security Onion's Grid provides information about node status, role, management address, version, connection status, Elasticsearch status, memory usage, and other system information.

# 7. Elasticsearch Status
Elasticsearch showed: OK
This indicates that Elasticsearch was healthy during the environment review.
Elasticsearch is important because Security Onion uses it to store and make security data available for searching and analysis.
Security Onion's documentation notes that Elasticsearch status is displayed in the Grid for nodes running Elasticsearch.

# 8. Suricata Review
No Suricata alerts were visible during the review.
This does not automatically indicate a problem.
Suricata is responsible for network intrusion detection and can generate alerts when monitored traffic matches detection rules.
At the time of this lab, no traffic had produced a visible Suricata alert.
Security Onion documentation explains that Suricata provides NIDS alerts and recommends checking network metadata when expected alerts are not appearing.

# 9. Zeek Review
Zeek network metadata was visible in the Security Onion environment.
This confirmed that Security Onion was receiving and processing network information that could be analyzed.
Zeek provides network protocol metadata that can help analysts understand network activity.
Examples of information that can be generated include:
* Network connections
* DNS
* HTTP
* SSL/TLS
* SSH
* Other network protocols

Security Onion documentation identifies Zeek as one of its network metadata engines.

# 10. Network Traffic Verification
The following command was used to verify that network traffic was reaching the Security Onion system: sudo tcpdump -i any -c 20
Network traffic was displayed.
This was an important result because it confirmed that packets were reaching the Security Onion system.
The relationship can be represented as:

Network Traffic
       |
       v
Security Onion Interface
       |
       v
Network Monitoring
       |
       +----------------+
       |                |
       v                v
    Suricata           Zeek
       |                |
       v                v
    Alerts           Metadata
       |                |
       +-------+--------+
               |
               v
          SOC Analyst

# 11. Suricata vs Zeek

### Suricata
Suricata is primarily being used in this lab as a network intrusion detection engine.
Its main purpose is to identify suspicious or malicious network activity and generate security alerts based on detection rules.

### Zeek
Zeek is a network security monitoring and analysis framework.
It provides detailed network metadata that helps analysts understand what is happening across the network.

### Comparison

| Suricata                           | Zeek                                   |
| ---------------------------------- | -------------------------------------- |
| Focuses on threat detection        | Focuses on network analysis            |
| Generates NIDS alerts              | Generates network metadata             |
| Uses detection rules               | Provides detailed protocol information |
| Helps identify suspicious activity | Helps understand network behavior      |

Both tools provide valuable information to a SOC analyst.

# 12. Why Network Traffic Is Important
Security monitoring systems need access to the traffic they are expected to analyze.
If traffic does not reach the monitoring interface, Security Onion cannot inspect that traffic and generate useful metadata or alerts from it.
The lab confirmed that network traffic was reaching the Security Onion system because tcpdump displayed packets and Zeek metadata was visible.

# 13. Possible Reasons for Missing Suricata Alerts
Although no Suricata alerts were visible, several possibilities could explain this.
Possible causes include:
* Not enough traffic reaching the monitoring interface
* Traffic that does not match an enabled detection rule
* Detection rules not being triggered by the observed activity
* Security Onion configuration issues
* Traffic being received on an interface that is not being monitored by the expected detection process

Security Onion documentation recommends checking network metadata and the Connections dashboard when expected Suricata alerts are not appearing.

Because Zeek metadata and packet traffic were visible in this lab, there was evidence that Security Onion was receiving network data.

# 14. SOC Analyst Investigation Approach
If Suricata is not generating alerts, I would not immediately assume that Security Onion is broken.
I would investigate in stages:
Check Network Interface
        |
        v
Verify Traffic with tcpdump
        |
        v
Check Zeek/Suricata Metadata
        |
        v
Check Detection Rules
        |
        v
Check Suricata Status
        |
        v
Investigate Configuration


This approach helps identify where the problem exists instead of making unnecessary configuration changes.

# Lab Reflection

## What did I learn?

I learned how to review the basic health and configuration of a Security Onion environment before beginning security investigations.

I learned how to identify the Security Onion version, hostname, network interface, IP address, default gateway, node role, Grid status, and Elasticsearch status.

I also learned that tcpdump can be used to verify whether network traffic is reaching the system.

Another important lesson was understanding the relationship between Suricata and Zeek. Suricata focuses on network threat detection and alerts, while Zeek provides detailed network metadata that can help with analysis and investigation.

## Most Important Finding

The most important finding from this lab was that **network traffic was reaching Security Onion and Zeek metadata was available, but no Suricata alerts were currently visible**.

This does not automatically indicate a problem because alerts depend on the traffic matching enabled detection rules.

## Challenges

No technical problems were encountered during this lab.

The Security Onion Console was accessible, the node was connected to the Grid, Elasticsearch showed an OK status, and network traffic was visible.

## Skills Practiced

* Security Onion administration
* Security Onion Console
* Grid monitoring
* Network interface identification
* IP configuration review
* Service health checking
* Elasticsearch health verification
* Suricata review
* Zeek metadata review
* tcpdump
* Network traffic verification
* SOC troubleshooting methodology

## Lab Status
No technical issues encountered.


