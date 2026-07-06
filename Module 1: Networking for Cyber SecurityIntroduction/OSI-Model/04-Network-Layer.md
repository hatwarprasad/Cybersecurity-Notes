# Network Layer (Layer 3)

## Introduction

The **Network Layer** is the **third layer** of the **OSI (Open Systems Interconnection) Model**. It is responsible for **logical addressing, routing, and packet forwarding** between different networks.

Unlike the Data Link Layer, which delivers data only within the same Local Area Network (LAN), the Network Layer enables communication between devices located on different networks, cities, countries, or even continents.

The primary protocol operating at this layer is the **Internet Protocol (IP)**, making it one of the most important layers in modern networking.

For cybersecurity professionals, understanding the Network Layer is essential because many attacks, such as **IP Spoofing, DDoS attacks, routing attacks, and network reconnaissance**, occur at this layer.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the Network Layer.
* Explain logical addressing.
* Differentiate between IPv4 and IPv6.
* Identify private and public IP addresses.
* Understand subnet masks and CIDR notation.
* Explain the function of the default gateway.
* Recognize how routers forward packets.
* Apply Network Layer concepts during cybersecurity investigations.

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
| Layer 4 - Transport         |
+-----------------------------+
| Layer 3 - Network   ← You are here
+-----------------------------+
| Layer 2 - Data Link         |
+-----------------------------+
| Layer 1 - Physical          |
+-----------------------------+
```

---

# Responsibilities of the Network Layer

The Network Layer performs several key functions:

### 1. Logical Addressing

Each device on a network is assigned a logical address called an **IP Address**.

Example:

```text
192.168.1.25
```

Unlike MAC addresses, IP addresses can change depending on the network configuration.

---

### 2. Routing

The Network Layer determines the best path for packets to travel from the source device to the destination device.

Example:

```text
Laptop (Nagpur)
      ↓
Home Router
      ↓
ISP Router
      ↓
Internet
      ↓
Web Server (Mumbai)
```

This routing process is handled by routers using routing tables.

---

### 3. Packet Forwarding

Routers examine the destination IP address of incoming packets and forward them toward the correct destination network.

---

### 4. Path Selection

When multiple routes are available, routing protocols help determine the most efficient path based on metrics such as hop count, bandwidth, latency, or link cost.

---

### 5. Fragmentation and Reassembly

If a packet is too large for the next network segment, the Network Layer can divide it into smaller fragments.

The receiving device later reassembles the fragments into the original packet.

---

# Data Unit

The data unit used by the Network Layer is called a **Packet**.

Data flow through the OSI Model:

| Layer        | Data Unit          |
| ------------ | ------------------ |
| Application  | Data               |
| Presentation | Data               |
| Session      | Data               |
| Transport    | Segment / Datagram |
| **Network**  | **Packet**         |
| Data Link    | Frame              |
| Physical     | Bits               |

Example:

```text
+---------------------------------------------+
| IP Header | TCP Segment | Application Data |
+---------------------------------------------+
```

---

# Packet Structure

A packet consists of two major parts:

## Header

The header contains important routing information, including:

* Source IP Address
* Destination IP Address
* Protocol
* Time To Live (TTL)
* Header Checksum

---

## Payload

The payload contains the data received from the Transport Layer.

Example:

```text
+------------------------------------------------+
| Header | TCP Segment | HTTP Data |
+------------------------------------------------+
```

---

# IP Address

## What is an IP Address?

An **Internet Protocol (IP) Address** is a unique logical identifier assigned to every device connected to a network.

Unlike MAC addresses, IP addresses identify the location of a device on a network and allow routers to forward packets correctly.

Example:

```text
192.168.1.100
```

Without IP addresses, communication between different networks would not be possible.

---

## Characteristics

* Logical address
* Assigned manually or automatically
* Can change over time
* Used by routers
* Operates at Layer 3

---

## IP Address Components

An IP address contains:

* **Network Portion** – Identifies the network.
* **Host Portion** – Identifies the specific device.

Example:

```text
192.168.10.25/24
```

Network:

```text
192.168.10.0
```

Host:

```text
25
```

---

# IPv4

## What is IPv4?

IPv4 (Internet Protocol Version 4) is the most widely used version of the Internet Protocol.

It uses **32-bit addresses** divided into four octets.

Example:

```text
192.168.1.10
```

---

## IPv4 Format

```text
11000000.10101000.00000001.00001010
```

Decimal Representation:

```text
192.168.1.10
```

---

## IPv4 Address Classes

| Class | Range                       | Purpose         |
| ----- | --------------------------- | --------------- |
| A     | 1.0.0.0 – 126.255.255.255   | Large Networks  |
| B     | 128.0.0.0 – 191.255.255.255 | Medium Networks |
| C     | 192.0.0.0 – 223.255.255.255 | Small Networks  |
| D     | 224.0.0.0 – 239.255.255.255 | Multicast       |
| E     | 240.0.0.0 – 255.255.255.255 | Experimental    |

> Modern networks primarily use CIDR instead of classful addressing, but understanding classes is useful for interviews.

---

## Advantages of IPv4

* Widely supported
* Simple implementation
* Mature technology

---

## Limitations

* Limited address space (approximately 4.3 billion addresses)
* Requires NAT due to address exhaustion
* Less efficient routing compared to IPv6

---

# IPv6

## What is IPv6?

IPv6 (Internet Protocol Version 6) was developed to overcome the limitations of IPv4.

It uses **128-bit addresses**, providing an enormous number of unique addresses.

Example:

```text
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

Compressed Format:

```text
2001:db8:85a3::8a2e:370:7334
```

---

## Advantages of IPv6

* Vast address space
* Improved routing efficiency
* Built-in support for IPsec
* No need for NAT in most deployments
* Better support for modern Internet growth

---

## IPv4 vs IPv6

| Feature        | IPv4         | IPv6            |
| -------------- | ------------ | --------------- |
| Address Length | 32-bit       | 128-bit         |
| Address Format | Decimal      | Hexadecimal     |
| NAT Required   | Often        | Usually Not     |
| Address Space  | ~4.3 Billion | Extremely Large |
| Header Size    | Variable     | Fixed           |

---

# Private vs Public IP Addresses

## Private IP Address

Private IP addresses are used within internal networks and are **not routable on the public Internet**.

Reserved ranges:

| Range                         | CIDR           |
| ----------------------------- | -------------- |
| 10.0.0.0 – 10.255.255.255     | 10.0.0.0/8     |
| 172.16.0.0 – 172.31.255.255   | 172.16.0.0/12  |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 |

Example:

```text
192.168.1.25
```

---

## Public IP Address

Public IP addresses are globally unique and assigned by Internet Service Providers (ISPs).

Example:

```text
142.250.183.46
```

These addresses are reachable over the Internet.

---

## Comparison

| Private IP   | Public IP           |
| ------------ | ------------------- |
| Internal Use | Internet Accessible |
| Free to Use  | Assigned by ISP     |
| Not Routable | Globally Routable   |

---

# Subnet Mask

## What is a Subnet Mask?

A subnet mask separates the **network portion** of an IP address from the **host portion**.

Example:

IP Address:

```text
192.168.1.20
```

Subnet Mask:

```text
255.255.255.0
```

This indicates that the first three octets represent the network, while the last octet identifies the host.

---

## Common Subnet Masks

| CIDR | Subnet Mask     |
| ---- | --------------- |
| /8   | 255.0.0.0       |
| /16  | 255.255.0.0     |
| /24  | 255.255.255.0   |
| /30  | 255.255.255.252 |

---

# CIDR (Classless Inter-Domain Routing)

CIDR is a notation used to specify the network prefix length.

Example:

```text
192.168.1.0/24
```

The `/24` means that the first 24 bits represent the network portion.

Common examples:

| CIDR | Hosts (Approx.) |
| ---- | --------------- |
| /24  | 254             |
| /25  | 126             |
| /26  | 62              |
| /27  | 30              |
| /28  | 14              |
| /30  | 2               |

CIDR allows more efficient use of IP addresses than the older class-based system.

---

# Default Gateway

## What is a Default Gateway?

A **Default Gateway** is the router that forwards packets from a local network to other networks.

If a destination device is outside the local LAN, the packet is sent to the default gateway.

Example:

```text
Laptop
IP: 192.168.1.20

↓

Default Gateway

192.168.1.1

↓

Internet

↓

Web Server
```

Without a default gateway, a device can communicate only with systems on the same local network.

---

## Viewing the Default Gateway

### Windows

```cmd
ipconfig
```

Look for:

```text
Default Gateway
```

### Linux

```bash
ip route
```

Example output:

```text
default via 192.168.1.1 dev eth0
```

---

# Cybersecurity Perspective

SOC Analysts frequently use Network Layer information during investigations:

* Identifying suspicious source IP addresses
* Blocking malicious IPs on firewalls
* Investigating communication with external servers
* Detecting IP spoofing attempts
* Analyzing network traffic in Wireshark
* Reviewing firewall and router logs
* Correlating IP addresses with threat intelligence feeds

---

# Key Takeaways

* The Network Layer provides logical addressing and routing.
* The data unit is the **packet**.
* IP addresses uniquely identify devices on networks.
* IPv4 uses 32-bit addresses; IPv6 uses 128-bit addresses.
* Private IP addresses are used internally, while public IP addresses are Internet-routable.
* Subnet masks and CIDR determine the network and host portions of an IP address.
* The default gateway allows communication beyond the local network.
* Understanding Layer 3 is essential for troubleshooting, network design, and cybersecurity investigations.
---

# Routers

## What is a Router?

A **Router** is a Layer 3 networking device that connects two or more networks and forwards packets based on their destination IP addresses.

Unlike a switch, which uses MAC addresses within a LAN, a router uses **IP addresses** to determine the best path for data between networks.

### Functions of a Router

* Connects different networks
* Forwards packets
* Maintains routing tables
* Selects the best path
* Separates broadcast domains
* Performs Network Address Translation (NAT)
* Connects private networks to the Internet

### Router Example

```text
                Internet
                    │
              ISP Router
                    │
             Home Router
              /        \
      Laptop          Smartphone
```

---

# Routing

## What is Routing?

**Routing** is the process of selecting the best path for a packet to travel from the source network to the destination network.

Every router examines the destination IP address and decides where to send the packet next.

### Example

```text
Computer
   │
   ▼
Home Router
   │
   ▼
ISP Router
   │
   ▼
Core Internet Router
   │
   ▼
Destination Server
```

Each router only knows the **next hop**, not the complete journey.

---

## Routing Process

```text
Packet Arrives

↓

Read Destination IP

↓

Check Routing Table

↓

Select Best Route

↓

Forward Packet

↓

Repeat Until Destination
```

---

# Routing Table

## What is a Routing Table?

A **Routing Table** is a database stored on a router that contains information about available network routes.

It tells the router where packets should be forwarded.

### Sample Routing Table

| Destination Network | Next Hop           | Interface          |
| ------------------- | ------------------ | ------------------ |
| 192.168.1.0/24      | Directly Connected | GigabitEthernet0/1 |
| 10.0.0.0/8          | 192.168.1.254      | GigabitEthernet0/0 |
| Default Route       | ISP Gateway        | WAN                |

---

## Components

* Destination Network
* Subnet Mask
* Next Hop
* Outgoing Interface
* Metric

---

## View Routing Table

### Windows

```cmd
route print
```

### Linux

```bash
ip route
```

or

```bash
netstat -rn
```

### Cisco Router

```text
show ip route
```

---

# Static Routing

## What is Static Routing?

Static Routing is when routes are **manually configured** by the network administrator.

The router does not automatically learn new routes.

### Advantages

* Simple
* Predictable
* Low CPU usage
* More secure
* Suitable for small networks

### Disadvantages

* Manual configuration
* Difficult to maintain
* Does not adapt automatically if a link fails

### Example

```text
Network A

↓

Router A

↓

Static Route

↓

Router B

↓

Network B
```

---

# Dynamic Routing

## What is Dynamic Routing?

Dynamic Routing allows routers to exchange routing information automatically using routing protocols.

If the network changes, routers update their routing tables without manual intervention.

### Advantages

* Automatic route updates
* Better scalability
* Supports large networks
* Automatically handles failures

### Disadvantages

* Higher CPU and memory usage
* More complex configuration
* Convergence time after changes

---

## Static vs Dynamic Routing

| Static Routing               | Dynamic Routing           |
| ---------------------------- | ------------------------- |
| Manual configuration         | Automatic updates         |
| Small networks               | Large networks            |
| Lower resource usage         | Higher resource usage     |
| Does not adapt automatically | Adapts to network changes |

---

# Common Routing Protocols

## RIP (Routing Information Protocol)

### Overview

RIP is one of the oldest dynamic routing protocols.

### Characteristics

* Distance Vector protocol
* Uses Hop Count
* Maximum of 15 hops
* Simple configuration

### Advantages

* Easy to configure
* Suitable for small networks

### Limitations

* Slow convergence
* Limited scalability
* Not suitable for enterprise networks

---

## OSPF (Open Shortest Path First)

### Overview

OSPF is a modern **Link-State Routing Protocol** widely used in enterprise environments.

### Characteristics

* Uses Dijkstra's Algorithm
* Fast convergence
* Scalable
* Supports hierarchical design

### Advantages

* Faster than RIP
* Efficient route calculation
* Enterprise-ready

---

## BGP (Border Gateway Protocol)

### Overview

BGP is the routing protocol that connects different Autonomous Systems (AS) across the Internet.

It is often called the **routing protocol of the Internet**.

### Characteristics

* Path Vector protocol
* Extremely scalable
* Used by Internet Service Providers (ISPs)
* Policy-based routing

### Example

```text
Company A

↓

ISP A

↓

Internet

↓

ISP B

↓

Company B
```

---

## Routing Protocol Comparison

| Protocol | Type            | Metric         | Typical Use         |
| -------- | --------------- | -------------- | ------------------- |
| RIP      | Distance Vector | Hop Count      | Small Networks      |
| OSPF     | Link State      | Cost           | Enterprise Networks |
| BGP      | Path Vector     | Policy/AS Path | Internet Routing    |

---

# Network Address Translation (NAT)

## What is NAT?

**Network Address Translation (NAT)** converts **private IP addresses** into **public IP addresses**, allowing multiple devices to share a single public Internet connection.

### Example

Without NAT:

```text
Laptop

192.168.1.10

↓

Internet

❌ Not Routable
```

With NAT:

```text
Laptop

192.168.1.10

↓

Router

↓

Public IP

142.250.x.x

↓

Internet
```

---

## Types of NAT

### Static NAT

One private IP maps to one public IP.

### Dynamic NAT

Private IPs are mapped to available public IPs from a pool.

### PAT (Port Address Translation)

Also called **NAT Overload**.

Many private devices share one public IP using different port numbers.

PAT is the most common NAT implementation in home and office networks.

---

## Advantages of NAT

* Conserves IPv4 addresses
* Hides internal IP addresses
* Adds a basic layer of security
* Enables Internet access for private networks

---

# Internet Control Message Protocol (ICMP)

## What is ICMP?

ICMP is a Network Layer protocol used for diagnostics and error reporting.

Unlike TCP and UDP, ICMP does not transport application data.

---

## Common ICMP Messages

* Echo Request
* Echo Reply
* Destination Unreachable
* Time Exceeded
* Redirect

---

## Ping

The **ping** command uses ICMP Echo Request and Echo Reply messages to test connectivity.

### Windows

```cmd
ping google.com
```

### Linux

```bash
ping google.com
```

Successful replies indicate that the destination is reachable.

---

# Time To Live (TTL)

## What is TTL?

TTL (Time To Live) is a field in the IP header that prevents packets from circulating indefinitely due to routing loops.

Each router decreases the TTL value by **1**.

If TTL reaches **0**, the packet is discarded and an ICMP Time Exceeded message is returned.

### Example

```text
TTL = 64

↓

Router 1

TTL = 63

↓

Router 2

TTL = 62

↓

Destination
```

---

# Traceroute

Traceroute works by manipulating TTL values to identify each router along the packet's path.

### Windows

```cmd
tracert google.com
```

### Linux

```bash
traceroute google.com
```

Each hop represents a router between your device and the destination.

---

# Fragmentation

## What is Fragmentation?

Different networks support different **Maximum Transmission Units (MTUs)**.

If an IP packet is larger than the MTU of the next network, it is divided into smaller pieces called **fragments**.

The destination device reassembles the fragments into the original packet.

### Example

```text
Large Packet

↓

Fragment 1

↓

Fragment 2

↓

Fragment 3

↓

Destination

↓

Reassembled Packet
```

---

## Why Fragmentation Occurs

* Different MTU sizes
* VPN tunnels
* Legacy networks
* Mixed network technologies

---

# Packet Forwarding

Packet forwarding is the process by which a router sends a packet to the next appropriate device based on its routing table.

### Packet Forwarding Process

```text
Receive Packet

↓

Read Destination IP

↓

Search Routing Table

↓

Find Best Route

↓

Forward to Next Hop

↓

Repeat Until Destination
```

---

# Real-World Example

Suppose a user in Nagpur visits a website hosted in Hyderabad.

1. The browser creates an HTTPS request.
2. TCP creates a segment.
3. IP encapsulates the segment into a packet.
4. The home router performs NAT.
5. The packet travels through multiple ISP routers.
6. Each router consults its routing table.
7. The packet reaches the web server.
8. The response follows the reverse path back to the user.

---

# Key Takeaways

* Routers operate at **Layer 3** and forward packets using IP addresses.
* Routing determines the best path between networks.
* Routing tables store information about available routes.
* Static routing is manually configured, while dynamic routing automatically adapts to network changes.
* RIP, OSPF, and BGP are common routing protocols used in different environments.
* NAT allows private networks to communicate with the Internet.
* ICMP is used for diagnostics and error reporting.
* TTL prevents packets from looping indefinitely.
* Fragmentation allows large packets to traverse networks with smaller MTUs.
* Packet forwarding is the core function of routers and enables communication across the Internet.
---

# Network Layer Security

## Introduction

The Network Layer is one of the most targeted layers in cybersecurity because it handles IP addressing, routing, and packet forwarding. Attackers exploit Layer 3 to hide their identity, overwhelm systems, bypass security controls, or interrupt network communication.

SOC Analysts continuously monitor Network Layer activity through:

* Firewall logs
* Router logs
* IDS/IPS alerts
* SIEM dashboards
* NetFlow/sFlow data
* Packet captures (PCAP)

Understanding Layer 3 attacks enables analysts to identify malicious traffic and respond effectively.

---

# Common Network Layer Attacks

## IP Spoofing

### What is IP Spoofing?

IP Spoofing is the process of forging the **source IP address** of a packet so that it appears to come from another device.

Example:

Normal Packet

```text id="8e8rvn"
Source IP:

192.168.1.20

Destination:

8.8.8.8
```

Spoofed Packet

```text id="vtzjlwm"
Source IP:

10.0.0.50

Destination:

8.8.8.8
```

The attacker hides their real identity by pretending to be another system.

---

### Why Attackers Use IP Spoofing

* Hide their real IP address
* Launch DDoS attacks
* Bypass IP-based filtering
* Conduct reflection attacks
* Impersonate trusted hosts

---

### Detection

SOC Analysts investigate:

* Impossible source IPs
* Unexpected geographic locations
* Traffic from reserved/private IP ranges on public interfaces
* Threat intelligence matches
* Abnormal routing behavior

---

### Prevention

* Ingress Filtering
* Egress Filtering
* Anti-Spoofing Rules
* Network ACLs
* Firewalls
* Router Filtering

---

# Distributed Denial of Service (DDoS)

## What is DDoS?

A **Distributed Denial of Service (DDoS)** attack floods a target with traffic from many compromised devices, making legitimate services unavailable.

Unlike a DoS attack, which uses one system, DDoS uses thousands or even millions of devices (often a botnet).

---

## Attack Flow

```text id="mjlwm9"
Attacker

↓

Botnet

↓

Millions of Requests

↓

Victim Server

↓

Service Unavailable
```

---

## Common DDoS Types

### Volumetric Attacks

Flood the network with massive amounts of traffic.

Examples:

* UDP Flood
* ICMP Flood

---

### Protocol Attacks

Exploit weaknesses in network protocols.

Examples:

* SYN Flood
* Ping of Death

---

### Application Layer Attacks

Target web applications.

Examples:

* HTTP GET Flood
* HTTP POST Flood

---

## Indicators

* Sudden spike in bandwidth
* Thousands of connections
* High CPU usage
* Increased latency
* Service outages

---

## Mitigation

* DDoS Protection Services
* Rate Limiting
* Web Application Firewalls (WAF)
* Content Delivery Networks (CDN)
* Traffic Filtering
* Load Balancing

---

# Smurf Attack

## What is a Smurf Attack?

A Smurf Attack is a type of DDoS attack that abuses ICMP.

The attacker sends ICMP Echo Requests with a spoofed source IP address to a broadcast address.

Every host replies to the spoofed victim, overwhelming it with traffic.

---

## Attack Diagram

```text id="a4w1j7"
Attacker

↓

Spoofed Ping

↓

Broadcast Address

↓

All Devices Reply

↓

Victim
```

---

## Prevention

* Disable IP-directed broadcasts
* Configure routers securely
* Block unnecessary ICMP traffic
* Implement anti-spoofing controls

---

# ICMP Abuse

## Common Misuses

Attackers may abuse ICMP for:

* Network reconnaissance
* Host discovery
* Ping floods
* Tunneling data
* Covert communication

---

## Detection

SOC Analysts monitor:

* Excessive ICMP traffic
* ICMP packets with unusual payload sizes
* Unexpected communication patterns
* Repeated Echo Requests

---

## Prevention

* Restrict ICMP where appropriate
* Firewall filtering
* IDS/IPS signatures
* Rate limiting

---

# Network Access Control Lists (ACLs)

## What is an ACL?

An **Access Control List (ACL)** is a set of rules applied to routers or firewalls to permit or deny network traffic.

ACLs help enforce security policies by controlling which packets are allowed through the network.

---

## Types of ACLs

### Standard ACL

Filters traffic based only on the **source IP address**.

---

### Extended ACL

Filters using multiple criteria:

* Source IP
* Destination IP
* Protocol
* Port Number

---

## Example

Allow HTTPS traffic:

```text id="x1yz7t"
Permit TCP

Destination Port 443
```

Deny Telnet:

```text id="q5na0g"
Deny TCP

Destination Port 23
```

---

## Benefits

* Restricts unauthorized access
* Limits attack surface
* Improves network security
* Supports segmentation

---

# Firewalls

## What is a Firewall?

A **Firewall** is a security device or software that monitors and controls incoming and outgoing network traffic based on predefined security rules.

Firewalls are commonly deployed between trusted internal networks and untrusted external networks such as the Internet.

---

## Types of Firewalls

### Packet Filtering Firewall

Examines:

* Source IP
* Destination IP
* Protocol
* Port

---

### Stateful Firewall

Tracks active connections and permits packets that belong to established sessions.

---

### Next-Generation Firewall (NGFW)

Provides advanced capabilities such as:

* Application awareness
* Intrusion Prevention (IPS)
* Malware detection
* URL filtering
* SSL/TLS inspection
* User identity integration

---

## Firewall Example

```text id="e8l6qf"
Internet

↓

Firewall

↓

Corporate Network
```

---

# Wireshark Lab

## Objective

Capture and analyze Layer 3 traffic.

---

## Requirements

* Wireshark
* Internet connection

---

## Steps

1. Open Wireshark.
2. Select the active network interface.
3. Start capturing packets.
4. Browse a website.
5. Stop the capture.
6. Select an IPv4 packet.

Observe:

* Source IP
* Destination IP
* TTL
* Protocol
* Packet Length

---

## Useful Display Filters

Show only IPv4 packets:

```text id="8ylhn8"
ip
```

Show only ICMP traffic:

```text id="pnjlwm"
icmp
```

Show only packets to a specific IP:

```text id="t8jbwe"
ip.dst == 8.8.8.8
```

Show packets from a specific IP:

```text id="i6hvns"
ip.src == 192.168.1.20
```

---

# Useful Commands

## Windows

Display IP configuration:

```cmd id="4gmdk9"
ipconfig
```

Detailed configuration:

```cmd id="4k9swm"
ipconfig /all
```

View routing table:

```cmd id="0tjlwm"
route print
```

Test connectivity:

```cmd id="xum78o"
ping google.com
```

Trace packet path:

```cmd id="lprcmg"
tracert google.com
```

Display ARP cache:

```cmd id="dyedhz"
arp -a
```

---

## Linux

Display IP addresses:

```bash id="63r2pk"
ip addr
```

Display routing table:

```bash id="cjlwmw"
ip route
```

View neighbor table:

```bash id="yy90w9"
ip neigh
```

Ping a host:

```bash id="mjlwmn"
ping google.com
```

Trace route:

```bash id="vjlwm8"
traceroute google.com
```

---

# SOC Investigation Scenario

## Alert

```
Multiple connections detected from external IP 203.0.113.25.
```

### Investigation Steps

1. Review firewall logs.
2. Check the source IP against threat intelligence feeds.
3. Determine the destination systems.
4. Analyze traffic volume.
5. Inspect packet captures using Wireshark.
6. Correlate with IDS/IPS alerts.
7. Check for failed login attempts.
8. Block the malicious IP if confirmed.
9. Document findings and notify stakeholders.

---

## Sample Findings

* Source IP linked to a known botnet.
* Repeated SYN packets observed.
* Firewall dropped most traffic.
* IDS generated multiple alerts.
* No successful compromise detected.

---

# Interview Questions

## 1. What is the primary function of the Network Layer?

To provide logical addressing and route packets between different networks.

---

## 2. What is the data unit of the Network Layer?

Packet.

---

## 3. Which protocol operates at Layer 3?

Internet Protocol (IP).

---

## 4. What is the difference between IPv4 and IPv6?

IPv4 uses 32-bit addresses, while IPv6 uses 128-bit addresses and offers a much larger address space.

---

## 5. What is the purpose of a router?

A router forwards packets between different networks using IP addresses and routing tables.

---

## 6. What is NAT?

Network Address Translation converts private IP addresses into public IP addresses, allowing internal devices to communicate over the Internet.

---

## 7. What is ICMP used for?

Diagnostics and error reporting, such as with the `ping` command.

---

## 8. What is TTL?

Time To Live is a field in the IP header that prevents packets from looping indefinitely by decreasing at each router hop.

---

## 9. What is IP Spoofing?

Forging the source IP address in packets to impersonate another system or hide the attacker's identity.

---

## 10. How can DDoS attacks be mitigated?

Using rate limiting, firewalls, DDoS protection services, CDNs, load balancing, and traffic filtering.

---

# Hands-on Lab

## Objective

Explore Layer 3 configuration on your computer.

### Windows

1. Run:

```cmd id="dtjlwm"
ipconfig /all
```

2. Record:

* IPv4 Address
* Subnet Mask
* Default Gateway
* DNS Servers

3. Test connectivity:

```cmd id="pjlwmx"
ping 8.8.8.8
```

4. View the route:

```cmd id="3tjlwm"
tracert 8.8.8.8
```

---

### Linux

1. Display network interfaces:

```bash id="ujjlwm"
ip addr
```

2. Display routing table:

```bash id="ibjlwm"
ip route
```

3. Test connectivity:

```bash id="0jlwm0"
ping 8.8.8.8
```

4. Trace the route:

```bash id="xtjlwm"
traceroute 8.8.8.8
```

---

# Best Practices

* Use private IP addresses internally.
* Keep router firmware updated.
* Restrict unnecessary ICMP traffic.
* Implement anti-spoofing filters.
* Configure secure ACLs.
* Monitor router and firewall logs.
* Use network segmentation.
* Enable logging on critical devices.
* Regularly review routing tables and firewall rules.

---

# Key Takeaways

* The Network Layer enables communication between different networks.
* Routers forward packets based on IP addresses.
* NAT allows private networks to access the Internet.
* ICMP supports diagnostics and troubleshooting.
* ACLs and firewalls help enforce network security.
* Layer 3 attacks include IP Spoofing, DDoS, and Smurf attacks.
* SOC Analysts use router logs, firewall logs, and packet captures to investigate suspicious network activity.

---

# Summary

The Network Layer is responsible for logical addressing, routing, and packet forwarding across interconnected networks. It forms the backbone of Internet communication by enabling devices on different networks to exchange data efficiently. From a cybersecurity perspective, understanding Layer 3 is critical because many attacks exploit IP-based communication. Mastering concepts such as routing, NAT, ICMP, ACLs, and firewalls equips cybersecurity professionals to detect, analyze, and respond to network threats effectively.
