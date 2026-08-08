# TCP/IP Protocol Suite: Transport Layer

## What is the Transport Layer?

The **Transport Layer** provides communication between the **source application and destination application**.

Its main jobs include:

* Reliable data transfer
* Error checking
* Flow control
* Managing communication between applications

The two main transport protocols are:

**TCP** and **UDP**

## TCP

**TCP = Transmission Control Protocol**

TCP is **reliable** and **connection-oriented**.

It:

* Makes a connection before sending data
* Checks for lost or damaged data
* Uses **sequence numbers** to keep data in order
* Uses **acknowledgements (ACKs)** to confirm data was received
* Can retransmit lost data
* Uses flow control so a fast sender does not overwhelm a slow receiver

### Three-Way Handshake

Before TCP sends data, it establishes a connection:

`Client → SYN → Server`

`Client ← SYN-ACK ← Server`

`Client → ACK → Server`

After this, data can be transferred.

## UDP

**UDP = User Datagram Protocol**

UDP is **fast and lightweight**, but it does not provide the reliability features of TCP.

UDP:

* Does not establish a connection first
* Does not retransmit lost data
* Does not guarantee order
* Has less overhead

UDP is useful for **real-time applications**, such as:

* Voice
* Video
* Live communication

### TCP vs UDP

| TCP                   | UDP                  |
| --------------------- | -------------------- |
| Reliable              | Less reliable        |
| Connection-oriented   | Connectionless       |
| Slower                | Faster               |
| Retransmits lost data | Does not retransmit  |
| Keeps data in order   | Order not guaranteed |
| More overhead         | Less overhead        |

## Port Numbers

TCP and UDP use **port numbers** to identify which application/service should receive the data.

Example:

`Server → Port 80 → HTTP`

**HTTP uses port 80.**

Port numbers range from **1 to 65,535**. Ports **0 to 1023** are called **well-known ports**.

## ⭐ Remember

* **Transport Layer → application-to-application communication**
* **TCP → reliable**
* **UDP → fast and lightweight**
* **TCP uses sequence numbers and ACKs**
* **TCP uses a three-way handshake**
* **Port number → identifies the application/service**
* **HTTP → port 80**
