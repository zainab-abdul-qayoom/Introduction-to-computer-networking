# Ethernet Fundamentals: Standards and Addressing

## What is Ethernet?

**Ethernet** is a networking technology mainly used to connect devices in a **LAN (Local Area Network)**.

Ethernet operates at two layers of the OSI model:

- **Layer 1 → Physical Layer**
- **Layer 2 → Data Link Layer**

Ethernet allows devices on the same LAN to communicate by sending **Ethernet frames**.

## Ethernet Standard

Ethernet was introduced in the **1970s** by a team led by **Robert Metcalfe** at Xerox PARC.

In the **mid-1980s**, the IEEE published the formal Ethernet standard:

**IEEE 802.3**

The IEEE 802.3 standard defines rules for:

- Configuring Ethernet networks
- How Ethernet devices communicate
- How different vendors' networking equipment can work together

## Ethernet Speed

Ethernet has evolved over time to provide higher speeds.

Some important speeds are:

- Original Ethernet → **10 Mbps**
- Later Ethernet → **100 Mbps**
- Modern Ethernet → up to **400 Gbps**

Ethernet maintains backward compatibility while supporting higher performance.

## Ethernet and the OSI Model

Ethernet operates at:

- **Layer 1 → Physical Layer**
- **Layer 2 → Data Link Layer**

### Physical Layer

The Physical Layer defines:

- Electrical properties
- Optical properties
- Physical connections
- Transfer speed

### Data Link Layer

The Data Link Layer provides:

- Data transfer between network nodes
- MAC addressing
- Ethernet frames
- Error detection

## Network Interface Card (NIC)

A **NIC (Network Interface Card)** is a hardware component that connects a device to a network.

A NIC allows devices to communicate:

- Using network cables
- Wirelessly

A NIC works at both the Physical and Data Link layers.

At the **Physical Layer**, it provides access to the physical medium.

At the **Data Link Layer**, it provides **MAC addressing**.

## MAC Address

**MAC = Media Access Control**

A MAC address is a unique identifier assigned to a network interface.

It is used for communication within a **local network**.

Example:

`00:1A:2B:3C:4D:5E`

A MAC address is:

- **48 bits long**
- Represented using **12 hexadecimal digits**

## MAC Address Structure

A MAC address has two main parts:

`00:1A:2B:3C:4D:5E`

- First 6 hexadecimal digits → **OUI**
- Last 6 hexadecimal digits → **Vendor-assigned identifier**

### OUI

**OUI = Organizationally Unique Identifier**

The OUI is the first **6 hexadecimal digits** of a MAC address.

It identifies the vendor and is assigned through IEEE.

The remaining 6 hexadecimal digits are assigned by the vendor to identify the network interface.

## Finding a MAC Address

### Windows

Use:

`ipconfig`

### Linux

Use:

`ifconfig`

A MAC address may be displayed as:

`00-1A-2B-3C-4D-5E`

or:

`00:1A:2B:3C:4D:5E`

Both represent a 48-bit MAC address.

## Ethernet Frame

An **Ethernet frame** is the unit of data sent over an Ethernet network.

A standard Ethernet frame contains:

1. Destination MAC Address
2. Source MAC Address
3. Type / EtherType
4. Payload
5. FCS

The basic structure is:

`Destination MAC → Source MAC → Type → Payload → FCS`

## Destination MAC Address

The **Destination MAC Address** identifies the device for which the frame is intended.

Example:

`Destination MAC = PC-B's MAC address`

## Source MAC Address

The **Source MAC Address** identifies the device that sent the frame.

Example:

`Source MAC = PC-A's MAC address`

## Type / EtherType

The **Type field**, also called **EtherType**, identifies the upper-layer protocol carried inside the Ethernet frame.

For example:

- IPv4 packet

## Payload

The **Payload** is the actual data received from the upper layer.

The payload is encapsulated inside the Ethernet frame.

The standard Ethernet payload size is:

**46 to 1500 bytes**

## FCS

**FCS = Frame Check Sequence**

FCS is added to the end of an Ethernet frame.

It is used to:

- Detect corrupted frames
- Check whether the frame was damaged during transmission

If a frame is corrupted, Ethernet normally **discards the frame**.

Ethernet generally does not retransmit corrupted frames.

Upper-layer protocols such as **TCP** can handle retransmission.

## MTU

**MTU = Maximum Transmission Unit**

For standard Ethernet, the maximum payload size is:

**1500 bytes**

So:

`MTU = 1500 bytes`

## Ethernet Frame Size

A standard Ethernet frame consists of:

- Header → **14 bytes**
- Payload → **46 to 1500 bytes**
- FCS → **4 bytes**

### Minimum Frame Size

`14 + 46 + 4 = 64 bytes`

### Maximum Frame Size

`14 + 1500 + 4 = 1518 bytes`

Therefore:

**Standard Ethernet frame size = 64 to 1518 bytes**

## Jumbo Frames

Frames with a payload larger than **1500 bytes** are called **Jumbo Frames**.

Important:

- Jumbo frames are not part of the standard Ethernet frame size.
- Some vendors and network devices support them.

## RUNT / Collision Fragment

An Ethernet frame smaller than **64 bytes** is called a:

**RUNT**

It may also be called a **Collision Fragment**.

Frames smaller than 64 bytes are automatically discarded by the receiving device.

## Simple Example

Suppose **PC-A** wants to send data to **PC-B**.

`PC-A → Switch → PC-B`

The Ethernet frame contains:

`Source MAC = PC-A`

`Destination MAC = PC-B`

`Payload = Actual data`

`FCS = Error detection`

The switch uses the **destination MAC address** to determine where the frame should be forwarded.

## Important Values

| Concept | Value |
|---|---:|
| Ethernet Standard | IEEE 802.3 |
| MAC Address | 48 bits |
| MAC Address | 12 hexadecimal digits |
| OUI | First 6 hexadecimal digits |
| Ethernet Header | 14 bytes |
| FCS | 4 bytes |
| Minimum Payload | 46 bytes |
| Maximum Payload / MTU | 1500 bytes |
| Minimum Frame Size | 64 bytes |
| Maximum Standard Frame Size | 1518 bytes |
| Jumbo Frame Payload | More than 1500 bytes |
| RUNT | Less than 64 bytes |

## ⭐ Remember

- **Ethernet → mainly used for LANs**
- **Ethernet → operates at Layer 1 and Layer 2**
- **Ethernet standard → IEEE 802.3**
- **NIC → connects a device to the network**
- **MAC → Media Access Control**
- **MAC address → 48 bits / 12 hexadecimal digits**
- **OUI → first 6 hexadecimal digits**
- **Ethernet → uses frames**
- **Ethernet frame → Destination MAC + Source MAC + Type + Payload + FCS**
- **FCS → detects corrupted frames**
- **MTU → 1500 bytes**
- **Standard Ethernet frame → 64 to 1518 bytes**
- **Jumbo Frame → payload larger than 1500 bytes**
- **RUNT → frame smaller than 64 bytes**
