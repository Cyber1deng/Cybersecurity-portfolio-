# Cybersecurity Incident Report: DNS Connectivity Failure

### Part 1: Summary of Findings (Traffic Analysis)
**Incident Overview:** investigation following reports of connectivity failures to the domain `yummyrecipesforme.com`. Using `tcpdump` for packet analysis, the security team monitored communication between the client browser and the DNS server.

**Technical Analysis:**
- **Protocol Handshake:** Client initiated communication using **UDP protocol** via **Port 53**.
- **Error Identification:** Recorded an **ICMP Destination Unreachable** error (Type 3, Code 3). Log: `"udp port 53 unreachable."`
- **Packet Metadata:** Inspection identified **Query ID 35084**. The `A?` symbol indicates the IPv4 resolution was never fulfilled. 
- **Conclusion:** The persistent ICMP error responses suggest the DNS server was either offline or blocked.

---

### Part 2: Root Cause Analysis & Mitigation
**Event Context:** Disruption logged at **1:24 p.m.**. External clients received "Destination Port Unreachable" alerts.

**Root Cause Assessment:**
- **Vector A: Denial of Service (DoS):** Malicious traffic may have exhausted server resources, crashing the DNS daemon.
- **Vector B: Security Misconfiguration:** Network Firewall or ACL may have erroneously blocked inbound/outbound UDP traffic on Port 53.

**Remediation:**
1. Perform a status check on DNS server hardware.
2. Inspect firewall logs for dropped traffic on Port 53.
3. Analyze logs for signs of a coordinated **DDoS attack**.
