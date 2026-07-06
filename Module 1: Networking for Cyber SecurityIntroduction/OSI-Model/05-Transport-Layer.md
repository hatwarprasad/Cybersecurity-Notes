# Transport Layer (Layer 4)

## Introduction

The **Transport Layer** is the **fourth layer** of the **OSI (Open Systems Interconnection) Model**. It is responsible for **end-to-end communication** between applications running on different devices.

While the Network Layer determines **where** data should be sent, the Transport Layer determines **how** the data is delivered reliably and efficiently.

It provides services such as:

* End-to-end communication
* Segmentation and reassembly
* Flow control
* Error detection and recovery
* Multiplexing
* Port addressing
* Connection management

The two most important protocols operating at this layer are:

* **TCP (Transmission Control Protocol)**
* **UDP (User Datagram Protocol)**

Every web request, email, file transfer, video call, or online game relies on one of these protocols.

For Cyber Security Analysts, understanding the Transport Layer is critical because attacks such as **SYN Floods, Port Scanning, TCP Reset Attacks, and UDP Floods** occur at this layer.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Explain the purpose of the Transport Layer.
* Understand segmentation and reassembly.
* Differentiate between TCP and UDP.
* Explain multiplexing and demultiplexing.
* Understand ports and sockets.
* Identify common Transport Layer attacks.
* Apply Layer 4 concepts during SOC investigations.

---

# Position in the OSI Model

```text
+-----------------------------+
| Layer 7 - Application       |
+-----------------------------+
| Layer 6 - Presentation      |
+-----------------------------+
| Layer 5 - Session           |
+-----------------------------+
| Layer 4 - Transport  ← You are here
+-----------------------------+
| Layer 3 - Network           |
+-----------------------------+
| Layer 2 - Data Link         |
+-----------------------------+
| Layer 1 - Physical          |
+-----------------------------+
```

---

# Responsibilities of the Transport Layer

The Transport Layer ensures that data reaches the correct application on the destination device.

Its major responsibilities include:

## 1. End-to-End Communication

Provides communication between applications on two different systems.

Example:

```text
Chrome Browser

↓

TCP

↓

Internet

↓

Web Server
```

---

## 2. Segmentation

Large amounts of data are divided into smaller units called **segments**.

Example:

Large File

```text
500 MB
```

↓

Segment 1

↓

Segment 2

↓

Segment 3

↓

Segment N

Each segment is transmitted separately.

---

## 3. Reassembly

The receiving Transport Layer collects all incoming segments and reconstructs the original data in the correct order.

---

## 4. Flow Control

Prevents a fast sender from overwhelming a slow receiver.

---

## 5. Error Recovery

Detects missing or corrupted segments and requests retransmission when necessary (TCP).

---

## 6. Multiplexing

Allows multiple applications to use the network simultaneously through different port numbers.

---

## 7. Port Addressing

Uses **port numbers** to identify which application should receive incoming data.

Example:

```text
Browser

↓

Port 443

↓

HTTPS
```

---

# Data Unit

The Transport Layer data unit is:

| Protocol | Data Unit |
| -------- | --------- |
| TCP      | Segment   |
| UDP      | Datagram  |

Example:

```text
+--------------------------------------+
| TCP Header | Application Data |
+--------------------------------------+
```

---

# Segmentation

## What is Segmentation?

Segmentation is the process of dividing large blocks of application data into smaller, manageable pieces called **segments**.

Without segmentation, transmitting large files would be inefficient and more prone to errors.

---

## Example

Suppose you upload a 50 MB file.

Instead of sending one large block:

```text
50 MB
```

The Transport Layer divides it into many smaller segments:

```text
Segment 1

↓

Segment 2

↓

Segment 3

↓

Segment 4

↓

Segment N
```

Each segment is transmitted independently across the network.

---

## Why Segmentation is Important

* Improves reliability
* Enables retransmission of only lost segments
* Supports efficient routing
* Prevents oversized packets
* Simplifies error handling

---

# Reassembly

After all segments reach the destination, they are placed back in the correct sequence.

Example:

```text
Segment 4

Segment 2

Segment 1

Segment 3
```

The Transport Layer uses **sequence numbers** to reorder them into:

```text
Segment 1

↓

Segment 2

↓

Segment 3

↓

Segment 4
```

The application receives the original file exactly as it was sent.

---

# Multiplexing

## What is Multiplexing?

Multiplexing allows multiple applications on the same computer to send data over a single network connection simultaneously.

Example:

Your computer is running:

* Chrome
* Microsoft Teams
* Spotify
* Outlook

All applications send traffic at the same time.

The Transport Layer assigns different **port numbers** to each application.

```text
Chrome

↓

Port 443

-------------------

Teams

↓

Port 443

-------------------

Spotify

↓

Port 4070

-------------------

Outlook

↓

Port 993
```

Although all traffic shares the same network interface, each application remains independent.

---

# Demultiplexing

## What is Demultiplexing?

Demultiplexing is the reverse process.

When data arrives at the destination, the Transport Layer examines the destination port number and forwards the data to the correct application.

Example:

Incoming Packet

↓

Destination Port:

```text
443
```

↓

Delivered to:

```text
Chrome Browser
```

---

# TCP (Transmission Control Protocol)

## What is TCP?

TCP is a **connection-oriented** Transport Layer protocol that provides reliable communication.

Before transmitting data, TCP establishes a connection between the sender and receiver.

TCP guarantees:

* Reliable delivery
* Ordered delivery
* Error recovery
* Flow control
* Congestion control

---

## Characteristics of TCP

* Connection-oriented
* Reliable
* Uses acknowledgments
* Retransmits lost segments
* Uses sequence numbers
* Performs error checking
* Slower than UDP due to reliability mechanisms

---

## Applications Using TCP

* HTTP
* HTTPS
* FTP
* SSH
* SMTP
* IMAP
* POP3

These applications require reliable delivery.

---

# UDP (User Datagram Protocol)

## What is UDP?

UDP is a **connectionless** Transport Layer protocol.

Unlike TCP, UDP does not establish a connection before sending data.

It simply sends datagrams without guaranteeing delivery.

---

## Characteristics of UDP

* Connectionless
* Faster
* Lower overhead
* No acknowledgments
* No retransmissions
* No guaranteed delivery
* No sequencing

---

## Applications Using UDP

* DNS
* VoIP
* Online Gaming
* Live Streaming
* Video Conferencing
* DHCP
* TFTP

These applications prioritize speed over reliability.

---

# TCP vs UDP

| Feature         | TCP                       | UDP                    |
| --------------- | ------------------------- | ---------------------- |
| Connection      | Connection-Oriented       | Connectionless         |
| Reliability     | Reliable                  | Unreliable             |
| Speed           | Slower                    | Faster                 |
| Acknowledgments | Yes                       | No                     |
| Error Recovery  | Yes                       | No                     |
| Ordering        | Guaranteed                | Not Guaranteed         |
| Header Size     | 20 Bytes (minimum)        | 8 Bytes                |
| Typical Use     | Web, Email, File Transfer | Streaming, Gaming, DNS |

---

# Ports

## What is a Port?

A **Port** is a logical communication endpoint used by the Transport Layer to identify applications and services running on a device.

An IP address identifies **which device** should receive data.

A port number identifies **which application** on that device should receive the data.

Example:

```text
IP Address

192.168.1.10

↓

Port

443

↓

HTTPS Service
```

---

## Common Port Numbers

| Port | Protocol/Service |
| ---- | ---------------- |
| 20   | FTP Data         |
| 21   | FTP Control      |
| 22   | SSH              |
| 23   | Telnet           |
| 25   | SMTP             |
| 53   | DNS              |
| 67   | DHCP Server      |
| 68   | DHCP Client      |
| 80   | HTTP             |
| 110  | POP3             |
| 143  | IMAP             |
| 443  | HTTPS            |
| 3389 | RDP              |

---

## Port Ranges

| Range       | Description             |
| ----------- | ----------------------- |
| 0–1023      | Well-Known Ports        |
| 1024–49151  | Registered Ports        |
| 49152–65535 | Dynamic/Ephemeral Ports |

---

# Sockets

## What is a Socket?

A **Socket** uniquely identifies a network connection.

A socket consists of:

* Source IP Address
* Source Port
* Destination IP Address
* Destination Port

Example:

```text
Source IP:

192.168.1.20

Source Port:

51512

↓

Destination IP:

142.250.183.46

Destination Port:

443
```

This unique combination allows multiple simultaneous connections between devices.

---

# Cybersecurity Perspective

SOC Analysts frequently analyze Transport Layer activity to:

* Detect port scans
* Investigate suspicious connections
* Identify malware communication
* Monitor unusual TCP or UDP traffic
* Correlate firewall alerts with destination ports
* Analyze network captures in Wireshark
* Validate allowed and blocked services

Understanding ports, TCP, UDP, and sockets helps analysts determine which applications are communicating and whether the activity is legitimate or malicious.

---

# Key Takeaways

* The Transport Layer provides end-to-end communication.
* TCP uses **segments**, while UDP uses **datagrams**.
* Segmentation improves reliability and efficiency.
* Multiplexing allows multiple applications to communicate simultaneously.
* Demultiplexing delivers incoming data to the correct application.
* TCP prioritizes reliability; UDP prioritizes speed.
* Port numbers identify services and applications.
* Sockets uniquely identify network connections.
---

# TCP Three-Way Handshake

## What is the Three-Way Handshake?

The **TCP Three-Way Handshake** is the process used by TCP to establish a reliable connection between a client and a server before data transmission begins.

The handshake ensures that:

* Both devices are reachable.
* Both devices agree to communicate.
* Initial sequence numbers are synchronized.
* Resources are allocated for the connection.

Without this process, reliable communication cannot occur.

---

## Why is it Needed?

Imagine making a phone call.

You don't immediately start talking.

Instead:

1. You call someone.
2. They answer.
3. You confirm they can hear you.

Only then does the conversation begin.

TCP follows a similar process.

---

## Step 1 – SYN

The client initiates the connection by sending a **SYN (Synchronize)** packet.

Purpose:

* Requests a connection.
* Sends the client's Initial Sequence Number (ISN).

```text
Client                     Server

SYN
Seq = 1000
-------------------------->
```

---

## Step 2 – SYN-ACK

The server receives the SYN request and responds with:

* SYN
* ACK (Acknowledgment)

Purpose:

* Accept the connection request.
* Send the server's Initial Sequence Number.

```text
Client                     Server

<--------------------------
SYN
ACK
Seq = 5000
Ack = 1001
```

---

## Step 3 – ACK

The client acknowledges the server.

```text
Client                     Server

ACK
Ack = 5001
-------------------------->
```

Connection established.

---

## Complete Three-Way Handshake

```text
        Client                     Server

          SYN  ------------------------>

               <-------------------- SYN ACK

          ACK  ------------------------>

        Connection Established
```

---

## Real-World Example

When opening:

```text
https://www.google.com
```

The browser:

1. Resolves the DNS name.
2. Starts a TCP handshake.
3. Establishes the TCP connection.
4. Starts the TLS handshake (HTTPS).
5. Sends the HTTP request.

---

## Importance

The handshake provides:

* Reliable communication
* Sequence synchronization
* Error handling
* Connection initialization

---

# TCP Four-Way Termination

## What is TCP Connection Termination?

After communication is complete, TCP gracefully closes the connection.

Unlike the handshake, termination requires **four packets**.

---

## Why Four Steps?

TCP connections are **full duplex**.

Each side must close its own communication channel independently.

---

## Step 1 – FIN

Client requests to terminate communication.

```text
Client

FIN

------------------------>

Server
```

---

## Step 2 – ACK

Server acknowledges.

```text
Client

<------------------------

ACK

Server
```

---

## Step 3 – FIN

Server finishes its remaining communication and sends its own FIN.

```text
Client

<------------------------

FIN

Server
```

---

## Step 4 – ACK

Client acknowledges.

```text
Client

ACK

------------------------>

Server
```

Connection closed.

---

## Complete Diagram

```text
Client                     Server

FIN  ------------------------>

      <-------------------- ACK

      <-------------------- FIN

ACK  ------------------------>

Connection Closed
```

---

# Flow Control

## What is Flow Control?

Flow Control ensures that a fast sender does not overwhelm a slower receiver.

Example:

Server:

```text
10 Gbps
```

Laptop:

```text
100 Mbps
```

Without flow control:

* Buffer overflow
* Packet loss
* Poor performance

---

## How TCP Implements Flow Control

TCP uses the **Receive Window**.

The receiver informs the sender how much data it can currently accept.

Example:

```text
Receive Window

4096 Bytes
```

The sender must not exceed this amount until further acknowledgments are received.

---

# Sliding Window

## What is Sliding Window?

The Sliding Window mechanism improves efficiency by allowing multiple packets to be sent before waiting for acknowledgments.

Instead of:

```text
Packet

↓

ACK

↓

Packet

↓

ACK
```

TCP sends:

```text
Packet 1

Packet 2

Packet 3

Packet 4

↓

ACK
```

This increases throughput and reduces network latency.

---

## Example

Window Size:

```text
4 Segments
```

Transmission:

```text
Segment 1

Segment 2

Segment 3

Segment 4

↓

ACK

↓

Window Slides

↓

Segment 5

Segment 6
```

---

## Benefits

* Higher throughput
* Better bandwidth utilization
* Fewer delays
* Improved efficiency

---

# Sequence Numbers

## What are Sequence Numbers?

Every TCP segment contains a **Sequence Number**.

Purpose:

* Maintain correct order
* Detect missing segments
* Support retransmission

---

## Example

```text
Segment 1

Seq = 1000

----------------

Segment 2

Seq = 2000

----------------

Segment 3

Seq = 3000
```

If Segment 2 is missing:

The receiver immediately detects the gap.

---

# Acknowledgments (ACK)

## What is an ACK?

TCP uses acknowledgments to confirm successful delivery.

Example:

```text
Client

Seq = 1000

↓

Server

ACK = 1001
```

Meaning:

"I successfully received everything up to byte 1000."

---

## Why ACKs Matter

ACKs help:

* Confirm delivery
* Trigger retransmissions
* Maintain reliability
* Support flow control

---

# Error Detection

TCP detects transmission errors using a **Checksum**.

---

## TCP Checksum

Each TCP segment includes a checksum.

Process:

Sender:

1. Calculates checksum.
2. Places checksum in header.

Receiver:

1. Calculates checksum again.
2. Compares values.

If they match:

Segment accepted.

If not:

Segment discarded.

---

## Why Checksums Are Important

Checksums detect:

* Corrupted packets
* Bit errors
* Damaged transmissions
* Memory corruption

---

# Retransmission

## What is Retransmission?

If a segment is lost, TCP automatically sends it again.

---

## How TCP Detects Packet Loss

### Method 1

Timeout

No ACK received.

↓

Resend segment.

---

### Method 2

Duplicate ACKs

Receiver repeatedly acknowledges the same sequence number.

This indicates that a segment is missing.

---

## Example

```text
Segment 1

✓

Segment 2

Lost

Segment 3

Arrives

↓

Receiver

ACK = Segment 2

↓

Sender

Retransmits Segment 2
```

---

# Congestion Control

## What is Congestion?

Congestion occurs when network devices become overloaded with more traffic than they can process.

Symptoms:

* High latency
* Packet loss
* Slow downloads
* Connection timeouts

---

## TCP Congestion Control

TCP automatically reduces transmission speed when congestion is detected.

This prevents network collapse.

---

## Slow Start

TCP begins with a small congestion window.

Example:

```text
1 Segment

↓

2 Segments

↓

4 Segments

↓

8 Segments

↓

16 Segments
```

Transmission rate increases gradually until packet loss occurs.

---

## Congestion Avoidance

Instead of doubling rapidly, TCP increases the window slowly to avoid overloading the network.

---

## Fast Retransmit

If multiple duplicate ACKs are received, TCP retransmits the missing segment immediately without waiting for the timeout.

---

## Fast Recovery

After retransmission, TCP reduces the congestion window but avoids returning to the very beginning of Slow Start, improving recovery time.

---

# Cybersecurity Relevance

SOC Analysts frequently investigate issues related to the Transport Layer.

Examples include:

* Large numbers of SYN packets indicating possible SYN Flood attacks.
* Numerous retransmissions suggesting packet loss or network instability.
* Unexpected connections to uncommon ports.
* High volumes of UDP traffic that may indicate UDP Flood attacks.
* Abnormal TCP resets that could signal scanning or connection interference.

Transport Layer analysis is commonly performed using:

* Wireshark
* TCPdump
* Firewall logs
* IDS/IPS alerts
* SIEM platforms such as Splunk or Microsoft Sentinel

---

# Key Takeaways

* TCP establishes connections using the **Three-Way Handshake**.
* TCP closes connections using the **Four-Way Termination** process.
* Flow Control prevents senders from overwhelming receivers.
* The Sliding Window improves network efficiency.
* Sequence Numbers maintain the correct order of segments.
* Acknowledgments confirm successful delivery.
* Checksums detect transmission errors.
* Retransmission ensures reliable communication.
* Congestion Control prevents network overload and maintains performance.
---

# Transport Layer Security Relevance

## Introduction

The Transport Layer is a common target for attackers because it manages TCP and UDP communication between applications. SOC Analysts monitor Layer 4 traffic to identify suspicious connections, abnormal port activity, and denial-of-service attacks.

Common monitoring sources include:

* Firewall Logs
* IDS/IPS Alerts
* SIEM Platforms (Splunk, Microsoft Sentinel)
* NetFlow/sFlow
* Wireshark Packet Captures
* Endpoint Detection and Response (EDR)

Understanding Layer 4 helps analysts determine whether traffic is legitimate or malicious.

---

# Common Transport Layer Attacks

The most common attacks targeting Layer 4 include:

* SYN Flood Attack
* TCP Reset Attack
* UDP Flood Attack
* Port Scanning
* TCP Session Hijacking
* Connection Exhaustion

---

# SYN Flood Attack

## What is a SYN Flood?

A SYN Flood is a **Denial-of-Service (DoS)** attack that exploits the TCP Three-Way Handshake.

The attacker sends thousands of SYN packets but never completes the handshake.

This causes the server to keep many half-open connections, eventually exhausting its resources.

---

## Attack Process

```text
Attacker

↓

SYN

↓

Server

↓

SYN-ACK

↓

(No ACK Received)

↓

Half-Open Connection

↓

Repeat Thousands of Times

↓

Server Resources Exhausted
```

---

## Indicators

SOC Analysts may observe:

* Large number of SYN packets
* Few ACK responses
* High number of half-open TCP sessions
* Increased CPU and memory usage on the server
* Service slowdown or unavailability

---

## Prevention

* SYN Cookies
* Rate Limiting
* Firewall Rules
* Intrusion Prevention Systems (IPS)
* Load Balancers
* DDoS Protection Services

---

# TCP Reset (RST) Attack

## What is a TCP Reset Attack?

TCP uses the **RST (Reset)** flag to immediately terminate a connection.

Attackers can send forged TCP Reset packets to disrupt communication between two systems.

---

## Attack Diagram

```text
Client

↓

TCP Connection

↓

Attacker Sends Fake RST

↓

Connection Closed
```

---

## Impact

* Interrupted file transfers
* VPN disconnections
* Remote session termination
* Application outages

---

## Detection

SOC Analysts investigate:

* Unexpected TCP RST packets
* Sudden session termination
* Repeated connection resets
* IDS/IPS alerts

---

## Prevention

* Encrypt traffic using TLS/SSL
* Implement firewall filtering
* Use authenticated VPNs
* Monitor abnormal RST traffic

---

# UDP Flood Attack

## What is a UDP Flood?

A UDP Flood is a Denial-of-Service attack where an attacker sends a massive number of UDP packets to random or targeted ports.

The victim attempts to process each packet, consuming CPU, memory, and bandwidth.

---

## Attack Flow

```text
Attacker

↓

Millions of UDP Packets

↓

Server

↓

CPU Usage Increases

↓

Bandwidth Saturation

↓

Service Unavailable
```

---

## Indicators

* High UDP traffic
* Network congestion
* Increased latency
* Packet loss
* Server slowdown

---

## Prevention

* Firewall Rules
* Rate Limiting
* DDoS Protection
* IDS/IPS
* Traffic Filtering

---

# Port Scanning

## What is Port Scanning?

Port Scanning is the process of identifying open, closed, or filtered ports on a system.

Attackers use it to discover running services before attempting exploitation.

Security teams also perform port scanning during vulnerability assessments.

---

## Why Attackers Scan Ports

* Identify services
* Discover vulnerabilities
* Detect operating systems
* Find outdated software
* Plan further attacks

---

## Common Scan Types

### TCP Connect Scan

Completes the full TCP Three-Way Handshake.

---

### SYN Scan (Half-Open Scan)

Sends only a SYN packet and analyzes the response.

Often called a stealth scan.

---

### UDP Scan

Checks whether UDP ports are open.

---

### FIN Scan

Uses TCP FIN packets to identify open ports.

---

### NULL Scan

Sends packets with no TCP flags set.

---

### XMAS Scan

Sends packets with FIN, PSH, and URG flags enabled.

---

## Nmap Examples

Scan a target:

```bash
nmap 192.168.1.10
```

Scan specific ports:

```bash
nmap -p 22,80,443 192.168.1.10
```

Stealth SYN Scan:

```bash
nmap -sS 192.168.1.10
```

UDP Scan:

```bash
nmap -sU 192.168.1.10
```

Service Version Detection:

```bash
nmap -sV 192.168.1.10
```

Operating System Detection:

```bash
nmap -O 192.168.1.10
```

---

# Firewalls and Port Filtering

## Why Port Filtering?

Not every service should be accessible from the Internet.

Firewalls inspect incoming and outgoing packets and determine whether they should be allowed or blocked.

---

## Example

Allow:

```text
TCP 443 (HTTPS)
```

Block:

```text
TCP 23 (Telnet)
```

---

## Common Firewall Actions

* Allow
* Deny
* Reject
* Log
* Rate Limit

---

## Best Practices

* Close unused ports
* Disable Telnet
* Use SSH instead
* Restrict RDP access
* Enable logging
* Review firewall rules regularly

---

# Wireshark Lab

## Objective

Capture TCP and UDP traffic.

---

## Requirements

* Wireshark
* Internet Connection

---

## Steps

1. Open Wireshark.
2. Select the active network interface.
3. Start packet capture.
4. Open a website.
5. Stop the capture.
6. Analyze TCP packets.

---

## Useful Display Filters

Show TCP traffic:

```text
tcp
```

Show UDP traffic:

```text
udp
```

Show TCP SYN packets:

```text
tcp.flags.syn == 1
```

Show TCP Reset packets:

```text
tcp.flags.reset == 1
```

Show traffic on Port 443:

```text
tcp.port == 443
```

Show DNS traffic:

```text
udp.port == 53
```

---

# Useful Commands

## Windows

Display active TCP connections:

```cmd
netstat -ano
```

Display listening ports:

```cmd
netstat -an
```

Display processes:

```cmd
tasklist
```

---

## Linux

Display listening ports:

```bash
ss -tuln
```

or

```bash
netstat -tulnp
```

Display established TCP connections:

```bash
ss -tan
```

Capture packets:

```bash
sudo tcpdump -i eth0
```

---

# SOC Investigation Scenario

## Alert

```
Multiple SYN packets detected from 198.51.100.45
```

---

## Investigation

1. Review firewall logs.
2. Identify destination server.
3. Check SYN packet rate.
4. Verify ACK responses.
5. Examine packet captures.
6. Determine whether a SYN Flood is occurring.
7. Check IDS/IPS alerts.
8. Block the malicious IP if necessary.
9. Escalate according to the incident response process.

---

## Sample Findings

* More than 50,000 SYN packets received in one minute.
* No corresponding ACK packets.
* Multiple half-open TCP connections.
* Firewall generated DoS alerts.
* Web application became temporarily unavailable.

---

# Interview Questions

## 1. What is the primary responsibility of the Transport Layer?

To provide end-to-end communication, segmentation, reliability, flow control, and port-based delivery between applications.

---

## 2. What is the difference between TCP and UDP?

TCP is connection-oriented and reliable, while UDP is connectionless, faster, and does not guarantee delivery.

---

## 3. What is the TCP Three-Way Handshake?

It is the connection establishment process consisting of SYN → SYN-ACK → ACK.

---

## 4. What is a SYN Flood attack?

A Denial-of-Service attack that overwhelms a server with incomplete TCP connection requests.

---

## 5. What is Port Scanning?

The process of discovering open, closed, or filtered ports on a target system.

---

## 6. Which protocol is commonly used for DNS?

UDP (Port 53), though TCP may also be used for larger responses and zone transfers.

---

## 7. What is Flow Control?

A TCP mechanism that prevents a sender from transmitting data faster than the receiver can process it.

---

## 8. What is the purpose of a Port Number?

It identifies the destination application or service running on a device.

---

## 9. Which command displays active network connections on Windows?

```cmd
netstat -ano
```

---

## 10. Name five common TCP ports.

* 21 – FTP
* 22 – SSH
* 25 – SMTP
* 80 – HTTP
* 443 – HTTPS

---

# Hands-on Lab

## Objective

Explore active network connections and open ports.

### Windows

Run:

```cmd
netstat -ano
```

Observe:

* Local Address
* Foreign Address
* State
* PID

Identify:

* Active TCP connections
* Listening services
* Established sessions

---

### Linux

Run:

```bash
ss -tuln
```

or

```bash
netstat -tulnp
```

Identify:

* Listening TCP ports
* Listening UDP ports
* Active connections

---

### Nmap Practice

Scan your local machine:

```bash
nmap localhost
```

Scan another device on your lab network (only systems you own or are authorized to test):

```bash
nmap 192.168.1.100
```

Observe:

* Open ports
* Service names
* Port states

---

# Best Practices

* Disable unused services.
* Close unnecessary ports.
* Use secure protocols (SSH instead of Telnet, HTTPS instead of HTTP).
* Monitor network traffic continuously.
* Enable firewall logging.
* Apply rate limiting to public-facing services.
* Keep servers patched and updated.
* Review open ports regularly.

---

# Key Takeaways

* The Transport Layer provides reliable end-to-end communication.
* TCP offers reliability through acknowledgments, retransmissions, and flow control.
* UDP provides fast, connectionless communication for latency-sensitive applications.
* Ports identify applications and services.
* Common Layer 4 attacks include SYN Floods, UDP Floods, and TCP Reset attacks.
* Firewalls and IDS/IPS play a critical role in defending Transport Layer communications.
* SOC Analysts use logs, packet captures, and monitoring tools to investigate Layer 4 incidents.

---

# Summary

The Transport Layer is responsible for delivering data between applications reliably and efficiently. It manages segmentation, connection establishment, flow control, error recovery, and port-based communication. Understanding TCP, UDP, ports, handshakes, and common Layer 4 attacks enables cybersecurity professionals to troubleshoot connectivity issues, detect malicious activity, investigate incidents, and strengthen network defenses. Mastery of this layer is essential for SOC Analysts, Network Engineers, and Incident Responders.

