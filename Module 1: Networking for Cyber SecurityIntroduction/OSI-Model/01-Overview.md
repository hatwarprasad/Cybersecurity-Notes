# OSI Model Overview

## Introduction

The **OSI (Open Systems Interconnection) Model** is a conceptual framework developed by the **International Organization for Standardization (ISO)** to explain how data travels from one device to another over a network.

Rather than being a protocol itself, the OSI Model provides a standardized way to understand network communication by dividing it into **seven logical layers**. Each layer has a specific responsibility and communicates with the layers directly above and below it.

The OSI Model is one of the most important networking concepts for Cyber Security Analysts, Network Engineers, System Administrators, and Penetration Testers because it helps identify where communication problems occur and where security controls should be applied.

---

# Learning Objectives

After completing this topic, you should be able to:

* Understand the purpose of the OSI Model.
* Explain why the OSI Model was created.
* Identify all seven layers.
* Describe the function of each layer.
* Understand how data moves through the layers.
* Explain encapsulation and decapsulation.
* Relate each layer to real-world cybersecurity tasks.

---

# What is the OSI Model?

The OSI Model is a **seven-layer networking model** that describes how information moves between devices across a network.

Instead of treating communication as one large process, the OSI Model breaks it into smaller, manageable steps. Each layer performs a dedicated function before passing the data to the next layer.

Think of it like sending a parcel through a courier service:

1. You pack the item.
2. You write the address.
3. The courier collects it.
4. It travels through sorting centers.
5. It reaches the destination city.
6. The local office delivers it.
7. The recipient opens the package.

Similarly, when you open a website, your computer prepares, packages, routes, transmits, and delivers data through the seven OSI layers.

---

# Why Was the OSI Model Created?

Before the OSI Model, networking technologies from different vendors often lacked compatibility.

The OSI Model introduced a common framework so that devices and software from different manufacturers could communicate using standardized networking principles.

Benefits include:

* Standardization
* Easier troubleshooting
* Better interoperability
* Simplified learning
* Modular design
* Improved security planning

---

# The Seven Layers of the OSI Model

| Layer | Name         | Main Responsibility                             |
| ----- | ------------ | ----------------------------------------------- |
| 7     | Application  | Provides network services to user applications  |
| 6     | Presentation | Data formatting, encryption, compression        |
| 5     | Session      | Establishes, manages, and terminates sessions   |
| 4     | Transport    | Reliable delivery, segmentation, error recovery |
| 3     | Network      | Logical addressing and routing                  |
| 2     | Data Link    | MAC addressing and frame delivery               |
| 1     | Physical     | Transmission of raw bits over the medium        |

---

# OSI Model Diagram

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

Data travels **down** the layers when sending and **up** the layers when receiving.

---

# Data Flow Through the OSI Model

### Sending Data

```text
Application
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

### Receiving Data

```text
Physical
     ↑
Data Link
     ↑
Network
     ↑
Transport
     ↑
Session
     ↑
Presentation
     ↑
Application
```

---

# How the OSI Model Works

Imagine you visit:

```
https://www.example.com
```

The communication occurs as follows:

1. Your browser creates an HTTP request.
2. Data is formatted and encrypted (HTTPS).
3. A communication session is established.
4. TCP divides the data into segments.
5. IP assigns source and destination addresses.
6. Ethernet adds MAC addresses.
7. Bits are transmitted over the network.

The destination device performs the reverse process to reconstruct the original data.

---

# Data Units at Each Layer

| Layer        | Data Unit                      |
| ------------ | ------------------------------ |
| Application  | Data                           |
| Presentation | Data                           |
| Session      | Data                           |
| Transport    | Segment (TCP) / Datagram (UDP) |
| Network      | Packet                         |
| Data Link    | Frame                          |
| Physical     | Bits                           |

---

# Devices Associated with OSI Layers

| Device       | Common Layer                  |
| ------------ | ----------------------------- |
| Hub          | Layer 1                       |
| Repeater     | Layer 1                       |
| Switch       | Layer 2                       |
| Bridge       | Layer 2                       |
| Router       | Layer 3                       |
| Firewall     | Layer 3/4/7 (depends on type) |
| Proxy Server | Layer 7                       |

---

# Real-World Example

Suppose a user in Mumbai accesses a web server in Hyderabad.

The request follows these steps:

* Browser creates an HTTPS request.
* TCP establishes a connection.
* IP determines the destination.
* Router forwards the packet.
* Switch delivers the frame.
* Signals travel over fiber-optic cables.
* The server receives and processes the request.
* The response follows the same layers in reverse.

---

# Why the OSI Model Matters in Cybersecurity

Cybersecurity professionals use the OSI Model to understand where attacks occur and how to investigate them.

Examples:

### Layer 7 (Application)

* SQL Injection
* Cross-Site Scripting (XSS)
* Phishing
* Malicious HTTP requests

### Layer 6 (Presentation)

* SSL/TLS certificate issues
* Encryption problems

### Layer 5 (Session)

* Session hijacking
* Session fixation

### Layer 4 (Transport)

* TCP SYN Flood
* Port scanning

### Layer 3 (Network)

* IP spoofing
* Routing attacks

### Layer 2 (Data Link)

* MAC spoofing
* ARP spoofing

### Layer 1 (Physical)

* Cable tampering
* Device theft
* Hardware sabotage

---

# SOC Analyst Perspective

A SOC Analyst frequently investigates incidents using knowledge of multiple OSI layers.

Examples:

| Alert                  | Relevant Layer |
| ---------------------- | -------------- |
| Multiple failed logins | Application    |
| Suspicious IP address  | Network        |
| Port scan detected     | Transport      |
| ARP spoofing           | Data Link      |
| Cable disconnected     | Physical       |

Understanding the OSI Model helps analysts identify where an issue originates and which logs or tools to examine.

---

# Memory Trick

Remember the layers from top to bottom:

**All People Seem To Need Data Processing**

* Application
* Presentation
* Session
* Transport
* Network
* Data Link
* Physical

From bottom to top:

**Please Do Not Throw Sausage Pizza Away**

* Physical
* Data Link
* Network
* Transport
* Session
* Presentation
* Application

---

# Advantages of the OSI Model

* Standardized networking framework
* Easier troubleshooting
* Vendor-independent
* Modular design
* Simplifies learning
* Helps map security controls

---

# Limitations

* Conceptual model rather than a real protocol stack.
* Modern networks commonly use the TCP/IP model.
* Some protocols span multiple OSI layers.
* Real implementations do not always fit neatly into one layer.

---

# Key Takeaways

* The OSI Model divides network communication into seven layers.
* Each layer has a specific responsibility.
* Data is encapsulated as it moves down the layers and decapsulated as it moves up.
* The model simplifies troubleshooting and security analysis.
* Cybersecurity professionals use the OSI Model to understand attacks, analyze traffic, and investigate incidents.

---

# Interview Questions

### 1. What is the OSI Model?

The OSI Model is a seven-layer conceptual framework that explains how data travels across a network.

---

### 2. Who developed the OSI Model?

The International Organization for Standardization (ISO).

---

### 3. How many layers are in the OSI Model?

Seven.

---

### 4. Which layer is responsible for routing?

The Network Layer (Layer 3).

---

### 5. Which layer handles MAC addresses?

The Data Link Layer (Layer 2).

---

### 6. Which layer deals with physical cables and signals?

The Physical Layer (Layer 1).

---

### 7. Why is the OSI Model important for cybersecurity?

It helps identify where attacks occur, improves troubleshooting, and provides a structured way to analyze network traffic and security events.



# Summary

The OSI Model is the foundation of computer networking and an essential concept for cybersecurity. Whether you're analyzing packets in Wireshark, investigating a SIEM alert, troubleshooting a network outage, or responding to an attack, understanding the OSI layers helps you determine where communication is occurring and where problems or threats may exist.
