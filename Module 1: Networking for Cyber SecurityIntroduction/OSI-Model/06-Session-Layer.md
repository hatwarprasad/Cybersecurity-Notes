
# Session Layer (Layer 5)

## Introduction

The **Session Layer** is the **fifth layer** of the **OSI (Open Systems Interconnection) Model**. It is responsible for **establishing, managing, synchronizing, and terminating communication sessions** between applications running on different devices.

A **session** is a logical conversation between two applications. The Session Layer ensures that this conversation starts correctly, remains active while data is exchanged, and closes properly when communication is complete.

Unlike the Transport Layer, which focuses on reliable data delivery, the Session Layer focuses on **managing the communication itself**.

---

# Learning Objectives

After completing this chapter, you should be able to:

* Explain the purpose of the Session Layer.
* Understand what a session is.
* Describe session establishment, maintenance, and termination.
* Explain synchronization using checkpoints.
* Identify protocols associated with the Session Layer.
* Understand common session-based attacks.
* Apply Session Layer concepts during cybersecurity investigations.

---

# Position in the OSI Model

```text
+-----------------------------+
| Layer 7 - Application       |
+-----------------------------+
| Layer 6 - Presentation      |
+-----------------------------+
| Layer 5 - Session  ← You are here
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

# Responsibilities of the Session Layer

The Session Layer performs several important functions.

## 1. Session Establishment

Before two applications exchange information, a communication session must be established.

Example:

```text
Client

↓

Login Request

↓

Server

↓

Session Created
```

---

## 2. Session Maintenance

While communication continues, the Session Layer keeps the session active.

Responsibilities include:

* Maintaining communication state
* Monitoring activity
* Handling interruptions
* Supporting multiple sessions

---

## 3. Session Termination

After communication is complete, the session is closed properly.

Example:

```text
Client

↓

Logout

↓

Server

↓

Session Closed
```

---

## 4. Synchronization

The Session Layer inserts **checkpoints** into long data transfers.

If communication fails, transmission resumes from the last checkpoint instead of starting over.

Example:

```text
File Transfer

25%

↓

Checkpoint

↓

50%

↓

Checkpoint

↓

75%

↓

Checkpoint

↓

100%
```

If the connection drops at 80%, the transfer can resume from the 75% checkpoint.

---

## 5. Dialog Control

The Session Layer determines how two devices communicate.

### Half Duplex

Only one device transmits at a time.

Example:

```text
Walkie-Talkie

Person A

↓

Person B

↓

Person A
```

---

### Full Duplex

Both devices communicate simultaneously.

Example:

```text
Phone Call

Person A ↔ Person B
```

---

# What is a Session?

A **session** is a logical connection between two applications.

Examples include:

* Logging into a website
* Connecting to an SSH server
* Joining a Microsoft Teams meeting
* Opening an online banking portal
* Starting a Remote Desktop session

The session begins when authentication is successful and ends when the user logs out or the connection times out.

---

# Session Lifecycle

```text
User Starts Application

↓

Authentication

↓

Session Created

↓

Data Exchange

↓

Session Maintained

↓

Logout / Timeout

↓

Session Destroyed
```

---

# Session Identification

Most modern applications identify sessions using one or more of the following:

* Session IDs
* Authentication Tokens
* Cookies
* JSON Web Tokens (JWT)
* API Tokens

Example:

```text
User Login

↓

Server Generates Session ID

↓

Session ID Stored in Browser Cookie

↓

Browser Sends Session ID with Every Request
```

---

# Checkpoints

Checkpoints allow long-running communications to recover after interruptions.

Example:

A 5 GB backup is being transferred.

```text
0%

↓

20%

↓

Checkpoint

↓

40%

↓

Checkpoint

↓

60%

↓

Connection Lost
```

Instead of restarting, the transfer resumes from the 40% checkpoint.

---

# Session Layer Protocols

Although the modern Internet does not always map protocols directly to OSI layers, several protocols and technologies perform Session Layer functions.

Examples include:

| Protocol                    | Purpose                               |
| --------------------------- | ------------------------------------- |
| NetBIOS                     | Session management                    |
| RPC (Remote Procedure Call) | Remote communication                  |
| SMB Session Service         | File sharing sessions                 |
| SIP                         | Voice and video session establishment |
| PPTP                        | VPN session management                |

---

# Real-World Examples

## Online Banking

```text
User Login

↓

Authentication

↓

Session Created

↓

View Balance

↓

Transfer Money

↓

Logout

↓

Session Closed
```

---

## SSH Connection

```text
SSH Client

↓

Authentication

↓

Secure Session

↓

Run Commands

↓

Disconnect
```

---

## Video Conference

```text
Join Meeting

↓

Session Created

↓

Audio

↓

Video

↓

Chat

↓

Leave Meeting

↓

Session Closed
```

---

# Cybersecurity Perspective

SOC Analysts investigate many issues related to sessions.

Common examples include:

* Session Hijacking
* Session Fixation
* Invalid Session Tokens
* Repeated Login Sessions
* Expired Sessions
* Concurrent Sessions
* Unauthorized Remote Sessions

Logs commonly reviewed include:

* Authentication logs
* VPN logs
* Web server logs
* Identity provider logs
* Application logs

---

# Why the Session Layer Matters

Without session management:

* Users would need to authenticate for every request.
* File transfers could not resume after interruptions.
* Remote desktop sessions would be unreliable.
* Video calls would disconnect frequently.
* Web applications could not maintain user login states.

---

# Key Takeaways

* The Session Layer establishes, manages, synchronizes, and terminates communication sessions.
* It supports authentication continuity through session identifiers.
* Checkpoints improve reliability during long transfers.
* Dialog control determines whether communication is half duplex or full duplex.
* Understanding session management is essential for investigating authentication-related incidents and web application security.
