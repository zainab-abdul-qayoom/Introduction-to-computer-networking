# Introduction to Networking

## 1. What is a Network?

A **network** is a group of devices connected together so they can **exchange data**.

Examples of data:

* Text
* Files
* Images
* Videos
* Voice

## 2. Network Components

There are two main types:

**End Nodes**

* Computers
* Servers
* Storage devices
* They are the **source or destination** of data.

**Intermediate Nodes**

* **Switches** forward data inside a network.
* **Routers** forward data between different networks.

## 3. NIC

**NIC = Network Interface Card**

It is the hardware that allows a device to connect to a network.

Example:

`Computer → NIC → Cable → Switch`

## 4. Protocol

A **protocol** is a set of rules that devices follow to communicate.

It defines things like:

* How data is formatted
* How communication starts and ends
* How errors are handled

A group of protocols working together is called a **Protocol Suite**.

## 5. OSI Model

The **OSI model** divides network communication into **7 layers**.

It helps us understand how data moves through a network.

The important idea for now:

**OSI = 7 layers**

## 6. TCP/IP Model

The **TCP/IP model** is another model used for networking.

**TCP/IP = 4 layers**

Some important protocols are:

* **HTTP, FTP** → Application
* **TCP, UDP** → Transport
* **IPv4, IPv6** → Internet

## 7. Encapsulation

When data is sent, each layer adds its own information to the data.

This process is called **encapsulation**.

Simple flow:

`Message → Segment → Packet → Frame → Bits`

### Remember

* **Segment** → Transport layer
* **Packet** → Internet layer
* **Frame** → Data Link layer
* **Bits** → Physical layer

## 8. Important Addresses

* **Port number** → Transport layer
* **IP address** → Internet layer
* **MAC address** → Data Link layer

## ⭐ Quick Revision

**Network:** Connected devices exchanging data.

**Protocol:** Rules for communication.

**Switch:** Forwards frames in a local network.

**Router:** Routes packets between networks.

**OSI:** 7-layer model.

**TCP/IP:** 4-layer model.

**Encapsulation:** Adding information to data as it moves down the layers.

### Main Flow

`Data → Segment → Packet → Frame → Bits`
