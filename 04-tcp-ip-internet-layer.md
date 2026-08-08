# TCP/IP Protocol Suite: Internet Layer

## What is the Internet Layer?

The **Internet Layer** is responsible for delivering packets from a **source network to a destination network**.

The main protocol here is **IP (Internet Protocol)**.

In this video, we mainly focus on **IPv4**.

## IP

IP provides network services to **TCP and UDP**.

IP is a **best-effort protocol**, meaning it does not guarantee that data will arrive successfully.

IP does **not** provide:

* Reliability
* Flow control
* Sequencing

These responsibilities are handled by higher layers, such as TCP.

## IPv4 Address

An IPv4 address is **32 bits**, divided into **4 groups of 8 bits** called octets.

Example:

`192.168.1.10`

The four parts are separated by dots. This is called **dotted decimal notation**.

## Network Part and Host Part

An IP address has two important parts:

* **Network address** → identifies the network/subnet
* **Host address** → identifies a particular device in that network

Example:

`192.168.1.10`

Here, the device `10` is an example of a host address within the `192.168.1.0` network.

Devices in the same subnet share the same network address.

## Routing

**Routing** means choosing the best path for a packet to reach its destination.

A **router** is a device that forwards IP packets between different networks.

Example:

`PC → Router → Router → Router → Destination`

Each router forwards the packet to the next router. This is called **hop-by-hop routing**.

## Routing Table

A router uses a **routing table** to decide where to send a packet.

The routing table contains information about:

* Destination networks
* Next-hop routers
* Interfaces used to reach them

## How the Layers Work Together

The data moves through the layers like this:

`Application → Transport → Internet → Network Access`

For example:

`Data → TCP/UDP → IP Packet → Ethernet`

The Internet Layer adds an **IP header** to the data.

## ⭐ Remember

* **Internet Layer → delivers packets between networks**
* **IP → main Internet Layer protocol**
* **IPv4 → 32-bit address**
* **IP address → identifies a network and host**
* **Router → forwards packets between networks**
* **Routing → choosing the best path**
* **Routing table → helps routers make forwarding decisions**
* **IP works hop-by-hop**
* **IP is best-effort and does not guarantee delivery**
