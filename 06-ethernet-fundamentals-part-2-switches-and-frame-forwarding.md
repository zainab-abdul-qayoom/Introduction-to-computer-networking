# Ethernet Fundamentals: Switches and Frame Forwarding

## What is an Ethernet Switch?

An **Ethernet switch** is a hardware device with multiple ports that connect Ethernet devices in a network.

A switch receives Ethernet frames and forwards them to the correct destination.

## MAC Address Table

A switch forwards frames using the **destination MAC address**.

To know where a device is connected, the switch maintains a **MAC address table**.

The table maps:

`MAC Address → Switch Port`

Example:

`MAC A → Port 1`

This means the device with MAC address A is connected through Port 1.

## How Does a Switch Learn MAC Addresses?

When a frame arrives at a switch, the switch looks at the **source MAC address** and learns which port the device is connected to.

Example:

`Node A → Switch Port 1`

The switch learns:

`MAC A → Port 1`

Later, if another node sends a frame to MAC A, the switch can forward it directly to Port 1.

## Dynamic MAC Addresses

MAC addresses learned automatically by the switch are called **dynamic entries**.

Dynamic entries have an **aging time**.

If an entry is not used for a certain period, it is removed from the MAC address table.

## Static MAC Addresses

MAC addresses can also be manually configured.

These are called **static entries**.

Static entries:

* Do not age out automatically
* Remain in the table until manually removed

## Known Unicast Frame

A **known unicast frame** is a frame whose destination MAC address is already present in the MAC address table.

The switch sends the frame only through the port associated with that MAC address.

Example:

`Node A → Switch → Port 2 → Node B`

If the switch knows that Node B is connected to Port 2, it forwards the frame only to Port 2.

## Unknown Unicast Frame

An **unknown unicast frame** is a frame whose destination MAC address is not found in the MAC address table.

The switch **floods** the frame.

Flooding means sending the frame through all ports **except the incoming port**.

Example:

`Node A → Switch → Ports 2, 3, 4`

The switch does this because it does not know which port contains the destination device.

## Broadcast Frame

A **broadcast frame** is intended for **all devices in the network**.

The Ethernet broadcast MAC address is:

`FF:FF:FF:FF:FF:FF`

When a switch receives a broadcast frame, it floods the frame to all other ports.

## Multicast Frame

A **multicast frame** is intended for a **selected group of devices**.

Multicast frames use special MAC addresses.

Traditional Ethernet switches may flood multicast frames because they may not have the logic to forward them only to the intended group members.

## Layer 2 Switching

Traditional Ethernet switching operates at **Layer 2 of the OSI model**.

Switches make forwarding decisions using the destination MAC address.

`Destination MAC Address → Switch Port`

## Layer 3 Routing

Routing operates at **Layer 3 of the OSI model**.

Routers forward packets based on the destination IP address.

`Destination IP Address → Next Hop`

So:

* **Layer 2 → MAC address → Switching**
* **Layer 3 → IP address → Routing**

## Layer 3 Switch

A **Layer 3 switch** combines the functionality of a switch and a router.

It can perform:

* Layer 2 switching
* Layer 3 routing

This provides more flexibility when designing a network.

## ⭐ Remember

* **Switch → forwards Ethernet frames**
* **Switch → uses destination MAC addresses**
* **MAC address table → maps MAC addresses to switch ports**
* **Dynamic entries → learned automatically and can age out**
* **Static entries → manually configured and do not age out**
* **Known unicast → forwarded through the specific port**
* **Unknown unicast → flooded to all ports except the incoming port**
* **Broadcast → sent to all devices**
* **Multicast → intended for a selected group**
* **Layer 2 → switching using MAC addresses**
* **Layer 3 → routing using IP addresses**
* **Layer 3 switch → combines switching and routing**
