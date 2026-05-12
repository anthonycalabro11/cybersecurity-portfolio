# Cybersecurity Incident Report
**Organization:** Travel Agency — Internal Web Server  
**Analyst:** Security Operations Team  
**Date of Incident:** [Date of Alert]  
**Report Classification:** Internal Use Only

---

## Section 1: Identifying the Type of Network Attack

### Summary of Findings

Based on analysis of the automated monitoring alert, direct observation of browser behavior (connection timeout), and review of captured packet data via Wireshark, the network interruption was caused by a **SYN Flood Attack** — a specific type of **Denial of Service (DoS) attack**.

### Evidence from Wireshark Log

The packet capture revealed the following key indicators:

- A **disproportionately large number of TCP SYN requests** were arriving from a single, unfamiliar IP address.
- The web server was sending back **SYN-ACK responses** to each request, allocating connection resources.
- **No corresponding ACK packets** were returned by the initiating IP to complete the three-way TCP handshake.
- As a result, the server's **connection table filled up** with half-open connections, exhausting available resources and preventing legitimate users from establishing sessions.

### DoS vs. DDoS — Key Distinction

| Feature | DoS | DDoS |
|---|---|---|
| **Source** | Single IP / machine | Multiple IPs / machines (botnet) |
| **Volume** | Moderate | Extremely high |
| **Mitigation** | Block single IP | Requires advanced filtering, rate limiting, CDN |
| **This Incident** | ✅ Matches (single unfamiliar IP) | ❌ Not indicated by current evidence |

In this incident, traffic originated from **one IP address**, classifying it as a **DoS SYN Flood attack**. However, it is noted that IP spoofing could make a DDoS attack appear to originate from a single source, so escalation monitoring is warranted.

---

## Section 2: Explaining How the Attack Affected the Website

### How a SYN Flood Attack Works

A SYN Flood attack exploits the **TCP three-way handshake**, which is the standard process used to establish a connection between a client and server:

```
Normal Handshake:
  Client  →  SYN       →  Server
  Client  ←  SYN-ACK   ←  Server
  Client  →  ACK       →  Server
  [ Connection Established ]

SYN Flood Attack:
  Attacker  →  SYN       →  Server
  Attacker  ←  SYN-ACK   ←  Server
  Attacker  ✗  (No ACK sent — connection left half-open)
  [ Repeated thousands of times → Server resources exhausted ]
```

The attacker intentionally never completes the handshake. Each unanswered SYN-ACK causes the server to hold a **half-open connection** in memory while it waits for the final ACK. These half-open connections consume server memory and connection slots until the server can no longer accept any new connections — including from legitimate users.

### Impact on the Organization's Network

| Area Affected | Impact |
|---|---|
| **Web Server Availability** | Server became overwhelmed and could not respond to legitimate requests |
| **Employee Productivity** | Staff could not access the sales webpage to search for vacation packages for customers |
| **Customer Experience** | Customers attempting to browse promotions received connection timeout errors |
| **Server Resources** | CPU, memory, and connection table capacity were consumed by half-open connections |
| **Business Operations** | Sales and promotional activities were interrupted during the attack window |

### Timeline of Events

1. **Attack Initiated** — Attacker begins sending high-volume TCP SYN packets from unfamiliar IP.
2. **Server Degradation** — Server's connection table fills with half-open connections; response time increases.
3. **Alert Triggered** — Automated monitoring system detects anomaly and notifies security analyst.
4. **Analyst Investigation** — Connection timeout confirmed; Wireshark packet capture deployed and analyzed.
5. **Containment** — Web server taken offline; firewall rule created to block attacker IP.
6. **Recovery** — Server brought back online after resources normalized.

### Potential Consequences

- **Revenue Loss:** Inability to access sales promotions directly disrupts booking activity.
- **Reputational Damage:** Customers encountering timeouts may lose trust in the platform's reliability.
- **Operational Disruption:** Employees are blocked from performing core job functions.
- **Escalation Risk:** If the attacker pivots to IP spoofing or a botnet, the DoS could escalate to a DDoS, making basic IP blocking ineffective.

---

## Section 3: Recommendations for Prevention

The following controls are recommended to reduce the risk of future SYN Flood attacks:

### Immediate Actions
- **Rate Limiting:** Configure the firewall or load balancer to limit the number of SYN packets accepted per second from any single IP.
- **SYN Cookies:** Enable SYN cookie technology on the web server so that it does not allocate resources until the full handshake is verified.
- **IP Reputation Blocking:** Subscribe to threat intelligence feeds to proactively block known malicious IPs.

### Short-Term Actions
- **Intrusion Detection System (IDS):** Deploy or tune an IDS with rules to detect SYN flood patterns and alert in real time.
- **Firewall Half-Open Connection Limits:** Configure the firewall to limit the number of half-open TCP connections allowed at one time.
- **Traffic Baseline:** Establish a baseline of normal traffic volume so anomalies can be detected faster in the future.

### Long-Term Actions
- **DDoS Protection Service:** Evaluate a cloud-based DDoS mitigation provider (e.g., Cloudflare, AWS Shield) to handle large-scale volumetric attacks that exceed on-premises capability.
- **Incident Response Plan:** Formalize and document a runbook for responding to DoS/DDoS incidents so future responses are faster and more coordinated.
- **Regular Security Audits:** Conduct periodic reviews of firewall rules, server configurations, and network architecture.

---

## Conclusion

The network interruption experienced on the company's web server was caused by a **TCP SYN Flood Denial of Service (DoS) attack**. The attacker sent an abnormally high volume of TCP SYN requests without completing the three-way handshake, exhausting server resources and making the website unavailable to both employees and customers. Immediate containment steps (taking the server offline and blocking the attacker's IP) were executed successfully. However, due to the attacker's potential ability to spoof IP addresses, longer-term technical controls such as SYN cookies, rate limiting, and a DDoS mitigation service are strongly recommended to prevent recurrence.

---

*Report prepared as part of the Google Cybersecurity Certificate — Network Security Module.*
