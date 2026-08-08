# Data Center Design Considerations

## What is a Data Center?

A **data center** is a facility used to house computer systems and their associated components.

These components can include:

* Compute systems
* Network systems
* Storage systems

A data center can range from a small server room to multiple buildings distributed across different locations.

Modern data centers can connect **on-premises infrastructure** with **cloud infrastructure**.

They require:

* Scalability
* Resiliency
* Security
* Efficiency

## Data Center Design

**Data center design** is the process of planning the important requirements of a data center.

Some important considerations include:

* Number and type of servers
* Network layout
* Power
* Cooling and ventilation
* Physical security
* Disaster recovery
* Business continuity

This lesson mainly focuses on **networking considerations**.

## Network Topology

A **network topology** is the arrangement of devices, links, and connections in a network.

It describes:

* How devices are connected
* How data moves between devices
* How the network is structured

## Factors for Choosing a Network Topology

Important factors include:

### Availability

The network should remain available even when problems occur.

High availability depends on:

* Hardware
* Software
* Network protocols
* Power
* Environmental systems

### Reliability

A reliable network should minimize downtime and delays.

### Performance

A good topology can improve:

* Network performance
* Fault detection
* Troubleshooting
* Resource utilization

### Future Growth

The topology should allow new devices and systems to be added without significantly affecting performance.

### Budget

The topology must also be affordable.

The best design is not always the most expensive one.

## Hierarchical Network Design

A **hierarchical network design** separates the network into different layers.

Each layer has a specific role.

This design is effective for **North-South traffic**, where most traffic enters or leaves the data center.

Example:

`Client → Network → Server`

The hierarchical design is modular and can scale reasonably well.

However, it can experience bottlenecks when links between layers become overloaded.

## East-West Traffic

Modern data centers have more **East-West traffic** because servers and storage systems communicate directly with each other.

Example:

`Server → Server`

Cloud computing, virtualization, and big data have increased the need for server-to-server communication.

Modern networks therefore need:

* High scalability
* High resiliency
* Efficient server-to-server communication

## Leaf-Spine Architecture

A **leaf-spine architecture** is a two-layer network design commonly used in modern data centers.

It consists of:

* **Leaf layer**
* **Spine layer**

Leaf switches connect servers to the network.

Spine switches connect the leaf switches together.

Every leaf switch connects to every spine switch.

```text
        Spine 1
       /   |   \
      /    |    \
 Leaf 1  Leaf 2  Leaf 3
   |       |       |
 Servers Servers Servers
```

Leaf switches are also called **Top-of-Rack (ToR) switches**.

## Super Spine

For very large networks, a third layer can be added.

This layer is called the:

* **Super Spine**
* **Core**

The super spine connects the spine switches together.

## Layer 2 Network Design

In a **Layer 2 network**, devices make forwarding decisions using **MAC addresses**.

Switches maintain a **MAC address table** that maps:

`MAC Address → Exit Port`

Switches forward Ethernet frames based on the destination MAC address.

### Limitations of Layer 2

Layer 2 networks:

* Do not scale as well
* Can provide lower performance
* Make redundancy more difficult
* Make multipath support more difficult

## Redundancy

**Redundancy** means having additional links or devices so that the network can continue working if one fails.

Example:

```text
        Spine 1
       /       \
Leaf 1           Leaf 2
       \       /
        Spine 2
```

If one path fails, another path can be used.

The main purpose of redundancy is to eliminate a **single point of failure**.

## Multipath

**Multipath** means using multiple paths to reach the same destination.

It can provide:

* Higher bandwidth
* Load balancing
* Better resource utilization

Instead of using only one path:

`Host → Spine 1 → Destination`

Traffic can use multiple paths:

`Host → Spine 1 → Destination`

`Host → Spine 2 → Destination`

## Layer 2 Loops

Redundant Layer 2 links can create **network loops**.

Broadcast frames are flooded by switches.

If a loop exists, broadcast frames can circulate continuously and consume network bandwidth.

This is called a **broadcast storm**.

## Spanning Tree Protocol (STP)

**STP** prevents Layer 2 loops by creating a loop-free logical topology.

STP identifies redundant links and places some ports into a **blocking state**.

If the active path fails, STP can move a blocked path into the forwarding state.

The traditional STP convergence time can be around **30–50 seconds**.

## Rapid Spanning Tree Protocol (RSTP)

**RSTP** is an improved version of STP designed for faster recovery.

It can react to topology changes much faster than traditional STP.

RSTP provides alternate paths that can quickly move into the forwarding state when an active path fails.

## Multiple Spanning Tree Protocol (MSTP)

**MSTP** allows multiple STP instances to be configured.

Different groups of VLANs can use different active paths.

Example:

```text
VLAN 1–50   → Spine 1
VLAN 51–100 → Spine 2
```

This can provide better load balancing and network utilization.

However, managing multiple MST instances can become difficult in large networks.

## Link Aggregation Group (LAG)

A **Link Aggregation Group (LAG)** combines multiple physical links into one logical link.

LAG is also known as:

* Port Channel
* Bonding

Benefits include:

* Higher bandwidth
* Load balancing
* High availability

If one physical link fails, the remaining links can continue carrying traffic.

## Multi-Chassis LAG (MLAG)

**MLAG** allows physical links from two separate switches to be combined into one logical connection.

The connected device sees the two switches as a single Layer 2 connection.

MLAG provides:

* Higher bandwidth
* Load balancing
* Link redundancy
* Switch redundancy

## Layer 3 Network Design

In a **Layer 3 network**, routers or Layer 3 switches forward packets using **IP addresses**.

Routers maintain a **routing table**.

The routing table maps remote networks to next-hop routers.

Routes can be configured using:

* Static routing
* Dynamic routing protocols

Examples of dynamic routing protocols include:

* OSPF
* BGP

## Layer 3 Advantages

Layer 3 networks make redundancy and multipath support easier.

Routing protocols can identify and avoid routing loops.

Layer 3 designs can therefore provide:

* Active-active links
* Redundancy
* Load balancing
* Better scalability

## ECMP

**Equal-Cost Multipath (ECMP)** allows traffic to reach the same destination using multiple paths with equal routing cost.

Example:

```text
             → Spine 1 →
Host → Leaf              → Destination
             → Spine 2 →
```

Traffic can be distributed across both paths.

This improves:

* Bandwidth utilization
* Load balancing
* Network performance

## TTL

IP packets contain a **Time To Live (TTL)** field.

TTL helps prevent packets from circulating forever in a routing loop.

Each router decreases the TTL value.

When the TTL reaches zero, the packet is discarded.

## OSPF vs BGP

Two important routing protocols are:

* **OSPF**
* **BGP**

BGP is widely used in modern large-scale data centers because it is designed for scalability and stability.

BGP is also the main routing protocol used to exchange routing information across the Internet.

## Layer 2 + Layer 3 Design

A data center can combine Layer 2 and Layer 3 networking.

For example:

* Leaf switches operate at Layer 2 toward hosts
* MLAG provides redundancy
* Links between leaf and spine switches operate at Layer 3
* ECMP provides load balancing and redundancy

This design is relatively simple and is commonly suitable for data centers and large enterprises.

## Full Layer 3 Design

A **full Layer 3 design** uses routing from the hosts through the leaf-spine network.

It provides:

* High scalability
* High redundancy
* ECMP
* No need for Layer 2 loop prevention protocols

One disadvantage is that host administration can become more complicated because routing may need to be configured on the hosts.

## Layer 2 vs Layer 3

| Feature         | Layer 2        | Layer 3                 |
| --------------- | -------------- | ----------------------- |
| Forwarding      | MAC address    | IP address              |
| Main device     | Switch         | Router / Layer 3 switch |
| Address table   | MAC table      | Routing table           |
| Multipath       | More difficult | Easier                  |
| Redundancy      | More complex   | Easier                  |
| Scalability     | Lower          | Higher                  |
| Loop prevention | STP/RSTP/MSTP  | Routing protocols       |
| Load balancing  | More difficult | ECMP                    |

## ⭐ Remember

* **Data center → houses compute, network, and storage systems**
* **Network topology → describes how devices and links are arranged**
* **Hierarchical design → traditional multi-layer design**
* **Leaf-spine → modern data center topology**
* **Leaf → connects servers**
* **Spine → connects leaf switches**
* **Redundancy → provides backup paths**
* **Multipath → uses multiple paths for traffic**
* **Layer 2 → forwards using MAC addresses**
* **Layer 3 → forwards using IP addresses**
* **STP → prevents Layer 2 loops**
* **RSTP → faster version of STP**
* **MSTP → supports multiple STP instances**
* **LAG → combines multiple physical links**
* **MLAG → combines links across multiple switches**
* **ECMP → uses multiple equal-cost paths**
* **TTL → prevents packets from looping forever**
* **BGP → widely used for large-scale data center routing**
* **Modern large-scale data centers generally favor Layer 3 designs**
