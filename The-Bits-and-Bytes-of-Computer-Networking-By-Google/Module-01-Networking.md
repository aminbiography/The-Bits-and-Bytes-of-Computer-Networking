# Networking Models

## 01. The Networking Models

Networking is understood through layered models where each layer provides a specific service to the one above it.

**Five-Layer Model:** Physical, Data Link, Network, Transport, and Application
**OSI Model:** Seven layers (adds Session and Presentation between Transport and Application)

| Layer # | TCP/IP Model (Practical)        | Maps To → | OSI Model (Theoretical) | Unit of Data |
| ------: | ------------------------------- | --------- | ----------------------- | ------------ |
|       5 | Application                     | ↔         | Application (L7)        | Data         |
|         | (Includes Presentation/Session) | ↔         | Presentation (L6)       | Data         |
|         | (Includes Presentation/Session) | ↔         | Session (L5)            | Data         |
|       4 | Transport                       | ↔         | Transport (L4)          | Segments     |
|       3 | Network                         | ↔         | Network (L3)            | Packets      |
|       2 | Data Link                       | ↔         | Data Link (L2)          | Frames       |
|       1 | Physical                        | ↔         | Physical (L1)           | Bits         |

***The diagram below shows the practical TCP/IP five-layer model.***  
***Each layer has specific protocols, data units, and addressing methods.***

![TCP/IP Five Layer Model](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-01-TCP-IP-five-layer-model.png)


**Key Concept:** A protocol is the “language” or set of rules computers use to communicate at each layer.

---

## 02. The Physical Layer (Layer 1)

Focuses on moving **bits (1s and 0s)** across hardware.

### Copper Cabling (Twisted Pair)

* Cat5 → older
* Cat5e → reduced crosstalk
* Cat6 → faster, better shielding, shorter max length at high speed

### Fiber Optic

* Uses pulses of light
* Faster, longer distances, immune to interference
* More fragile and expensive

### Transmission Modes

* **Simplex:** one-way only
* **Half-Duplex:** both ways, but not at the same time
* **Full-Duplex:** both ways simultaneously

---

## 03. The Data Link Layer (Layer 2)

Responsible for communication between devices on the same network using **Ethernet**.

* **MAC Address:** 48-bit unique hardware ID (e.g., `00:1A:2B:3C:4D:5E`)

  * OUI (first 3 octets) identifies the manufacturer
* **Ethernet Frame:** structured data package

  * CRC/FCS detects data corruption

### Communication Types

* **Unicast:** to one device
* **Multicast:** to a group
* **Broadcast:** to everyone on the LAN (`FF:FF:FF:FF:FF:FF`)

---

## 04. Duplex Communication

* **Full-Duplex:** both directions at once
* **Half-Duplex:** one direction at a time
* **Simplex:** one-way only

---

## 05. Networking Hardware

* **Hub (Layer 1):** sends data to all devices (large collision domain; rarely used)
* **Switch (Layer 2):** forwards data only to intended recipient (uses MAC)
* **Router (Layer 3):** connects networks; uses IP and BGP to choose best paths
* **Core Routers + BGP:** direct global Internet traffic
* **Patch Panel:** organizes cable endpoints; does not process data

---

## 06. Clients and Servers

* **Server:** provides data or services
* **Client:** requests data
* Most devices act as both at different times

---

## 07. Cabling Tools

* Crimper — attach connectors
* Cable stripper — remove insulation
* Punch-down tool — attach wires to panels
* Toner probe — trace cables
* Cable tester — verify cable quality
* Loopback plug — test ports
* Network tap — monitor traffic
* Wi-Fi analyzer — measure wireless performance

---

## 08. Transmission Types

* **Unicast:** one device to one device
* **Multicast:** targeted group
* **Broadcast:** all devices (`FF:FF:FF:FF:FF:FF`)

---

## 09. Ethernet Frames

* Preamble + SFD — synchronization
* Destination MAC + Source MAC
* EtherType / VLAN header (optional)
* Payload (46–1500 bytes)
* Frame Check Sequence (CRC) — detects corruption (does not repair)

**Ethernet Frame Structure**

***An Ethernet frame is a structured collection of data that travels across a network link.***  
***Each part of the frame has a specific purpose, from synchronization to addressing and error detection.***

![Ethernet Frame](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-01-Ethernet-Frame.png)


---





