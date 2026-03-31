# Lab 12: The Life of a Packet — DNS & ARP Analysis

This laboratory focuses on exploring DNS configuration on Cisco routers and analyzing the behavior of the ARP cache in a multi-hop environmentThe exercise simulates a real-world scenario where hostnames are used for connectivity instead of static IP addresses[cite: 30, 34].

## 🌐 Topology Overview
[cite_start]The network consists of a centralized DNS server, two switches, and three routers (R1, R2, R3) interconnected to form two distinct subnets[cite: 5, 26].

### IP Addressing Table
| Device | Interface | IP Address | Role |
| :--- | :--- | :--- | :--- |
| **DNS-Server** | F0 | 10.10.10.10 | [cite_start]DNS Resolver [cite: 4, 30] |
| **R1** | F0/0 | 10.10.10.1 | [cite_start]DNS Client (Subnet A) [cite: 18, 20] |
| **R2** | F0/0 | 10.10.10.2 | [cite_start]Intermediate Gateway (Subnet A) [cite: 7, 8] |
| **R2** | F1/0 | 10.10.20.2 | [cite_start]Intermediate Gateway (Subnet B) [cite: 7, 9] |
| **R3** | F0/0 | 10.10.20.1 | [cite_start]DNS Client (Subnet B) [cite: 21, 23] |

## 🛠️ Configuration Steps

### 1. DNS Client Setup
[cite_start]Each router (R1, R2, and R3) is configured to use the host at `10.10.10.10` as its DNS server[cite: 32]. 
> [cite_start]**Note:** In Cisco Packet Tracer, routers do not support the `ip dns server` command; therefore, a dedicated server device is utilized for name resolution[cite: 29].

### 2. Connectivity Verification
Successful communication is verified by performing ICMP pings using hostnames:
* [cite_start]**From R1:** Verified reachability to `R2` and `R3`[cite: 34].
* [cite_start]**From R3:** Verified reachability to `R1` and `R2`[cite: 35].

##  Technical Analysis: The ARP Cache
A key objective of this lab is understanding the scope of Address Resolution Protocol (ARP).

[cite_start]**Analysis Question:** Do you expect to see an entry for **R3** in the ARP cache of **R1**? [cite: 37]

[cite_start]**Finding:** No[cite: 37]. 
**Reasoning:** ARP is a Layer 2 protocol used to map IP addresses to MAC addresses within a single broadcast domain. [cite_start]Since R1 and R3 reside on different subnets, R1 only needs the MAC address of its default gateway (R2) to forward packets[cite: 37]. [cite_start]The destination MAC address in the frame sent by R1 will be that of R2's F0/0 interface, not R3's[cite: 37].

##  Verification Commands
* `show hosts`: Displays the temporary list of host names and addresses.
* [cite_start]`show arp`: Displays the Address Resolution Protocol (ARP) table[cite: 38].
* [cite_start]`ping [hostname]`: Tests connectivity using DNS resolution[cite: 34].

---
[cite_start]**Tools Used:** Cisco Packet Tracer[cite: 25].
**Focus:** CCNA 200-301 Certification Prep - Network Fundamentals.
