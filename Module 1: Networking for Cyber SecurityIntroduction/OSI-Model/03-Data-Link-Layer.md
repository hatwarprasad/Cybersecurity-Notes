
# Data Link Layer (Layer 2)

## Introduction

The **Data Link Layer** is the **second layer** of the **OSI (Open Systems Interconnection) Model**. It is responsible for ensuring reliable communication between devices on the **same local network (LAN)**. While the Physical Layer transmits raw bits, the Data Link Layer organizes those bits into **frames**, assigns **MAC (Media Access Control) addresses**, detects transmission errors, and controls access to the physical medium.

This layer acts as a bridge between the Physical Layer (Layer 1) and the Network Layer (Layer 3). It ensures that data sent across a local network reaches the correct destination device before it is forwarded by routers to other networks.

For Cyber Security Analysts, understanding the Data Link Layer is essential because attacks such as **ARP Spoofing**, **MAC Flooding**, and **VLAN Hopping** occur at this layer.

---

# Learning Objectives

After completing this chapter, you should be able to:

* Explain the purpose of the Data Link Layer.
* Describe how frames are created and transmitted.
* Understand MAC addresses and their importance.
* Explain the role of a Network Interface Card (NIC).
* Differentiate between the LLC and MAC sublayers.
* Describe the structure of an Ethernet frame.
* Identify common Layer 2 networking devices.
* Understand the basics of Ethernet communication.

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
| Layer 3 - Network           |
+-----------------------------+
| Layer 2 - Data Link   ← You are here
+-----------------------------+
| Layer 1 - Physical          |
+-----------------------------+
```

---

# Responsibilities of the Data Link Layer

The Data Link Layer performs several important functions:

### 1. Framing

The layer converts raw bits received from the Physical Layer into structured **frames**.

Each frame contains:

* Source MAC Address
* Destination MAC Address
* Payload (Data)
* Error Detection Information

Without framing, devices would not know where one message ends and another begins.

---

### 2. Physical Addressing

Unlike the Network Layer, which uses **IP addresses**, the Data Link Layer uses **MAC addresses** to identify devices within the same LAN.

Every network interface has a unique MAC address assigned by the manufacturer.

Example:

```text
00:1A:2B:3C:4D:5E
```

---

### 3. Error Detection

The Data Link Layer checks whether data has been corrupted during transmission.

It uses techniques such as:

* CRC (Cyclic Redundancy Check)
* Frame Check Sequence (FCS)

If an error is detected, the damaged frame is discarded.

---

### 4. Media Access Control

When multiple devices share the same network medium, the Data Link Layer determines when each device is allowed to transmit data to avoid collisions.

---

### 5. Flow Control

The Data Link Layer helps regulate the speed of data transmission between devices so that a faster sender does not overwhelm a slower receiver.

---

### 6. Reliable Delivery (on Some Technologies)

Some Layer 2 technologies provide acknowledgments and retransmissions to improve reliability within the local network.

---

# Data Unit: Frame

Each OSI layer uses a different name for the data it processes.

| Layer         | Data Unit          |
| ------------- | ------------------ |
| Application   | Data               |
| Presentation  | Data               |
| Session       | Data               |
| Transport     | Segment / Datagram |
| Network       | Packet             |
| **Data Link** | **Frame**          |
| Physical      | Bits               |

A frame is created by adding a header and trailer around the data received from the Network Layer.

### Frame Encapsulation

```text
+------------------------------------------------+
| Header | Network Packet | Trailer (FCS/CRC)    |
+------------------------------------------------+
```

The header contains addressing information, while the trailer contains error-checking information.

---

# MAC Address

## What is a MAC Address?

A **MAC (Media Access Control) Address** is a unique hardware identifier assigned to a network interface.

It identifies devices within the same local network.

Example:

```text
00:1A:2B:3C:4D:5E
```

---

## Characteristics

* 48 bits (6 bytes)
* Written in hexadecimal
* Assigned by the manufacturer
* Usually permanent (burned into hardware)
* Can be changed temporarily through software (MAC spoofing)

---

## Structure

```text
00:1A:2B : 3C:4D:5E
|------|   |-------|
 Vendor     Device ID
```

* **First 24 bits** → Organizationally Unique Identifier (OUI), identifying the manufacturer.
* **Last 24 bits** → Unique identifier assigned by that manufacturer.

---

## MAC Address vs IP Address

| MAC Address          | IP Address                   |
| -------------------- | ---------------------------- |
| Physical address     | Logical address              |
| Assigned to hardware | Assigned by DHCP or manually |
| Layer 2              | Layer 3                      |
| Used within a LAN    | Used across networks         |
| Rarely changes       | May change over time         |

---

# Network Interface Card (NIC)

A **Network Interface Card (NIC)** is the hardware component that connects a device to a network.

It enables communication using wired or wireless technologies.

Examples:

* Ethernet adapter
* Wi-Fi adapter
* USB network adapter

Every NIC has its own MAC address.

---

## Functions of a NIC

* Sends and receives frames.
* Stores the device's MAC address.
* Converts data into electrical, optical, or radio signals.
* Detects incoming frames addressed to the device.

---

## Viewing the MAC Address

### Windows

```cmd
ipconfig /all
```

Look for:

```
Physical Address
```

Example:

```
00-1A-2B-3C-4D-5E
```

---

### Linux

```bash
ip link
```

or

```bash
ip addr
```

Look for:

```
link/ether
```

---

# LLC and MAC Sublayers

The Data Link Layer is divided into two sublayers.

## 1. Logical Link Control (LLC)

Responsibilities:

* Communicates with the Network Layer.
* Identifies which Layer 3 protocol is being used (such as IPv4 or IPv6).
* Manages logical communication between devices.

Think of the LLC as the interface between networking protocols and the hardware.

---

## 2. Media Access Control (MAC)

Responsibilities:

* Controls access to the transmission medium.
* Uses MAC addresses.
* Creates Ethernet frames.
* Determines when devices can transmit.

This is the part of the Data Link Layer responsible for actual communication over the local network.

---

## LLC vs MAC

| LLC                       | MAC                       |
| ------------------------- | ------------------------- |
| Upper part of Layer 2     | Lower part of Layer 2     |
| Communicates with Layer 3 | Communicates with Layer 1 |
| Protocol identification   | Hardware addressing       |
| Logical communication     | Physical media access     |

---

# Ethernet Frame Structure

A standard Ethernet frame contains multiple fields.

```text
+---------------------------------------------------------------+
| Destination MAC | Source MAC | Type | Data | FCS (CRC) |
+---------------------------------------------------------------+
```

---

## Destination MAC

Specifies which device should receive the frame.

---

## Source MAC

Specifies which device sent the frame.

---

## EtherType

Indicates the protocol carried inside the frame.

Examples:

| Value  | Protocol |
| ------ | -------- |
| 0x0800 | IPv4     |
| 0x86DD | IPv6     |
| 0x0806 | ARP      |

---

## Payload

Contains the Network Layer packet (usually an IP packet).

---

## Frame Check Sequence (FCS)

Uses CRC to detect transmission errors.

If the calculated value does not match the received value, the frame is discarded.

---

# Data Link Layer Devices

## Switch

A switch is the primary Layer 2 networking device.

Functions:

* Learns MAC addresses.
* Builds a MAC address table.
* Forwards frames only to the intended destination.
* Reduces unnecessary traffic.
* Improves network performance.

---

## Bridge

A bridge connects two LAN segments and filters traffic based on MAC addresses.

Although largely replaced by switches, bridges introduced the concept of forwarding frames intelligently.

---

## Wireless Access Point (Layer 2 Functionality)

Wireless access points bridge wireless clients to a wired Ethernet network.

They forward Layer 2 frames between Wi-Fi devices and the wired LAN.

---

# Ethernet Basics

**Ethernet** is the most widely used LAN technology and operates primarily at the Data Link and Physical Layers.

Characteristics:

* Uses MAC addresses for communication.
* Organizes data into Ethernet frames.
* Commonly uses UTP (Cat5e/Cat6/Cat6a) or fiber-optic cables.
* Supports speeds from 10 Mbps to 400 Gbps depending on the standard.

---

## How Ethernet Communication Works

Example:

```text
Laptop
   │
   │ Ethernet Frame
   ▼
Switch
   │
   ▼
Server
```

Steps:

1. The laptop creates an Ethernet frame.
2. The frame includes the source and destination MAC addresses.
3. The switch checks its MAC address table.
4. The switch forwards the frame only to the correct destination port.
5. The server receives the frame and processes the data.

This efficient forwarding is one reason Ethernet is the dominant LAN technology.

---

# Key Takeaways

* The Data Link Layer is responsible for communication within the same local network.
* It organizes data into **frames**.
* It uses **MAC addresses** instead of IP addresses.
* Switches operate primarily at Layer 2.
* Ethernet is the most common Layer 2 technology.
* Error detection is performed using **CRC/FCS**.
* Understanding Layer 2 is essential for troubleshooting LAN issues and investigating attacks such as ARP spoofing and MAC flooding.
---

# Switching

## What is a Switch?

A **network switch** is a Layer 2 networking device that connects multiple devices within the same Local Area Network (LAN). Unlike a hub, which broadcasts data to every connected device, a switch intelligently forwards data only to the intended destination.

Switches make networks more efficient, reduce unnecessary traffic, and improve overall performance.

### How a Switch Works

A switch examines the **destination MAC address** of every incoming frame and checks its **MAC Address Table** to determine which port should receive the frame.

Example:

```text
                 Switch
        +----------------------+
Port1---|                      |---Port3
 Laptop |                      | Server
         |                      |
Port2---|                      |---Port4
Printer |                      | Desktop
        +----------------------+
```

If the destination MAC address is known, the switch forwards the frame only to that specific port.

---

# MAC Address Table

## What is a MAC Address Table?

A MAC Address Table (also called a CAM Table) is a database maintained by the switch. It maps MAC addresses to switch ports.

Example:

| MAC Address       | Port   |
| ----------------- | ------ |
| 00:11:22:33:44:55 | Port 1 |
| AA:BB:CC:DD:EE:FF | Port 2 |
| 12:34:56:78:90:AB | Port 3 |

---

## MAC Learning Process

When a frame arrives:

1. The switch records the **source MAC address**.
2. It associates the MAC address with the incoming port.
3. Future traffic destined for that MAC address is forwarded directly to that port.

Example:

Laptop sends a frame:

```text
Laptop (MAC A)
      │
      ▼
   Switch learns:
   MAC A → Port 1
```

Over time, the switch builds a complete MAC Address Table.

---

## Unknown Destination

If the destination MAC address is **not** in the MAC Address Table, the switch performs **Flooding**.

```text
Frame Received

↓

Unknown Destination

↓

Forward to all ports except incoming port
```

Once the destination replies, the switch learns its MAC address.

---

# Collision Domain

## What is a Collision?

A collision occurs when two devices transmit data at the same time on the same communication medium.

Older Ethernet networks using hubs experienced frequent collisions.

---

## Collision Domain

A Collision Domain is the portion of a network where collisions can occur.

### Hub

```text
PC1
 \
  Hub ---- PC2
 /
PC3
```

Entire network = One Collision Domain

---

### Switch

```text
PC1 ---- Switch ---- PC2
          |
          |
         PC3
```

Each switch port creates a separate Collision Domain.

Advantages:

* Better performance
* Faster communication
* Fewer retransmissions

---

# Broadcast Domain

## What is a Broadcast?

A broadcast is a frame sent to **every device** on the local network.

Example:

A computer sends an ARP Request.

Every device on the LAN receives it.

---

## Broadcast Domain

A Broadcast Domain is the group of devices that receive broadcast traffic.

Example:

```text
        Switch

PC1  PC2  PC3  PC4
```

All four computers belong to the same Broadcast Domain.

---

## How Routers Affect Broadcast Domains

Routers do **not** forward Layer 2 broadcasts.

Example:

```text
LAN 1

PC1
 |
Router
 |
PC2

LAN 2
```

Broadcast traffic from LAN 1 stops at the router.

Therefore:

* One router separates Broadcast Domains.

---

# Collision Domain vs Broadcast Domain

| Feature   | Collision Domain           | Broadcast Domain            |
| --------- | -------------------------- | --------------------------- |
| Caused by | Simultaneous transmissions | Broadcast traffic           |
| Hub       | One domain                 | One domain                  |
| Switch    | One per port               | One large domain            |
| Router    | Not affected               | Separates broadcast domains |

---

# VLAN (Virtual Local Area Network)

## What is a VLAN?

A VLAN is a logical segmentation of a physical network.

Instead of placing all devices in one LAN, VLANs divide the network into multiple isolated broadcast domains.

Example:

```text
Switch

VLAN 10

HR PCs

--------------------

VLAN 20

Finance PCs

--------------------

VLAN 30

IT PCs
```

Although all devices connect to the same physical switch, they behave as if they are on separate networks.

---

## Benefits of VLANs

* Better security
* Reduced broadcast traffic
* Easier network management
* Department isolation
* Improved performance

---

## Example

Without VLANs

```text
All users

↓

Same Broadcast Domain
```

With VLANs

```text
HR

↓

Separate VLAN

Finance

↓

Separate VLAN

IT

↓

Separate VLAN
```

Departments cannot communicate directly unless routing is configured.

---

# VLAN IDs

Common VLAN range:

| VLAN ID   | Description    |
| --------- | -------------- |
| 1         | Default VLAN   |
| 2–1001    | Normal Range   |
| 1006–4094 | Extended Range |

---

# ARP Relationship

Although ARP (Address Resolution Protocol) is discussed separately, it works closely with the Data Link Layer.

Example:

Computer wants to send data to:

```text
192.168.1.20
```

The computer knows the IP address but does **not** know the destination MAC address.

Process:

```text
IP Address

↓

ARP Request

↓

Who has 192.168.1.20?

↓

Destination replies

↓

MAC Address learned

↓

Ethernet Frame created
```

Without ARP, Ethernet communication inside a LAN would not be possible.

---

# Error Detection (CRC)

## What is CRC?

CRC (Cyclic Redundancy Check) is an error detection mechanism used by Ethernet.

The sender calculates a mathematical value based on the frame contents.

That value is stored inside the **Frame Check Sequence (FCS)**.

---

## Receiving Process

Receiver calculates CRC again.

If:

```text
Calculated CRC

=

Received CRC
```

Frame is accepted.

If:

```text
Calculated CRC

≠

Received CRC
```

Frame is discarded.

---

## Why CRC is Important

CRC helps detect:

* Damaged cables
* Electrical interference
* Corrupted frames
* Transmission errors

---

# Duplex Modes

## Half Duplex

Communication occurs in **both directions**, but **not simultaneously**.

Example:

Walkie-Talkie

```text
Person A

↓

Talks

↓

Person B

↓

Replies
```

Characteristics:

* One device transmits at a time
* More collisions
* Lower performance

---

## Full Duplex

Both devices transmit and receive simultaneously.

Example:

Telephone Call

```text
Person A ↔ Person B
```

Characteristics:

* No collisions
* Faster communication
* Used by modern switches

---

## Comparison

| Half Duplex             | Full Duplex                    |
| ----------------------- | ------------------------------ |
| One direction at a time | Both directions simultaneously |
| More collisions         | No collisions                  |
| Slower                  | Faster                         |
| Older Ethernet          | Modern Ethernet                |

---

# Cybersecurity Relevance

The Data Link Layer plays an important role in enterprise security.

SOC Analysts frequently investigate incidents related to Layer 2 communication.

Examples include:

### Unauthorized Devices

An attacker connects an unknown laptop to an office switch.

Indicators:

* New MAC address
* New switch port activity
* NAC alerts

---

### Rogue Switch

An attacker installs a personal switch.

Risks:

* Unauthorized access
* Packet sniffing
* Network expansion

---

### Rogue Access Point

An employee installs an unauthorized Wi-Fi router.

Risks:

* Bypasses corporate security
* Weak encryption
* Easy attacker access

---

### MAC Spoofing

Attackers change their MAC address to impersonate another device.

Used for:

* Bypassing MAC filtering
* Avoiding detection
* Impersonating trusted devices

---

### SOC Investigation Example

Alert:

```text
Unknown MAC Address detected
```

Analyst investigates:

* Switch logs
* Port number
* Connected user
* Device inventory
* DHCP logs
* NAC alerts

Containment:

* Disable switch port
* Isolate device
* Notify IT team
* Investigate user activity

---

# Key Takeaways

* Switches use MAC addresses to forward frames efficiently.
* MAC Address Tables help switches learn device locations.
* Each switch port forms a separate Collision Domain.
* Routers separate Broadcast Domains.
* VLANs improve security by isolating departments.
* ARP resolves IP addresses to MAC addresses.
* CRC detects corrupted Ethernet frames.
* Full Duplex communication eliminates collisions.
* Understanding Layer 2 is essential for SOC Analysts investigating local network attacks.
---

# Layer 2 Security Attacks

Although the Data Link Layer is responsible for local network communication, it is also a common target for attackers. Many enterprise attacks begin inside a Local Area Network (LAN), making Layer 2 security an important responsibility for Network Engineers and SOC Analysts.

Common Layer 2 attacks include:

* MAC Flooding
* ARP Spoofing
* VLAN Hopping
* MAC Spoofing
* Rogue DHCP Server
* STP Manipulation

Understanding these attacks helps analysts identify suspicious network behavior and implement appropriate security controls.

---

# MAC Flooding Attack

## What is MAC Flooding?

A **MAC Flooding Attack** is a technique where an attacker overwhelms a switch by sending thousands of fake MAC addresses.

The switch stores these fake entries in its MAC Address Table until the table becomes full.

Once full, the switch behaves like a hub and forwards traffic to all ports.

---

## Attack Process

```text
Attacker

↓

Generates Thousands of Fake MAC Addresses

↓

Switch MAC Table Becomes Full

↓

Unknown Frames Are Flooded

↓

Attacker Captures Other Users' Traffic
```

---

## Impact

* Network congestion
* Packet sniffing
* Data theft
* Loss of confidentiality

---

## Prevention

* Port Security
* Dynamic ARP Inspection (DAI)
* 802.1X Authentication
* MAC Address Limits
* Network Access Control (NAC)

---

# ARP Spoofing (ARP Poisoning)

## What is ARP?

ARP (Address Resolution Protocol) maps an IP address to a MAC address within the same local network.

Example:

```text
192.168.1.10

↓

Who has 192.168.1.20?

↓

MAC Address Returned
```

---

## What is ARP Spoofing?

An attacker sends fake ARP replies to convince devices that the attacker's MAC address belongs to another device (often the default gateway).

This redirects network traffic through the attacker's system.

---

## Attack Diagram

```text
Victim

↓

Fake ARP Reply

↓

Attacker

↓

Router
```

Instead of sending traffic directly to the router, the victim unknowingly sends it to the attacker.

---

## Risks

* Man-in-the-Middle (MITM)
* Credential theft
* Session hijacking
* Data modification
* Network monitoring

---

## Detection

SOC Analysts investigate:

* Duplicate MAC addresses
* Unexpected ARP replies
* Frequent ARP broadcasts
* Firewall alerts
* IDS/IPS notifications

---

## Prevention

* Dynamic ARP Inspection
* Static ARP entries (critical systems)
* Port Security
* VLAN segmentation
* Network monitoring

---

# VLAN Hopping Attack

## What is VLAN Hopping?

VLAN Hopping is an attack where an attacker gains access to traffic from another VLAN.

Normally:

```text
HR VLAN

↓

Cannot Access

↓

Finance VLAN
```

After VLAN Hopping:

```text
HR VLAN

↓

Attacker

↓

Finance VLAN
```

---

## Attack Methods

### Switch Spoofing

The attacker pretends to be another switch.

### Double Tagging

The attacker inserts two VLAN tags into a frame to bypass VLAN separation.

---

## Prevention

* Disable unused ports
* Disable Dynamic Trunking Protocol (DTP)
* Use dedicated native VLANs
* Restrict trunk ports
* Configure allowed VLAN lists

---

# MAC Spoofing

## What is MAC Spoofing?

MAC Spoofing is the process of changing a device's MAC address to impersonate another device.

Example:

Original:

```text
00:11:22:33:44:55
```

Spoofed:

```text
AA:BB:CC:DD:EE:FF
```

---

## Why Attackers Use MAC Spoofing

* Bypass MAC filtering
* Impersonate trusted devices
* Hide identity
* Evade simple access controls

---

## Detection

* Duplicate MAC addresses
* Unexpected MAC changes
* Switch log analysis
* NAC alerts

---

# Rogue DHCP Server

## What is a Rogue DHCP Server?

A Rogue DHCP Server is an unauthorized DHCP server connected to a network.

Instead of the legitimate DHCP server assigning IP addresses, the attacker's server responds first.

---

## Risks

* Incorrect gateway
* Malicious DNS server
* Traffic interception
* Man-in-the-Middle attacks

---

## Prevention

* DHCP Snooping
* Switch Port Security
* Network Access Control
* Monitor unauthorized devices

---

# Port Security

## What is Port Security?

Port Security is a switch feature that restricts which devices can connect to a switch port.

Administrators can:

* Allow only specific MAC addresses
* Limit the number of devices
* Disable ports after violations

---

## Example

Only one approved device is allowed.

```text
Port 1

↓

Allowed MAC

↓

00:11:22:33:44:55
```

If another MAC address appears:

```text
Violation

↓

Port Shutdown
```

---

## Benefits

* Prevents unauthorized devices
* Reduces MAC Flooding attacks
* Improves physical network security

---

# Spanning Tree Protocol (STP)

## What is STP?

Spanning Tree Protocol (STP) prevents network loops in Ethernet networks.

Without STP:

```text
Switch A

↔

Switch B

↔

Switch C

↔

Switch A
```

Frames continue circulating indefinitely.

---

## Problems Caused by Loops

* Broadcast storms
* Duplicate frames
* MAC table instability
* Network outages

---

## How STP Works

STP:

1. Elects a Root Bridge.
2. Calculates the best path.
3. Blocks redundant links.
4. Re-enables links if a primary path fails.

---

## Advantages

* Prevents loops
* Improves network stability
* Provides redundancy

---

# Layer 2 Troubleshooting

Common issues:

* Incorrect VLAN assignment
* Faulty switch ports
* Duplex mismatch
* MAC address conflicts
* STP blocking ports
* Excessive broadcasts
* Physical cable problems

---

## Troubleshooting Steps

### Step 1

Check cable connections.

---

### Step 2

Verify switch port status.

---

### Step 3

Check VLAN membership.

---

### Step 4

Review MAC Address Table.

---

### Step 5

Inspect ARP cache.

Windows:

```cmd
arp -a
```

Linux:

```bash
ip neigh
```

---

### Step 6

Check interface statistics.

Linux:

```bash
ip -s link
```

Cisco Switch:

```text
show mac address-table

show interfaces

show vlan brief
```

---

# Wireshark Lab

## Objective

Capture and analyze Ethernet frames.

---

## Requirements

* Wireshark
* Two networked devices
* Internet connection

---

## Steps

1. Open Wireshark.
2. Select your network interface.
3. Start packet capture.
4. Open a website.
5. Stop the capture.
6. Select an Ethernet frame.

Observe:

* Source MAC Address
* Destination MAC Address
* EtherType
* Frame Length
* Payload

---

## Display Filters

Show only ARP traffic:

```text
arp
```

Show only Ethernet frames:

```text
eth
```

Show broadcast frames:

```text
eth.dst == ff:ff:ff:ff:ff:ff
```

---

# SOC Investigation Scenario

### Alert

"Multiple ARP replies detected from a single host."

### Investigation

1. Check ARP traffic in Wireshark.
2. Identify the suspicious MAC address.
3. Compare with the asset inventory.
4. Review switch logs.
5. Determine affected systems.
6. Isolate the compromised device.
7. Block the switch port.
8. Reset affected credentials if necessary.

---

# Interview Questions

## 1. What is the primary responsibility of the Data Link Layer?

To provide reliable communication between devices on the same LAN using frames and MAC addresses.

---

## 2. What is the data unit of Layer 2?

Frame.

---

## 3. What address does Layer 2 use?

MAC Address.

---

## 4. Which device operates at Layer 2?

Switch.

---

## 5. What is the purpose of a MAC Address Table?

To map MAC addresses to switch ports and forward frames efficiently.

---

## 6. What is the difference between a hub and a switch?

A hub broadcasts traffic to all ports, while a switch forwards frames only to the destination port using MAC addresses.

---

## 7. What is ARP Spoofing?

An attack where false ARP messages associate the attacker's MAC address with another device's IP address, enabling traffic interception.

---

## 8. How can MAC Flooding be prevented?

By enabling Port Security, limiting MAC addresses per port, and monitoring switch activity.

---

## 9. What is the purpose of STP?

To prevent switching loops and broadcast storms by blocking redundant paths.

---

## 10. Why are VLANs used?

To logically separate networks, improve security, reduce broadcast traffic, and simplify management.

---

# Hands-on Lab

## Objective

Explore Layer 2 information on your own computer.

### Windows

Display the ARP cache:

```cmd
arp -a
```

Display network adapter details:

```cmd
ipconfig /all
```

---

### Linux

View network interfaces:

```bash
ip addr
```

Display neighbor (ARP) table:

```bash
ip neigh
```

View interface statistics:

```bash
ip -s link
```

---

## Exercise

1. Record your MAC address.
2. Identify your default gateway.
3. View the ARP cache before browsing.
4. Open a website.
5. View the ARP cache again.
6. Compare the entries and note any changes.

---

# Key Takeaways

* The Data Link Layer provides communication within the same LAN.
* It uses **frames** and **MAC addresses**.
* Switches forward traffic using MAC Address Tables.
* VLANs improve security through logical segmentation.
* CRC helps detect transmission errors.
* STP prevents network loops.
* Port Security restricts unauthorized devices.
* SOC Analysts investigate Layer 2 attacks such as ARP Spoofing, MAC Flooding, and VLAN Hopping.

---

# Summary

The Data Link Layer is responsible for reliable local network communication. It organizes data into frames, uses MAC addresses to identify devices, and ensures efficient frame forwarding through switches. Understanding Layer 2 technologies and attacks is essential for cybersecurity professionals because many internal network threats originate here. Mastering concepts such as Ethernet, switching, VLANs, ARP, STP, and Port Security enables SOC Analysts to troubleshoot connectivity issues, detect malicious activity, and strengthen enterprise network security.
