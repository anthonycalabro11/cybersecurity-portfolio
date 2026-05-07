# Cybersecurity Incident Report
## DNS & ICMP Traffic Analysis

**Analyst:** Anthony Calabro  
**Date:** 5/7/2026  
**Incident:** www.yummyrecipesforme.com — Destination Port Unreachable  
**Tools Used:** tcpdump (network protocol analyzer)

---

## Part 1: Summary of the Problem Found in the tcpdump Log

### Protocols Involved
- **UDP (User Datagram Protocol)** — used by the browser to send DNS queries to the DNS server
- **DNS (Domain Name System)** — the service being requested on port 53
- **ICMP (Internet Control Message Protocol)** — used to return error messages back to the source

### tcpdump Log Analysis

Upon attempting to access `www.yummyrecipesforme.com`, the network analyzer captured the following sequence of events:

1. **Outgoing UDP request (13:24:32.192571):** The browser sent a UDP packet from source IP `192.51.100.15` to the DNS server at `203.0.113.2` on **port 53**, requesting the IP address (A record) for `yummyrecipesforme.com`. The query ID was `35084+`, with the `A?` flag indicating a DNS A record lookup.

2. **ICMP error response:** The DNS server at `203.0.113.2` responded with an ICMP error packet directed back to `192.51.100.15`. The error message stated: **"udp port 53 unreachable"** — indicating that the UDP packet could not be delivered because no service was actively listening on port 53 of the DNS server.

3. **Repeated failures:** The same exchange occurred two additional times, with identical ICMP error responses each time, confirming that the issue was consistent and not a transient network glitch.

### Interpretation

The log reveals that the **DNS service on the server (`203.0.113.2`) was not responding on port 53**. Because the browser could not resolve the domain name to an IP address, it was unable to establish an HTTPS connection to the web server — resulting in the "destination port unreachable" error experienced by users.

---

## Part 2: Analysis and Proposed Solution

### When the Problem Was First Reported

The incident was first reported by multiple customers of clients who were unable to access `www.yummyrecipesforme.com`. The error message observed by users was **"destination port unreachable."** Based on the tcpdump timestamps, the earliest captured evidence of the failure occurred at **13:24:32** on the date of analysis.

### Scenario and Events

| Item | Detail |
|------|--------|
| **Affected website** | www.yummyrecipesforme.com |
| **User-reported error** | "Destination port unreachable" |
| **Protocol affected** | DNS over UDP (port 53) |
| **Error mechanism** | ICMP "udp port 53 unreachable" returned to client |
| **Impacted layer** | Internet layer / Application layer (TCP/IP model) |

### Current Status

The issue is ongoing at the time of this report. The DNS server at `203.0.113.2` is not responding to DNS queries on port 53. The incident has been escalated to the security engineering team for resolution.

### Information Discovered During Investigation

- UDP packets sent to DNS server port 53 are being returned with ICMP error messages
- The error "udp port 53 unreachable" indicates port 53 is **closed or the DNS service is down** on the server
- The failure occurred consistently across three separate query attempts, ruling out a one-time packet loss
- Without DNS resolution, no HTTPS connection can be initiated — explaining the end-user error

### Next Steps in Troubleshooting and Resolving the Issue

1. **Verify DNS service status** — Check whether the DNS service (e.g., BIND, dnsmasq) is running on `203.0.113.2`
2. **Check firewall rules** — Confirm that port 53 (UDP/TCP) is not being blocked by a firewall on the DNS server or upstream network device
3. **Review server logs** — Inspect the DNS server's system logs for crashes, misconfigurations, or signs of a denial-of-service attack
4. **Test alternate DNS servers** — Attempt DNS resolution using a backup DNS server to restore service while the primary is investigated
5. **Check for DoS/DDoS activity** — Determine whether the DNS server was deliberately taken offline or overwhelmed by malicious traffic (DNS amplification attack)
6. **Restart DNS service if appropriate** — If the service simply stopped, restart it and monitor for recurrence

### Suspected Root Cause

The most likely root cause is that the **DNS service on the server (`203.0.113.2`) stopped running or became unavailable**, causing port 53 to be unreachable. This could be due to:

- A **service crash or misconfiguration** on the DNS server
- A **firewall rule change** that inadvertently blocked UDP port 53
- A **denial-of-service (DoS) attack** targeting the DNS server, causing it to become unresponsive

Until the DNS service is restored and able to respond to A record queries for `yummyrecipesforme.com`, users will continue to receive the "destination port unreachable" error and will be unable to access the website.

---

## Summary Table

| Field | Details |
|-------|---------|
| **Incident type** | DNS service unavailability |
| **Affected protocol** | DNS / UDP port 53 |
| **Error returned** | ICMP — "udp port 53 unreachable" |
| **Root cause (suspected)** | DNS service down or port 53 blocked on DNS server |
| **Impact** | Users unable to resolve domain; website inaccessible |
| **Status** | Escalated to security engineering team |

---

*This report was produced as part of a network traffic analysis exercise using tcpdump to capture and interpret DNS and ICMP packets in the context of a cybersecurity incident.*
