# Encapsulation and Decapsulation

## Introduction

**Encapsulation** and **Decapsulation** are two of the most fundamental concepts in computer networking. Every piece of data that travels across a network goes through these two processes.

* **Encapsulation** is the process of **adding protocol-specific headers (and sometimes trailers)** as data moves **down** the OSI or TCP/IP model at the sender.
* **Decapsulation** is the reverse process, where these headers and trailers are **removed** as data moves **up** the OSI or TCP/IP model at the receiver.

These processes allow devices using different hardware, operating systems, and applications to communicate reliably.

For cybersecurity professionals, understanding encapsulation is essential for packet analysis, network troubleshooting, malware investigations, and incident response.

---

# Learning Objectives

After completing this chapter, you should be able to:

* Explain encapsulation and decapsulation.
* Understand how data changes at each OSI layer.
* Identify the Protocol Data Unit (PDU) for each layer.
* Understand headers and trailers.
* Explain how packets travel across a network.
* Analyze packets using Wireshark.
* Apply encapsulation concepts during cybersecurity investigations.

---

# Why Encapsulation is Needed

When an application sends data, the network requires additional information to deliver it correctly.

Examples:

* Which application should receive it?
* Which IP address is the destination?
* Which MAC address is the next hop?
* How should errors be detected?

Each OSI layer adds the information it needs.

---

# Encapsulation Process

Suppose a user opens:

```text
https://github.com
```

The browser generates an HTTP request.

As the data moves downward through the OSI Model, each layer adds its own information.

```text
Application Data

↓

Presentation

↓

Session

↓

Transport

↓

Network

↓

Data Link

↓

Physical
```

---

# Protocol Data Units (PDU)

Each layer has its own data unit.

| OSI Layer    | PDU                            |
| ------------ | ------------------------------ |
| Application  | Data                           |
| Presentation | Data                           |
| Session      | Data                           |
| Transport    | Segment (TCP) / Datagram (UDP) |
| Network      | Packet                         |
| Data Link    | Frame                          |
| Physical     | Bits                           |

---

# Encapsulation at Each Layer

## Layer 7 – Application

The Application Layer creates the original user data.

Example:

```text
GET / HTTP/1.1
Host: github.com
```

PDU:

```text
Data
```

---

## Layer 6 – Presentation

The Presentation Layer prepares the data.

Possible operations:

* UTF-8 Encoding
* Compression
* TLS Encryption

The data is still referred to as:

```text
Data
```

---

## Layer 5 – Session

The Session Layer establishes and manages the communication session.

Examples:

* Session ID
* Authentication
* Session Control

PDU:

```text
Data
```

---

## Layer 4 – Transport

The Transport Layer adds the **TCP or UDP Header**.

Example TCP Header Information:

* Source Port
* Destination Port
* Sequence Number
* Acknowledgment Number
* Flags (SYN, ACK, FIN)
* Window Size
* Checksum

Result:

```text
TCP Header

+

Application Data

=

Segment
```

---

## Layer 3 – Network

The Network Layer adds the **IP Header**.

Typical fields:

* Source IP
* Destination IP
* TTL
* Protocol
* Identification
* Fragment Offset

Result:

```text
IP Header

+

TCP Segment

=

Packet
```

---

## Layer 2 – Data Link

The Data Link Layer adds:

* Ethernet Header
* Frame Check Sequence (FCS) Trailer

Ethernet Header includes:

* Source MAC
* Destination MAC
* EtherType

Result:

```text
Ethernet Header

+

IP Packet

+

FCS Trailer

=

Frame
```

---

## Layer 1 – Physical

The Physical Layer converts the frame into electrical, optical, or radio signals.

Result:

```text
010101010101010...
```

These binary bits travel across the transmission medium.

---

# Complete Encapsulation Diagram

```text
Application Layer
-----------------
Data

↓

Presentation Layer
------------------
Data

↓

Session Layer
-------------
Data

↓

Transport Layer
---------------
TCP Header + Data

↓

Segment

↓

Network Layer
-------------
IP Header + Segment

↓

Packet

↓

Data Link Layer
---------------
Ethernet Header + Packet + FCS

↓

Frame

↓

Physical Layer
--------------
Bits

↓

Transmission Medium
```

---

# Header Overview

Each header contains different information.

| Layer     | Header Information     |
| --------- | ---------------------- |
| Transport | Ports, Sequence Number |
| Network   | Source/Destination IP  |
| Data Link | Source/Destination MAC |
| Physical  | Bits (no header)       |

---

# Trailer

Only the Data Link Layer normally adds a trailer.

Example:

```
Frame Check Sequence (FCS)
```

Purpose:

* Error Detection
* CRC Validation

---

# Decapsulation

At the destination, the process is reversed.

Each layer removes the information it added.

---

## Physical Layer

Receives:

```text
Bits
```

Converts them into:

```text
Frame
```

---

## Data Link Layer

Removes:

* Ethernet Header
* FCS Trailer

Remaining:

```text
Packet
```

---

## Network Layer

Removes:

* IP Header

Remaining:

```text
Segment
```

---

## Transport Layer

Removes:

* TCP Header

Remaining:

```text
Application Data
```

---

## Session Layer

Restores the communication session.

---

## Presentation Layer

Performs:

* Decryption
* Decompression
* Character Decoding

---

## Application Layer

The application receives the original data.

Example:

```text
GitHub Home Page
```

---

# Complete Decapsulation Diagram

```text
Bits

↓

Frame

↓

Packet

↓

Segment

↓

Application Data

↓

Browser Displays Webpage
```

---

# Encapsulation vs Decapsulation

| Encapsulation              | Decapsulation           |
| -------------------------- | ----------------------- |
| Sender Side                | Receiver Side           |
| Adds Headers               | Removes Headers         |
| Data Moves Down the Stack  | Data Moves Up the Stack |
| Creates Frames and Packets | Restores Original Data  |

---

# Real-World Example

A user visits:

```text
https://github.com
```

### Sender

1. Browser creates an HTTP request.
2. TLS encrypts the request.
3. TCP adds a transport header.
4. IP adds source and destination addresses.
5. Ethernet adds MAC addresses.
6. The frame is transmitted as bits.

### Receiver

1. Bits are received.
2. Ethernet header removed.
3. IP header removed.
4. TCP header removed.
5. TLS decrypts the data.
6. HTTP request is processed.
7. GitHub returns a response using the same process in reverse.

---

# Wireshark Lab

## Objective

Observe encapsulation using Wireshark.

### Steps

1. Open Wireshark.
2. Select the active network interface.
3. Start packet capture.
4. Open:

```text
https://github.com
```

5. Stop the capture.

---

## Observe

Expand the packet details.

You should see:

```
Frame

↓

Ethernet II

↓

Internet Protocol

↓

Transmission Control Protocol

↓

Transport Layer Security

↓

HTTP
```

This demonstrates the encapsulation process.

---

## Useful Display Filters

Show TCP traffic:

```text
tcp
```

Show IP packets:

```text
ip
```

Show Ethernet frames:

```text
eth
```

Show TLS traffic:

```text
tls
```

Show DNS traffic:

```text
dns
```

---

# Cybersecurity Perspective

SOC Analysts analyze encapsulated traffic every day.

Common tasks include:

* Reviewing packet captures (PCAP)
* Identifying suspicious IP addresses
* Investigating malicious ports
* Detecting unusual protocols
* Validating TLS handshakes
* Inspecting DNS requests
* Correlating firewall logs with packet data

Understanding which layer added each header helps analysts quickly identify where communication problems or attacks occur.

---

# Interview Questions

## 1. What is encapsulation?

Encapsulation is the process of adding protocol headers (and sometimes trailers) to data as it moves down the networking stack before transmission.

---

## 2. What is decapsulation?

Decapsulation is the process of removing protocol headers and trailers as data moves up the networking stack at the receiving device.

---

## 3. Which layer adds the IP header?

The Network Layer (Layer 3).

---

## 4. Which layer adds the TCP header?

The Transport Layer (Layer 4).

---

## 5. Which layer adds the Ethernet header?

The Data Link Layer (Layer 2).

---

## 6. Which layer adds the Frame Check Sequence (FCS)?

The Data Link Layer.

---

## 7. What is the PDU of the Network Layer?

Packet.

---

## 8. What is the PDU of the Transport Layer?

Segment (TCP) or Datagram (UDP).

---

## 9. Why is encapsulation important?

It provides addressing, routing, reliability, error detection, and application identification so data can travel correctly across networks.

---

## 10. Which tool is commonly used to observe encapsulation?

Wireshark.

---

# Hands-on Lab

## Objective

Identify each protocol layer in a packet capture.

### Exercise

1. Start Wireshark.
2. Visit `https://github.com`.
3. Capture several packets.
4. Select an HTTPS packet.
5. Expand each protocol layer.
6. Identify:

* Ethernet Header
* IP Header
* TCP Header
* TLS
* HTTP (if applicable)

Write down:

* Source MAC Address
* Destination MAC Address
* Source IP Address
* Destination IP Address
* Source Port
* Destination Port

Explain which OSI layer each field belongs to.

---

# Best Practices

* Learn the PDU associated with each OSI layer.
* Understand which headers are added at each layer.
* Practice analyzing packets in Wireshark.
* Correlate packet captures with firewall and IDS/IPS logs.
* Use encapsulation knowledge during troubleshooting and incident response.
* Remember that every network communication follows encapsulation before transmission and decapsulation upon receipt.

---

# Key Takeaways

* Encapsulation adds protocol information as data moves down the OSI stack.
* Decapsulation removes protocol information as data moves up the stack.
* Each OSI layer has a specific responsibility and PDU.
* Headers provide addressing, routing, sequencing, and error-checking information.
* The Data Link Layer adds the FCS trailer for error detection.
* Wireshark is an essential tool for visualizing encapsulation.
* Understanding encapsulation is fundamental for networking, cybersecurity, packet analysis, and SOC investigations.

---

# Summary

Encapsulation and decapsulation are the core mechanisms that enable reliable communication across computer networks. Each OSI layer contributes specific information by adding or removing headers and trailers, ensuring data reaches the correct destination and application. Mastering these concepts allows cybersecurity professionals to interpret packet captures, troubleshoot network issues, investigate security incidents, and understand how protocols interact throughout the communication process.
