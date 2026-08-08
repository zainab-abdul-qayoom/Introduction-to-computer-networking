# Ethernet Fundamentals: Switches and Frame Forwarding

## 1. What is an Ethernet Switch?

An **Ethernet switch** is a hardware device with multiple ports used to connect Ethernet nodes such as computers, servers, and other network devices.

Switches can have different:

* Number of ports
* Port speeds
* Models and sizes

The main purpose of a switch is to **forward Ethernet frames to the correct destination**.

## 2. How Does a Switch Forward Frames?

An Ethernet switch forwards frames based on the **destination MAC address**.

Example:

`Node A → Switch → Node B`

When Node A sends a frame to Node B:

1. Node A creates an Ethernet frame.
2. The frame contains a **source MAC address** and **destination MAC address**.
3. The switch receives the frame.
4. The switch checks its **MAC address table**.
5. The switch determines which port leads to Node B.
6. The frame is forwarded through that port.

## 3. MAC Address Table

A switch maintains a database called the **MAC address table**.

The table maps:

`MAC Address → Switch Port`

Example:

| MAC Address | Port   |
| ----------- | ------ |
| MAC A       | Port 1 |
| MAC B       | Port 2 |
| MAC C       | Port 3 |

The switch uses this table to determine where Ethernet frames should be forwarded.

## 4. How Does a Switch Learn MAC Addresses?

A switch learns MAC addresses from the **source MAC address** of incoming frames.

Example:

Node A sends a frame through **Port 1**.

The switch sees:

`Source MAC = MAC A`

The switch stores:

`MAC A → Port 1`

Later, if another node sends a frame to MAC A, the switch knows that MAC A is reachable through **Port 1**.

## 5. Dynamic MAC Address Entries

MAC addresses learned automatically by the switch are called **dynamic entries**.

Dynamic entries have an **aging time**.

If an entry is not used for a certain period:

`MAC entry → Aging → Removed from table`

This prevents old information from remaining in the MAC address table forever.

The aging time can be adjusted by the switch vendor's configuration.

## 6. Static MAC Address Entries

A **static MAC address entry** is manually configured by a network administrator.

Unlike dynamic entries:

* Static entries do not age out.
* They remain in the MAC address table.
* They must be manually removed or changed.

Example:

`MAC A → Port 1`

This entry remains until an administrator removes it.

## 7. Known Unicast Frames

A **known unicast frame** is a frame whose destination MAC address exists in the switch's MAC address table.

Example:

`Destination MAC = MAC B`

If the table contains:

`MAC B → Port 2`

The switch forwards the frame only through **Port 2**.

### Key Point

**Known unicast → Forward to the specific port**

## 8. Unknown Unicast Frames

An **unknown unicast frame** occurs when the destination MAC address is not found in the MAC address table.

Example:

Node A sends a frame to Node D, but the switch does not know where MAC D is located.

The switch **floods** the frame.

Flooding means:

> Send the frame through all ports except the port where the frame was received.

### Key Point

**Unknown unicast → Flood**

## 9. Broadcast Frames

A **broadcast frame** is intended for **all nodes** on the local network.

The broadcast MAC address is:

`FF:FF:FF:FF:FF:FF`

It contains 12 hexadecimal `F` digits.

When a switch receives a broadcast frame, it **floods** the frame through all ports except the incoming port.

### Key Point

**Broadcast → Flood to all other ports**

## 10. Multicast Frames

A **multicast frame** is intended for a **specific group of destinations**.

Multicast MAC addresses have a special format where the **least significant bit of the first octet is set to 1**.

Traditional Ethernet switches may not have the logic to identify the exact multicast group members.

Therefore, multicast frames may be **flooded**.

### Key Point

**Multicast → Traditionally flooded**

## 11. Unicast vs Broadcast vs Multicast

| Type                | Destination                | Switch Action          |
| ------------------- | -------------------------- | ---------------------- |
| **Unicast**         | One node                   | Specific port if known |
| **Unknown Unicast** | One node, location unknown | Flood                  |
| **Broadcast**       | All nodes                  | Flood                  |
| **Multicast**       | Selected group             | Traditionally flooded  |

## 12. Layer 2 Switching

Traditional Ethernet switching operates at **Layer 2 (Data Link Layer)** of the OSI model.

A Layer 2 switch uses the:

**Destination MAC address**

to determine where to forward a frame.

Example:

`Ethernet Frame → Destination MAC → Switch → Port`

## 13. Routing vs Switching

Switching and routing operate at different OSI layers.

### Switching

* Operates at **Layer 2**
* Uses **MAC addresses**
* Uses a **MAC address table**
* Forwards Ethernet frames

### Routing

* Operates at **Layer 3**
* Uses **IP addresses**
* Uses a **routing table**
* Forwards IP packets

| Feature   | Switching         | Routing       |
| --------- | ----------------- | ------------- |
| OSI Layer | Layer 2           | Layer 3       |
| Address   | MAC               | IP            |
| Device    | Switch            | Router        |
| Table     | MAC address table | Routing table |
| Data      | Ethernet frame    | IP packet     |

## 14. Layer 3 Switch

A **Layer 3 switch**, also called a **multilayer switch**, combines the functionality of:

* A Layer 2 switch
* A Layer 3 router

This provides greater flexibility when designing a network.

A Layer 3 switch can perform both:

`MAC-based switching`

and

`IP-based routing`

## 15. Frame Forwarding Process

The basic process is:

```text
1. Frame arrives at switch
          ↓
2. Switch reads source MAC
          ↓
3. Switch learns source MAC + incoming port
          ↓
4. Switch checks destination MAC
          ↓
5. Destination found?
       ↙       ↘
     Yes        No
      ↓          ↓
Specific       Flood
   port
```

## ⭐ Remember

* **Switch → connects Ethernet nodes**
* **Switch forwards frames using destination MAC addresses**
* **MAC address table → maps MAC addresses to switch ports**
* **Source MAC → used by switch to learn**
* **Known unicast → sent to specific port**
* **Unknown unicast → flooded**
* **Broadcast → flooded**
* **Broadcast MAC → `FF:FF:FF:FF:FF:FF`**
* **Dynamic MAC entries → age out**
* **Static MAC entries → do not age out**
* **Layer 2 switching → uses MAC addresses**
* **Layer 3 routing → uses IP addresses**
* **Layer 3 switch → combines switching and routing**
