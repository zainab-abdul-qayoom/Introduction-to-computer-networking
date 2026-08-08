# TCP/IP Protocol Suite: Application Layer

## What is the Application Layer?

The **Application Layer** is where network applications communicate with each other.

Examples:

* Web browser ↔ Web server
* File transfer between computers

The applications need to use the **same protocol** to understand each other.

## HTTP

**HTTP = Hypertext Transfer Protocol**

It is used for communication between a **web browser (client)** and a **web server**.

Simple example:

`Browser → HTTP Request → Server`

`Browser ← HTTP Response ← Server`

**HTTPS** is the secure version of HTTP.

## FTP

**FTP = File Transfer Protocol**

It is used to **transfer files between computers**.

For example:

`Computer A → File → Computer B`

FTP can use authentication such as a username and password. Secure versions can protect the login details and file contents.

## Important Point

Application layer protocols pass their data to the **Transport Layer**.

The transport layer can use:

* **TCP**
* **UDP**

We'll learn about TCP and UDP in the next video.

## ⭐ Remember

* **Application Layer** → Communication between applications
* **HTTP** → Web communication
* **HTTPS** → Secure web communication
* **FTP** → File transfer
* Applications must use the **same protocol** to communicate
* Application Layer → sends data to the **Transport Layer**
