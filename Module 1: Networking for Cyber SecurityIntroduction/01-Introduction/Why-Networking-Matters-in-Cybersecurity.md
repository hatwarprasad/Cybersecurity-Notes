# Why Networking Matters in Cybersecurity

## Introduction

Networking is the backbone of cybersecurity. Every cyberattack, whether it is phishing, malware, ransomware, denial-of-service, or data theft, relies on network communication.

A Cyber Security Analyst spends a significant amount of time analyzing network traffic, identifying malicious behavior, and responding to network-based attacks.

---

## Importance of Networking Knowledge

Understanding networking helps security professionals:

- Detect cyberattacks
- Monitor suspicious traffic
- Analyze packet captures
- Investigate compromised systems
- Secure communication channels
- Configure firewalls
- Monitor IDS/IPS alerts
- Hunt for threats

---

## Real SOC Scenario

A SIEM generates an alert:

"Multiple failed login attempts detected."

To investigate, an analyst needs to know:

- Source IP
- Destination IP
- Protocol
- Port Number
- Username
- Network Location

Without networking knowledge, the alert cannot be investigated effectively.

---

## Networking in Different Security Domains

### Incident Response

- Identify attacker IP
- Block malicious traffic
- Trace attack path

---

### Threat Hunting

- Search unusual network connections
- Detect lateral movement
- Find beaconing traffic

---

### Digital Forensics

Analyze:

- Packet captures
- DNS logs
- Firewall logs
- Proxy logs

---

### Vulnerability Assessment

Network scanning uses:

- Nmap
- Nessus
- OpenVAS

Networking knowledge helps interpret scan results.

---

## Common Network-Based Attacks

### Phishing

Victim clicks malicious link.

↓

Browser connects to attacker server.

↓

Malware downloads.

---

### Brute Force Attack

Attacker repeatedly attempts login.

Indicators:

- Multiple failed logins
- Same source IP
- Same destination

---

### Malware Communication

Compromised computer communicates with Command and Control (C2) server.

SOC analysts identify:

- Destination IP
- Domain
- Protocol
- Port

---

### Data Exfiltration

Sensitive information leaves the organization.

Indicators:

- Large outbound traffic
- Unknown destinations
- Unusual upload activity

---

## SOC Analyst Daily Tasks

Typical tasks include:

- Monitor SIEM alerts
- Investigate suspicious IPs
- Analyze firewall logs
- Review VPN logs
- Investigate phishing emails
- Examine DNS requests
- Monitor endpoint activity

---

## Key Networking Concepts Used Daily

- IP Address
- MAC Address
- DNS
- DHCP
- HTTP
- HTTPS
- TCP
- UDP
- Ports
- VPN
- Firewall
- Proxy
- NAT

---

## Interview Questions

### Why is networking important for SOC analysts?

Because almost all cyberattacks involve network communication. Analysts use networking concepts to investigate alerts and detect malicious activity.

---

### Name three network logs commonly analyzed in SOC.

- Firewall Logs
- DNS Logs
- Proxy Logs

---

## Practical Exercise

Open Command Prompt or Terminal and run:

```
ipconfig
```

or on Linux:

```
ifconfig
```

or

```
ip addr
```

Identify:

- IP Address
- Gateway
- DNS Server

Record your findings.
