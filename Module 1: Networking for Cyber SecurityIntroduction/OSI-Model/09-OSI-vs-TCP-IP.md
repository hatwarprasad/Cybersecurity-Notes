
# OSI Model vs TCP/IP Model

## Introduction

The **OSI (Open Systems Interconnection)** Model and the **TCP/IP (Transmission Control Protocol/Internet Protocol)** Model are two fundamental networking models used to understand how devices communicate over a network.

Although both models describe the communication process, they differ in their structure, number of layers, purpose, and practical implementation.

* The **OSI Model** is primarily a **reference model** used for learning, troubleshooting, and designing networks.
* The **TCP/IP Model** is the **practical networking model** used on the Internet and in modern computer networks.

Understanding the differences between these models is essential for Network Engineers, SOC Analysts, Security Engineers, and Cybersecurity Professionals.

---

# Learning Objectives

After completing this chapter, you should be able to:

* Understand the purpose of the OSI Model.
* Understand the TCP/IP Model.
* Compare the layers of both models.
* Identify which protocols belong to each layer.
* Explain why the TCP/IP Model is used in real-world networking.
* Apply both models during cybersecurity investigations.

---

# What is the OSI Model?

The **OSI Model** is a conceptual framework developed by the **International Organization for Standardization (ISO)** in 1984.

It divides network communication into **seven distinct layers**, each responsible for specific networking functions.

The OSI Model helps engineers understand how data flows through a network and simplifies troubleshooting by isolating problems to individual layers.

---

# OSI Layers

```text
+-----------------------------+
| Layer 7 - Application       |
+-----------------------------+
| Layer 6 - Presentation      |
+-----------------------------+
| Layer 5 - Session           |
+-----------------------------+
| Layer 4 - Transport         |
+-----------------------------+
| Layer 3 - Network           |
+-----------------------------+
| Layer 2 - Data Link         |
+-----------------------------+
| Layer 1 - Physical          |
+-----------------------------+
```

---

# What is the TCP/IP Model?

The **TCP/IP Model** is the networking architecture used on the Internet today.

It was developed as part of the **ARPANET** project before the OSI Model became widely known.

Unlike the OSI Model, the TCP/IP Model is based on real protocols that power modern networks.

Most operating systems—including Windows, Linux, macOS, Android, and iOS—implement the TCP/IP protocol suite.

---

# TCP/IP Layers

The TCP/IP Model contains **four layers**.

```text
+-----------------------------+
| Application                 |
+-----------------------------+
| Transport                   |
+-----------------------------+
| Internet                    |
+-----------------------------+
| Network Access              |
+-----------------------------+
```

Some books describe a **five-layer model** by separating the Physical and Data Link layers, but the classic TCP/IP Model contains four layers.

---

# Layer Mapping

The OSI and TCP/IP models can be mapped as follows:

| OSI Model    | TCP/IP Model   |
| ------------ | -------------- |
| Application  | Application    |
| Presentation | Application    |
| Session      | Application    |
| Transport    | Transport      |
| Network      | Internet       |
| Data Link    | Network Access |
| Physical     | Network Access |

---

# Layer Comparison

## OSI Application Layer

Provides services directly to applications.

Examples:

* HTTP
* HTTPS
* DNS
* SMTP
* FTP
* SSH

TCP/IP Equivalent:

Application Layer

---

## OSI Presentation Layer

Responsible for:

* Encryption
* Compression
* Translation
* Character Encoding

TCP/IP Equivalent:

Application Layer

---

## OSI Session Layer

Responsible for:

* Session Establishment
* Session Maintenance
* Session Termination

TCP/IP Equivalent:

Application Layer

---

## OSI Transport Layer

Responsible for:

* TCP
* UDP
* Segmentation
* Flow Control
* Reliability

TCP/IP Equivalent:

Transport Layer

---

## OSI Network Layer

Responsible for:

* IP Addressing
* Routing
* Routers

TCP/IP Equivalent:

Internet Layer

---

## OSI Data Link Layer

Responsible for:

* Ethernet
* Switching
* MAC Addresses
* VLANs

TCP/IP Equivalent:

Network Access Layer

---

## OSI Physical Layer

Responsible for:

* Cables
* Bits
* Electrical Signals
* Fiber Optics

TCP/IP Equivalent:

Network Access Layer

---

# Protocol Comparison

## Application Layer Protocols

| OSI   | TCP/IP |
| ----- | ------ |
| HTTP  | HTTP   |
| HTTPS | HTTPS  |
| DNS   | DNS    |
| SMTP  | SMTP   |
| FTP   | FTP    |
| SSH   | SSH    |

---

## Transport Layer Protocols

| OSI | TCP/IP |
| --- | ------ |
| TCP | TCP    |
| UDP | UDP    |

---

## Network Layer Protocols

| OSI  | TCP/IP |
| ---- | ------ |
| IP   | IP     |
| ICMP | ICMP   |
| ARP* | ARP*   |

> *ARP is often associated with Layer 2/Layer 3 interactions depending on the networking model and implementation.

---

## Data Link Layer Protocols

Examples:

* Ethernet
* PPP
* Frame Relay

TCP/IP Equivalent:

Network Access Layer

---

# OSI vs TCP/IP Comparison Table

| Feature              | OSI Model            | TCP/IP Model   |
| -------------------- | -------------------- | -------------- |
| Number of Layers     | 7                    | 4              |
| Developed By         | ISO                  | DARPA          |
| Type                 | Reference Model      | Protocol Suite |
| Practical Use        | Educational & Design | Real Networks  |
| Session Layer        | Separate             | Combined       |
| Presentation Layer   | Separate             | Combined       |
| Internet Standard    | No                   | Yes            |
| Protocol Independent | Yes                  | No             |

---

# Advantages of the OSI Model

* Easy to understand
* Excellent for learning
* Simplifies troubleshooting
* Modular design
* Vendor independent
* Standardized reference model

---

# Limitations of the OSI Model

* Rarely implemented exactly as designed
* More theoretical
* Some layers overlap
* More complex than TCP/IP

---

# Advantages of the TCP/IP Model

* Used worldwide
* Internet standard
* Proven reliability
* Supports millions of devices
* Simple architecture
* Practical implementation

---

# Limitations of the TCP/IP Model

* Less modular than OSI
* Does not clearly separate Session and Presentation functions
* Less useful as a teaching model for layer-specific concepts

---

# Encapsulation Comparison

## OSI Model

```text
Application Data

↓

Presentation

↓

Session

↓

Transport

↓

Segment

↓

Network

↓

Packet

↓

Data Link

↓

Frame

↓

Physical

↓

Bits
```

---

## TCP/IP Model

```text
Application Data

↓

Transport

↓

Segment

↓

Internet

↓

Packet

↓

Network Access

↓

Frame

↓

Bits
```

---

# Troubleshooting Using the OSI Model

One of the biggest advantages of the OSI Model is structured troubleshooting.

| Problem                | OSI Layer    |
| ---------------------- | ------------ |
| Cable unplugged        | Physical     |
| Switch issue           | Data Link    |
| Incorrect IP Address   | Network      |
| TCP Connection Failure | Transport    |
| Authentication Issue   | Session      |
| Certificate Error      | Presentation |
| Website Not Loading    | Application  |

---

# Cybersecurity Perspective

Cybersecurity professionals frequently use both models.

### SOC Analyst

* Analyze packets
* Review firewall logs
* Investigate TCP sessions
* Detect malicious traffic

### Penetration Tester

* Port scanning
* Protocol analysis
* Network enumeration
* Web application testing

### Incident Responder

* Trace attack paths
* Identify affected layers
* Analyze network captures
* Contain attacks

---

# Real-World Example

Suppose a user visits:

```text
https://github.com
```

### OSI Model

1. Application – Browser generates an HTTP request.
2. Presentation – TLS encrypts the data.
3. Session – Session is established and maintained.
4. Transport – TCP creates segments.
5. Network – IP addresses are added.
6. Data Link – Ethernet frames are created.
7. Physical – Bits are transmitted over the network.

### TCP/IP Model

1. Application – HTTP and TLS processing.
2. Transport – TCP segments the data.
3. Internet – IP routes the packets.
4. Network Access – Ethernet frames are transmitted over the physical medium.

---

# Interview Questions

## 1. What is the main difference between the OSI Model and the TCP/IP Model?

The OSI Model is a theoretical reference model with seven layers, while the TCP/IP Model is a practical networking model with four layers used on the Internet.

---

## 2. Which model is used in real-world networking?

The TCP/IP Model.

---

## 3. How many layers are in the OSI Model?

Seven.

---

## 4. How many layers are in the TCP/IP Model?

Four.

---

## 5. Which OSI layers are combined into the TCP/IP Application Layer?

* Application
* Presentation
* Session

---

## 6. Which OSI layer corresponds to the Internet Layer?

The Network Layer.

---

## 7. Which devices operate at the Network Layer?

Routers.

---

## 8. Which protocols operate at the Transport Layer?

TCP and UDP.

---

## 9. Why is the OSI Model useful?

It simplifies learning, troubleshooting, and understanding network communication.

---

## 10. Why is the TCP/IP Model important?

It is the protocol suite used by the Internet and almost all modern computer networks.

---

# Hands-on Lab

## Objective

Observe communication using networking tools.

### Step 1

Open Wireshark and start capturing packets.

---

### Step 2

Visit:

```text
https://github.com
```

---

### Step 3

Observe:

* DNS Query (Application Layer)
* TCP Three-Way Handshake (Transport Layer)
* IP Packets (Internet/Network Layer)
* Ethernet Frames (Network Access/Data Link Layer)
* TLS Handshake (Application/Presentation Layer)

---

### Step 4

Use the following commands:

Windows:

```cmd
ipconfig
ping github.com
tracert github.com
netstat -ano
nslookup github.com
```

Linux:

```bash
ip addr
ping github.com
traceroute github.com
ss -tuln
dig github.com
```

Relate the output to the corresponding OSI and TCP/IP layers.

---

# Best Practices

* Use the OSI Model for troubleshooting and documentation.
* Understand the TCP/IP Model because it reflects real-world networking.
* Learn common protocols associated with each layer.
* Use packet analysis tools such as Wireshark to observe encapsulation.
* Practice identifying which layer is responsible for specific networking problems.
* Apply layer-based thinking during security investigations.

---

# Key Takeaways

* The OSI Model has **7 layers** and is primarily a reference model.
* The TCP/IP Model has **4 layers** and is the foundation of modern Internet communication.
* Multiple OSI layers are combined into the TCP/IP Application Layer.
* Both models describe how data moves across a network, but they differ in complexity and practical use.
* Understanding both models is essential for networking, cybersecurity, troubleshooting, and incident response.

---

# Summary

The OSI and TCP/IP models provide structured approaches to understanding network communication. The OSI Model offers a detailed, layer-by-layer framework that is valuable for education and troubleshooting, while the TCP/IP Model represents the protocol suite used in real-world networking. By understanding both models and their layer mappings, cybersecurity professionals can analyze network traffic, troubleshoot connectivity issues, investigate attacks, and communicate effectively with other IT professionals.
