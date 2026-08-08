# Ethernet Fundamentals (Part 2): Switches and Frame Forwarding

## 1. What is an Ethernet Switch?

An **Ethernet switch** is a hardware device that connects multiple Ethernet devices in a network.

A switch has multiple:

> **Ports**

Devices such as computers, servers, and other switches can connect to these ports.

Example:

```text
PC A ───┐
PC B ───┤
PC C ───┤ Switch
PC D ───┘
```

Different switches can have:

* Different numbers of ports
* Different port speeds
* Different sizes
* Different capabilities

depending on the vendor and model.

---

# 2. Why Do We Need a Switch?

Suppose we have two computers:

```text
PC A ─── Switch ─── PC B
```

PC A wants to send an Ethernet frame to PC B.

The switch receives the frame and needs to determine:

> **Which port should the frame leave from to reach PC B?**

The switch makes this decision using the:

> **Destination MAC address**

---

# 3. How Does a Switch Know Where a Device Is?

A switch needs to know:

> **Which MAC address is located on which port?**

For this purpose, the switch maintains a database called the:

> **MAC Address Table**

The MAC address table contains mappings between:

```text
MAC Address → Switch Port
```

Example:

| MAC Address | Port   |
| ----------- | ------ |
| MAC A       | Port 1 |
| MAC B       | Port 2 |
| MAC C       | Port 3 |

This tells the switch where each learned device can be reached.

---

# 4. MAC Address Learning

One of the most important things to understand is:

> **A switch learns MAC addresses from the SOURCE MAC address of incoming frames.**

Suppose:

```text
PC A
MAC = AAA
   |
   | Port 1
   ↓
Switch
```

PC A sends a frame.

The frame contains:

```text
Source MAC = AAA
Destination MAC = BBB
```

The switch receives the frame on:

> **Port 1**

The switch learns:

```text
AAA → Port 1
```

It stores this information in its MAC address table.

---

# 5. Step-by-Step Example

Initially, the switch's table may be empty:

```text
MAC Address Table

MAC Address     Port
---------------------
(empty)
```

PC A sends a frame.

```text
Source MAC = MAC A
Incoming Port = 1
```

The switch learns:

```text
MAC A → Port 1
```

Now the table becomes:

```text
MAC Address     Port
---------------------
MAC A           1
```

Later, if the switch receives a frame destined for MAC A, it already knows:

> MAC A is on Port 1.

So it sends the frame only through:

> **Port 1**

---

# 6. How Does Forwarding Work?

Suppose we have:

```text
PC A ── Port 1
          |
       Switch
          |
      Port 2 ── PC B
```

PC A sends a frame to PC B.

The frame contains:

```text
Source MAC      = MAC A
Destination MAC = MAC B
```

The switch:

### Step 1

Receives the frame on Port 1.

### Step 2

Looks at the **source MAC address**.

It learns:

```text
MAC A → Port 1
```

### Step 3

Looks at the **destination MAC address**.

It searches the MAC address table for:

```text
MAC B
```

### Step 4

If MAC B is known:

```text
MAC B → Port 2
```

The switch forwards the frame only through:

> **Port 2**

---

# 7. MAC Address Table

The MAC address table is also called the:

> **Forwarding Database**

It stores:

> **Destination MAC address → Exit port**

Example:

```text
MAC Address Table

MAC A → Port 1
MAC B → Port 2
MAC C → Port 3
MAC D → Port 4
```

The switch uses this table to make forwarding decisions.

---

# 8. Dynamic MAC Address Learning

Normally, switches learn MAC addresses automatically.

These are called:

> **Dynamically learned entries**

The switch learns them by observing incoming frames.

Example:

```text
Frame arrives on Port 3

Source MAC = MAC C
        ↓
Switch learns:
MAC C → Port 3
```

No administrator needs to manually enter this information.

---

# 9. Aging of Dynamic Entries

Dynamically learned MAC addresses do not stay in the table forever.

They have an:

> **Aging Time**

If an entry is not used for a defined amount of time, the switch removes it from the MAC address table.

This process is called:

> **Aging / Flushing**

Example:

```text
MAC A → Port 1
```

If MAC A is not used for the configured aging period:

```text
MAC A → Port 1
```

is removed.

The switch can then learn the MAC address again when it sees another frame from that device.

---

# 10. Static MAC Address Entries

MAC addresses can also be configured manually.

These are called:

> **Static entries**

Static entries:

* Are manually configured
* Do not age out automatically
* Remain in the table
* Stay until manually removed

### Difference

| Dynamic Entry                   | Static Entry                   |
| ------------------------------- | ------------------------------ |
| Learned automatically           | Configured manually            |
| Has aging time                  | Does not normally age out      |
| Can be removed after inactivity | Remains until manually removed |

---

# 11. Known Unicast

A **unicast** frame is intended for:

> **One specific destination**

Suppose the switch receives:

```text
Destination MAC = MAC B
```

and its table contains:

```text
MAC B → Port 2
```

The destination is known.

Therefore, this is a:

> **Known Unicast Frame**

The switch sends the frame only through:

> **Port 2**

Example:

```text
        Port 1
PC A ────────┐
             │
          [SWITCH]
             │
        Port 2
             │
             PC B
```

Only the correct exit port is used.

---

# 12. Unknown Unicast

Sometimes the switch receives a frame for a destination MAC address that is **not present** in its MAC address table.

Example:

```text
Destination MAC = MAC D
```

But the table contains:

```text
MAC A → Port 1
MAC B → Port 2
MAC C → Port 3
```

There is no entry for:

```text
MAC D
```

This is called an:

> **Unknown Unicast Frame**

---

# 13. What Does a Switch Do With Unknown Unicast?

When the destination MAC is unknown, the switch:

> **Floods the frame**

Flooding means:

> Send the frame out of all ports except the port where the frame came in.

Example:

```text
              PC B
               ↑
               |
PC A → [SWITCH] → PC C
               |
               ↓
              PC D
```

If PC A sends an unknown unicast frame, the switch sends it out:

* Port to PC B
* Port to PC C
* Port to PC D

But **not back to PC A's incoming port**.

### Important

```text
Unknown Unicast → Flood
Known Unicast   → Specific port
```

---

# 14. Broadcast

A **broadcast** frame is intended for:

> **All devices in the network**

A broadcast MAC address has all bits set to 1.

Its hexadecimal representation is:

```text
FF:FF:FF:FF:FF:FF
```

This means:

> **Everyone should receive this frame.**

---

# 15. What Does a Switch Do With Broadcast?

When a switch receives a broadcast frame:

> **It floods the frame.**

It sends the frame out all appropriate ports except the incoming port.

Example:

```text
              PC B
               ↑
               |
PC A → [SWITCH] → PC C
               |
               ↓
              PC D
```

If PC A sends a broadcast:

```text
PC A → Switch → PC B
             → PC C
             → PC D
```

All connected devices receive it.

---

# 16. Multicast

A **multicast** frame is intended for:

> **A selected group of devices**

It is not meant for one device and not necessarily for everyone.

Think of it as:

```text
Unicast    → One
Broadcast  → Everyone
Multicast  → Selected group
```

---

# 17. Multicast MAC Address

Multicast Ethernet addresses are identified by a special bit:

> **The least significant bit of the first octet is set to 1.**

For example, the first octet has a certain bit indicating multicast.

You do not need to calculate this every time, but remember:

> **Multicast → selected group**

---

# 18. Traditional Multicast Forwarding

Traditional Ethernet switches did not have the logic required to forward multicast frames only to the intended group members.

Therefore, traditionally:

> **Multicast frames were flooded.**

So in the simplified behavior taught in this course:

```text
Unknown Unicast → Flood
Broadcast       → Flood
Traditional Multicast → Flood
Known Unicast   → Specific port
```

---

# 19. Flooding

**Flooding** means:

> Sending a frame out multiple switch ports instead of only one specific port.

The frame is normally sent out:

> **All appropriate ports except the incoming port.**

Example:

```text
                 PC B
                  ↑
                  |
                  |
PC A ──────── [SWITCH] ─────── PC C
                  |
                  ↓
                 PC D
```

If flooding occurs:

```text
PC A → Switch
        ├──→ PC B
        ├──→ PC C
        └──→ PC D
```

It does not send the frame back through the incoming port.

---

# 20. Multiple Switches

A network can contain multiple switches.

Example:

```text
PC A
  |
Switch 1
  |
Switch 2
  |
PC B
```

The switches need to learn where MAC addresses exist.

For example:

```text
Switch 1:
MAC B → Port connected toward Switch 2
```

Then Switch 1 knows that frames for MAC B should be sent toward Switch 2.

This allows switches to forward frames even when the destination device is **not directly connected** to them.

---

# 21. MAC Address Learning Across Multiple Switches

Consider:

```text
PC A
 |
Switch 1
 |
Switch 2
 |
PC B
```

PC A sends a frame.

Switch 1 receives it and learns:

```text
MAC A → Port connected to PC A
```

Switch 1 forwards the frame toward Switch 2.

Switch 2 receives the frame and learns:

```text
MAC A → Port connected to Switch 1
```

In this way, switches gradually learn where devices are located.

---

# 22. Switch vs Router

This is extremely important.

### Switch

Traditional Ethernet switching operates at:

> **Layer 2**

It forwards frames based on:

> **Destination MAC address**

### Router

Routing operates at:

> **Layer 3**

It forwards packets based on:

> **Destination IP address**

Remember:

```text
Switch → MAC address → Layer 2
Router → IP address  → Layer 3
```

---

# 23. Layer 2 Switching

Traditional switching:

```text
Destination MAC
       ↓
MAC Address Table
       ↓
Exit Port
```

The switch asks:

> "Where is this MAC address?"

Then it sends the frame through the correct port.

---

# 24. Layer 3 Routing

Routing works differently.

```text
Destination IP
       ↓
Routing Table
       ↓
Next Hop / Interface
```

The router asks:

> "What is the best path to this IP network?"

Then it forwards the packet toward the destination.

---

# 25. Layer 3 Switch

A **Layer 3 switch** combines functionality of:

> **Switch + Router**

It can perform:

* Layer 2 switching
* Layer 3 routing

Therefore, it provides more flexibility when designing a network.

It is also commonly called a:

> **Multilayer Switch**

---

# 26. Important Comparison

| Feature            | Layer 2 Switch | Router                 | Layer 3 Switch      |
| ------------------ | -------------- | ---------------------- | ------------------- |
| OSI Layer          | Layer 2        | Layer 3                | Layer 2 + Layer 3   |
| Uses               | MAC address    | IP address             | MAC + IP            |
| Main function      | Switching      | Routing                | Switching + Routing |
| Uses MAC table     | Yes            | No, uses routing table | Yes                 |
| Uses routing table | No             | Yes                    | Yes                 |

---

# 27. Frame Forwarding Decision

A switch basically follows this process:

```text
Frame arrives
     ↓
Read Source MAC
     ↓
Learn Source MAC + Incoming Port
     ↓
Read Destination MAC
     ↓
Search MAC Address Table
     ↓
   ┌───────────────┐
   │ Is destination│
   │    known?     │
   └───────┬───────┘
           │
      ┌────┴────┐
     YES        NO
      ↓          ↓
Specific       Flood
Port
```

---

# 28. The Four Important Cases

Remember these four:

### 1. Known Unicast

```text
Destination known
        ↓
Send to specific port
```

### 2. Unknown Unicast

```text
Destination unknown
        ↓
Flood
```

### 3. Broadcast

```text
Destination = Everyone
        ↓
Flood
```

### 4. Traditional Multicast

```text
Destination = Selected group
        ↓
Traditionally flooded
```

---

# 29. Easy Real-Life Example

Imagine a school with many classrooms.

The **switch** is like the receptionist who learns:

```text
Student A → Room 1
Student B → Room 2
Student C → Room 3
```

If someone asks for Student B:

> The receptionist knows Room 2 → sends them there.

This is like:

```text
Known Unicast → Specific Port
```

If the receptionist doesn't know where Student D is:

> They ask/search multiple rooms.

This is like:

```text
Unknown Unicast → Flooding
```

If there is an announcement for everyone:

```text
Broadcast → Everyone
```

---

# 30. Important Terms

### Switch

A device that connects Ethernet devices and forwards frames.

### Port

A physical/logical connection point on a switch.

### MAC Address Table

A table that maps MAC addresses to switch ports.

### MAC Learning

The process by which a switch learns source MAC addresses.

### Dynamic Entry

An automatically learned MAC address that can age out.

### Static Entry

A manually configured MAC address that does not normally age out.

### Unicast

Communication from one device to one destination.

### Broadcast

Communication intended for all devices.

### Multicast

Communication intended for a selected group.

### Flooding

Sending a frame out multiple ports except the incoming port.

### Known Unicast

Unicast destination is found in the MAC address table.

### Unknown Unicast

Unicast destination is not found in the MAC address table.

### Layer 2 Switching

Forwarding based on MAC addresses.

### Layer 3 Routing

Forwarding based on IP addresses.

### Layer 3 / Multilayer Switch

A switch capable of both switching and routing.

---

# 31. Most Important Exam Points

Memorize these:

1. **Switches operate traditionally at Layer 2.**
2. **Switches forward Ethernet frames using destination MAC addresses.**
3. **A switch learns MAC addresses from the source MAC of incoming frames.**
4. **MAC addresses are stored in a MAC address table.**
5. **MAC address table entries map MAC addresses to switch ports.**
6. **Dynamic MAC entries have an aging time.**
7. **Static MAC entries remain until manually removed.**
8. **Known unicast frames are sent through a specific port.**
9. **Unknown unicast frames are flooded.**
10. **Broadcast frames are flooded.**
11. **Broadcast MAC address = `FF:FF:FF:FF:FF:FF`.**
12. **Traditional Ethernet switches flood multicast frames.**
13. **Routing operates at Layer 3 and uses IP addresses.**
14. **A Layer 3 switch combines switching and routing functionality.**

---

# 32. Quick Revision

```text
ETHERNET SWITCH
      ↓
Layer 2
      ↓
Uses MAC addresses
      ↓
Learns Source MAC
      ↓
Stores MAC → Port
      ↓
MAC Address Table
      ↓
Checks Destination MAC
      ↓
 ┌──────────────┬─────────────────┐
 │              │                 │
Known         Unknown          Broadcast
Unicast       Unicast
 │              │                 │
 ↓              ↓                 ↓
Specific      Flood             Flood
Port
```

### One-line memory trick

> **Switch learns SOURCE MAC, forwards using DESTINATION MAC.**

And:

> **MAC = Switching, IP = Routing.**
