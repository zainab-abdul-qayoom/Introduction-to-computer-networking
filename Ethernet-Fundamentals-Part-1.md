# Ethernet Fundamentals (Part 1): Standards and Addressing

## 1. What is Ethernet?

**Ethernet** is the most commonly used technology for **Local Area Networks (LANs)**.

It allows devices such as:

* Computers
* Laptops
* Servers
* Printers
* Switches

to communicate with each other over a network.

Ethernet works at:

* **Layer 2: Data Link Layer**
* **Layer 1: Physical Layer**

---

## 2. Two Layers Used by Ethernet

### Data Link Layer

The Data Link Layer is responsible for transferring data between directly connected network devices.

It also provides:

* MAC addressing
* Ethernet frames
* Error detection

### Physical Layer

The Physical Layer deals with the actual transmission of signals.

It defines things such as:

* Electrical signals
* Optical signals
* Cables
* Transmission speed
* Physical connections

### Easy way to remember

> **Data Link = Frames + MAC addresses**

> **Physical = Cables/signals + transmission**

---

# 3. Why is Ethernet Important?

Ethernet became the dominant LAN technology because it:

* Can provide high performance
* Can continuously evolve to higher speeds
* Maintains backward compatibility
* Works for many different types of networks

Ethernet is used in:

* Home networks
* Office/corporate networks
* Data centers
* LANs

---

# 4. History of Ethernet

Ethernet was introduced in the **1970s**.

It was developed by a team led by:

**Robert Metcalfe**

at:

**Xerox Palo Alto Research Center (PARC)**

In the **mid-1980s**, the **IEEE** published the formal Ethernet standard:

> **IEEE 802.3**

### IEEE 802.3

IEEE 802.3 defines rules for Ethernet networks, including how network devices communicate and interact.

Because manufacturers follow the same standard, equipment from different vendors can communicate with each other.

### Ethernet Speed Evolution

Ethernet originally supported:

> **10 Mbps**

Then it increased to:

> **100 Mbps**

Modern Ethernet can support speeds up to:

> **400 Gbps**

---

# 5. Ethernet Frames

Devices connected to the same LAN communicate by sending **Ethernet frames**.

An Ethernet frame contains information that helps the network deliver the data to the correct device.

Every Ethernet frame contains:

* Source MAC address
* Destination MAC address
* Type
* Payload
* FCS

---

# 6. MAC Address

**MAC** stands for:

> **Media Access Control**

A MAC address is a unique address used to identify a network interface on a local Ethernet network.

Think of it as the **local network identity of a network interface**.

Example:

```text
00:1A:2B:3C:4D:5E
```

A MAC address is:

> **48 bits long**

It is represented using:

> **12 hexadecimal digits**

---

# 7. MAC Address Structure

A MAC address has two main parts:

```text
00:1A:2B : 3C:4D:5E
<------>   <------->
   OUI     Serial Number
```

### First 6 hexadecimal digits

These form the:

> **OUI (Organizationally Unique Identifier)**

The OUI identifies the organization/vendor.

### Last 6 hexadecimal digits

These are assigned by the vendor to identify the particular network interface.

Therefore:

> **OUI + unique vendor-assigned number = unique MAC address**

---

# 8. Who Assigns the OUI?

Ethernet vendors register with:

> **IEEE (Institute of Electrical and Electronics Engineers)**

IEEE assigns the vendor an:

> **OUI (Organizationally Unique Identifier)**

This helps make MAC addresses globally unique.

---

# 9. NIC

**NIC** stands for:

> **Network Interface Card**

A NIC is the hardware that connects a device to a network.

For example, your computer may have:

* Ethernet NIC
* Wi-Fi NIC

The NIC allows a device to communicate through a network.

### NIC works with two layers

**Physical Layer:**

* Provides access to the physical network medium.

**Data Link Layer:**

* Provides MAC addressing.

So remember:

> **NIC connects the device to the network.**

---

# 10. Finding a MAC Address

### Windows

Use:

```text
ipconfig
```

### Linux

Use:

```text
ifconfig
```

A MAC address may appear like:

```text
00-1A-2B-3C-4D-5E
```

or:

```text
00:1A:2B:3C:4D:5E
```

Both represent the same type of 48-bit MAC address.

---

# 11. Ethernet Frame Structure

An Ethernet frame contains:

```text
+------------------------+
| Destination MAC        |
+------------------------+
| Source MAC             |
+------------------------+
| Type / EtherType       |
+------------------------+
| Payload                |
+------------------------+
| FCS                    |
+------------------------+
```

The frame consists of a:

> **Layer 2 header + payload + trailer**

---

# 12. Destination MAC Address

The **Destination MAC Address** tells us:

> Which device should receive the frame?

Example:

```text
Destination MAC:
AA:BB:CC:DD:EE:FF
```

The Ethernet network uses this address when forwarding the frame.

---

# 13. Source MAC Address

The **Source MAC Address** tells us:

> Which device sent the frame?

Example:

```text
Source MAC:
11:22:33:44:55:66
```

So:

> **Source = Sender**

> **Destination = Receiver**

---

# 14. Type / EtherType

The **Type field**, also called **EtherType**, tells the receiving device what type of upper-layer protocol is contained inside the Ethernet frame.

For example, it can indicate:

> **IPv4**

So the Ethernet frame can carry an IP packet as its payload.

---

# 15. Payload

The **payload** is the actual data received from the upper layer.

In simple words:

> **Payload = The data being carried**

For example:

```text
Application Data
       ↓
TCP/UDP
       ↓
IP Packet
       ↓
Ethernet Frame
```

The Ethernet frame carries the IP packet as its payload.

---

# 16. FCS

**FCS** stands for:

> **Frame Check Sequence**

FCS is placed at the end of an Ethernet frame.

Its purpose is:

> **To detect corrupted frames.**

If a frame is corrupted during transmission, the receiving device can detect the error using the FCS.

Generally:

> Corrupted Ethernet frames are discarded.

Ethernet itself normally does **not retransmit** the corrupted frame.

Retransmission can be handled by an upper-layer protocol such as:

> **TCP**

---

# 17. Ethernet Frame Size

A standard Ethernet frame has:

### Header

```text
14 bytes
```

### Payload

```text
46 to 1500 bytes
```

### FCS/Trailer

```text
4 bytes
```

Therefore:

### Minimum frame size

```text
14 + 46 + 4 = 64 bytes
```

### Maximum standard frame size

```text
14 + 1500 + 4 = 1518 bytes
```

So remember:

> **Standard Ethernet frame = 64 to 1518 bytes**

---

# 18. MTU

**MTU** stands for:

> **Maximum Transmission Unit**

For standard Ethernet:

> **MTU = 1500 bytes**

Here, MTU refers to the maximum size of the **payload** that can normally be carried in an Ethernet frame.

Remember:

```text
Maximum Payload = 1500 bytes
Maximum Frame = 1518 bytes
```

Do not confuse these two.

---

# 19. Jumbo Frames

A frame with a payload larger than:

> **1500 bytes**

is called a:

> **Jumbo Frame**

Jumbo frames are supported by some vendors, but they are **not part of the standard Ethernet frame size** described here.

---

# 20. RUNT / Collision Fragment

If an Ethernet frame is smaller than:

> **64 bytes**

it is considered a:

> **RUNT** or **Collision Fragment**

The receiving device automatically discards it.

Remember:

```text
< 64 bytes → RUNT → Discarded
64–1518 bytes → Standard Ethernet frame
> 1518 bytes → May be a jumbo frame if supported
```

---

# 21. Important Numbers to Remember

| Concept                         |                 Value |
| ------------------------------- | --------------------: |
| Ethernet standard               |            IEEE 802.3 |
| MAC address                     |               48 bits |
| MAC address                     | 12 hexadecimal digits |
| OUI                             |    First 6 hex digits |
| Vendor/serial part              |     Last 6 hex digits |
| Ethernet header                 |              14 bytes |
| Minimum payload                 |              46 bytes |
| Maximum payload / MTU           |            1500 bytes |
| FCS                             |               4 bytes |
| Minimum Ethernet frame          |              64 bytes |
| Maximum standard Ethernet frame |            1518 bytes |
| RUNT                            |    Less than 64 bytes |

---

# 22. Ethernet Frame: Easy Visualization

Think of an Ethernet frame like a **parcel**:

```text
+-------------------+
| Destination       | ← Who receives it?
| MAC               |
+-------------------+
| Source MAC        | ← Who sent it?
+-------------------+
| Type              | ← What is inside?
+-------------------+
| Payload           | ← Actual data
+-------------------+
| FCS               | ← Error checking
+-------------------+
```

---

# 23. Big Picture

When a computer sends data:

```text
Application
     ↓
TCP / UDP
     ↓
IP
     ↓
Ethernet
     ↓
Physical Medium
```

Ethernet takes the network-layer packet and puts it inside an **Ethernet frame**.

The frame contains:

```text
Destination MAC
Source MAC
Type
Payload
FCS
```

---

# 24. Key Differences: IP vs MAC

| IP Address                        | MAC Address                           |
| --------------------------------- | ------------------------------------- |
| Layer 3                           | Layer 2                               |
| Used by IP                        | Used by Ethernet                      |
| Logical address                   | Hardware/network-interface address    |
| Used for routing between networks | Used for local Ethernet communication |
| IPv4 = 32 bits                    | 48 bits                               |
| Example: `192.168.1.10`           | Example: `00:1A:2B:3C:4D:5E`          |

### Easy memory trick

> **IP = Where the device is on the network**

> **MAC = Which network interface it is**

---

# 25. Key Takeaways

* Ethernet is the most common **LAN technology**.
* Ethernet operates at **OSI Layer 1 and Layer 2**.
* Ethernet is standardized by **IEEE 802.3**.
* Ethernet uses **MAC addresses** to identify network interfaces.
* A MAC address is **48 bits / 12 hexadecimal digits**.
* The first 6 hexadecimal digits are the **OUI**.
* A NIC connects a device to the network.
* Ethernet carries data using **frames**.
* An Ethernet frame has a **Destination MAC, Source MAC, Type, Payload, and FCS**.
* FCS is used to detect corrupted frames.
* Standard Ethernet payload is **46 to 1500 bytes**.
* Standard Ethernet frame size is **64 to 1518 bytes**.
* **MTU = 1500 bytes** for standard Ethernet.
* Frames smaller than 64 bytes are called **RUNT/collision fragments** and are discarded.
* Frames larger than 1500-byte payload may be **jumbo frames** if supported.
* Ethernet normally does not retransmit corrupted frames. Upper-layer protocols such as **TCP** can provide retransmission.
* Ethernet allows devices from different vendors to communicate because they follow common standards.

---

## Quick Revision

```text
Ethernet
   ↓
Layer 1 + Layer 2
   ↓
IEEE 802.3
   ↓
Uses MAC addresses
   ↓
MAC = 48 bits
   ↓
Ethernet sends Frames
   ↓
Frame:
Destination MAC
Source MAC
Type
Payload
FCS
   ↓
Payload = 46–1500 bytes
   ↓
Frame = 64–1518 bytes
   ↓
MTU = 1500 bytes
```
