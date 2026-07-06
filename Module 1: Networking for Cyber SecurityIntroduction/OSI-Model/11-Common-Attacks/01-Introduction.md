# Introduction to Cyber Attacks

## Overview

Cyber attacks are deliberate attempts by individuals, criminal groups, or nation-state actors to compromise the confidentiality, integrity, or availability of computer systems, networks, applications, or data. Attackers exploit vulnerabilities in software, hardware, network configurations, or human behavior to gain unauthorized access, steal information, disrupt operations, or cause financial and reputational damage.

Understanding cyber attacks is essential for cybersecurity professionals because recognizing attack techniques helps organizations detect threats early, respond effectively, and implement appropriate security controls.

This module introduces the most common cyber attacks encountered in enterprise environments and explains how they work, how they are detected, and how they can be prevented.

---

# Learning Objectives

After completing this module, you should be able to:

* Understand what a cyber attack is.
* Identify different categories of cyber attacks.
* Recognize attacker objectives.
* Understand the Cyber Kill Chain.
* Learn how attackers exploit vulnerabilities.
* Identify Indicators of Compromise (IOCs).
* Understand the role of a SOC Analyst during an attack.
* Apply attack knowledge to incident response and threat hunting.

---

# What is a Cyber Attack?

A **cyber attack** is an intentional action designed to compromise the security of a computer system or network.

The attack may aim to:

* Steal confidential information
* Gain unauthorized access
* Install malware
* Encrypt files for ransom
* Disrupt business operations
* Destroy or modify data
* Spy on users
* Bypass authentication
* Interrupt network services

Example:

```text
Attacker

↓

Internet

↓

Company Firewall

↓

Web Server

↓

Database

↓

Sensitive Data
```

---

# Objectives of Attackers

Attackers have different motivations depending on their goals.

## Financial Gain

Examples:

* Ransomware
* Banking malware
* Credit card theft
* Cryptocurrency theft

---

## Data Theft

Targets include:

* Customer databases
* Passwords
* Intellectual property
* Medical records
* Financial documents

---

## Espionage

Nation-state groups may target:

* Government agencies
* Defense organizations
* Research institutions
* Critical infrastructure

---

## Hacktivism

Hacktivists attack organizations to promote political or social causes.

Examples:

* Website defacement
* Data leaks
* DDoS attacks

---

## Sabotage

The goal is to damage systems or interrupt business operations.

Examples:

* Deleting data
* Destroying backups
* Disabling services

---

# Types of Cyber Attacks

Cyber attacks can be grouped into several categories.

## Malware Attacks

Malicious software designed to damage systems or steal information.

Examples:

* Virus
* Worm
* Trojan
* Spyware
* Rootkit
* Ransomware

---

## Network Attacks

Target network infrastructure and communication.

Examples:

* DDoS
* ARP Spoofing
* DNS Poisoning
* Packet Sniffing
* IP Spoofing

---

## Web Application Attacks

Target websites and web applications.

Examples:

* SQL Injection
* Cross-Site Scripting (XSS)
* CSRF
* Command Injection
* File Inclusion
* SSRF

---

## Authentication Attacks

Target user credentials and authentication mechanisms.

Examples:

* Brute Force
* Password Spraying
* Credential Stuffing
* Session Hijacking

---

## Social Engineering

Manipulates people rather than technology.

Examples:

* Phishing
* Spear Phishing
* Vishing
* Smishing
* Pretexting
* Baiting

---

# Attack Lifecycle (Cyber Kill Chain)

Many attacks follow a sequence of stages.

## 1. Reconnaissance

The attacker gathers information about the target.

Examples:

* Google searches
* LinkedIn research
* WHOIS lookups
* DNS enumeration
* Social media

---

## 2. Weaponization

The attacker prepares tools such as malware, exploits, or phishing emails.

---

## 3. Delivery

The attack is delivered to the victim.

Examples:

* Email attachment
* Malicious website
* USB device
* Drive-by download

---

## 4. Exploitation

The attacker exploits a vulnerability to execute malicious code.

---

## 5. Installation

Malware is installed on the victim's system.

---

## 6. Command and Control (C2)

The infected system communicates with the attacker's server.

---

## 7. Actions on Objectives

The attacker performs the intended activity, such as:

* Data theft
* Ransomware encryption
* Privilege escalation
* Lateral movement

---

# Indicators of Compromise (IOCs)

Indicators of Compromise are pieces of evidence suggesting that a system has been compromised.

Common IOCs include:

* Suspicious IP addresses
* Malicious domain names
* File hashes (MD5, SHA-256)
* Registry changes
* New user accounts
* Unusual network connections
* Unexpected scheduled tasks
* High CPU or memory usage
* Unknown running processes

---

# Indicators of Attack (IOAs)

Unlike IOCs, which indicate a compromise has already occurred, Indicators of Attack focus on attacker behavior.

Examples:

* Repeated failed logins
* PowerShell execution
* Privilege escalation attempts
* Lateral movement
* Network scanning
* Credential dumping

---

# Common Attack Vectors

Attack vectors are the paths attackers use to gain access.

Examples include:

* Email
* Web browsers
* Public-facing servers
* VPN gateways
* Weak passwords
* Misconfigured cloud services
* Remote Desktop Protocol (RDP)
* USB devices
* Third-party software

---

# Role of a SOC Analyst

SOC Analysts play a key role in detecting and responding to cyber attacks.

Typical responsibilities include:

* Monitoring SIEM alerts
* Investigating suspicious activity
* Reviewing firewall and IDS/IPS logs
* Analyzing endpoint telemetry
* Examining email security alerts
* Investigating phishing incidents
* Escalating confirmed incidents
* Documenting findings
* Supporting incident response teams

---

# Common Security Tools

SOC Analysts commonly use:

* Splunk
* Microsoft Sentinel
* Microsoft Defender for Endpoint
* CrowdStrike Falcon
* Wireshark
* Nessus
* Nmap
* VirusTotal
* AbuseIPDB
* Any.Run
* Hybrid Analysis

---

# Real-World Example

A user receives an email claiming to be from the company's HR department.

1. The user clicks the attachment.
2. Malware is installed.
3. The malware connects to a Command-and-Control server.
4. Credentials are stolen.
5. The attacker moves laterally through the network.
6. Sensitive data is exfiltrated.

A SOC Analyst would investigate the email, endpoint alerts, network connections, and authentication logs to contain the incident.

---

# Key Takeaways

* Cyber attacks aim to compromise confidentiality, integrity, or availability.
* Attackers have different motivations, including financial gain, espionage, and sabotage.
* Attacks can target users, applications, networks, and cloud environments.
* Understanding the Cyber Kill Chain helps defenders detect attacks at different stages.
* IOCs and IOAs are essential for threat detection.
* SOC Analysts use multiple tools and log sources to investigate attacks.

---

# Summary

Cyber attacks continue to evolve in sophistication and frequency, making cybersecurity knowledge essential for every security professional. Understanding attacker objectives, common attack vectors, the Cyber Kill Chain, and indicators of compromise enables SOC Analysts to detect threats, investigate incidents, and respond effectively. The following chapters in this module examine each major attack type in detail, including how it works, how to detect it, and how to defend against it.
