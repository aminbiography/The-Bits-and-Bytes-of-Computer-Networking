## Computer Networking Overview

Computer networking enables devices to communicate and exchange data across local and global networks.  
The Internet is a massive interconnection of independent networks operated by different organizations.  
Networking relies on layered models, standardized protocols, and routing mechanisms to deliver data reliably and efficiently.

---

## Network Models

### Five-Layer Model

- **Physical** – Cables, signals, connectors, and hardware used to transmit raw bits.
- **Data Link** – Ethernet frames, MAC addresses, switches, and local network communication.
- **Network** – IP addressing, packet forwarding, fragmentation, and routing between networks.
- **Transport** – End-to-end communication using protocols such as TCP and UDP.
- **Application** – User-facing protocols and services that applications use.

---

## IP Addressing

IP addressing is a method of uniquely identifying devices on a network so they can communicate with each other.  
IP addresses are logical and hierarchical, allowing packets to traverse multiple networks.

### IP Address Types

#### IPv4
- 32-bit numerical address
- Written in dotted decimal notation  
- Example: `192.168.1.1`

#### IPv6
- 128-bit numerical address
- Written in hexadecimal, separated by colons
- Introduced to solve IPv4 address exhaustion  
- Example: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

---

## Subnetting

Subnetting is the process of dividing a large network into smaller, more manageable subnetworks (subnets).  
It improves performance, security, routing efficiency, and IP address utilization.

### Subnet Mask

A subnet mask is a 32-bit value that determines which portion of an IP address represents:

- **Network/Subnet ID** – Bits set to `1`
- **Host ID** – Bits set to `0`

Usable hosts per subnet are calculated as:

```

2^n − 2

```

(where `n` is the number of host bits)

---

## CIDR (Classless Inter-Domain Routing)

CIDR replaces the rigid Class A, B, and C addressing system.  
It uses **slash notation** to define the network prefix length.

Example:
- `/24` → 24 bits for network ID
- `9.100.100.100/27`

CIDR allows flexible network sizing and reduces routing table size.

---

## Address Classes (Legacy System)

- **Class A** – First octet is the network ID (0–127)
- **Class B** – First two octets are the network ID (128–191)
- **Class C** – First three octets are the network ID (192–223)
- **Class D** – Multicast traffic
- **Class E** – Experimental use

These classes are largely obsolete but still important for foundational understanding.

---

## Binary Math & Logic

- **Base 2** – Computers use binary due to logic gate design (0 = False, 1 = True)
- **Octets** – IP addresses consist of four 8-bit octets (0–255)

### Logical Operators

- **AND** – Result is 1 only if both bits are 1  
  Used to calculate network IDs with subnet masks.
- **OR** – Result is 1 if at least one bit is 1

---

## The IP Datagram

An IP datagram is the packet used at the **Network Layer**.  
It consists of a header (control information) and a payload (actual data).

### IP Datagram Header Fields

![IP Datagram Header](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-02-01-Source-and-Destination-IP-Address-fields.jpg)

Key fields include:
- Version
- Header Length
- Service Type
- Total Length
- Identification
- Flags
- Fragment Offset
- Time To Live (TTL)
- Protocol
- Header Checksum
- Source IP Address
- Destination IP Address
- Options and Padding

**TTL** prevents infinite routing loops by limiting hop count.

---

## Fragmentation

Fragmentation occurs when an IP datagram exceeds the Maximum Transmission Unit (MTU) of a network.

- Large datagrams are split into smaller fragments
- Identification field groups fragments
- Fragment Offset ensures proper reassembly
- Reassembly happens at the destination host

---

## Encapsulation (Layered Data Flow)

Encapsulation is the process of wrapping data with protocol headers as it moves down the network stack.

![Encapsulation Process](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-02-02-IP-Datagram.jpg)

Flow:
- Application message
- TCP or UDP header added (Transport Layer)
- IP header added (Network Layer)
- Ethernet header and footer added (Data Link Layer)

---

## ARP (Address Resolution Protocol)

ARP resolves IP addresses to MAC addresses within a local network.

Process:
1. Device checks ARP table
2. If no entry exists, an ARP broadcast is sent
3. Target replies with its MAC address
4. Entry is cached temporarily

ARP operates only within a LAN.

---

## Routing & Routing Tables

### Router
A router is a device with at least two network interfaces that forwards packets based on destination IP addresses.

### Routing Table

Contains:
1. **Destination Network**
2. **Next Hop**
3. **Metric (Total Hops)**
4. **Interface**

Routers select the shortest or best available path.

---

## Routing Protocols

### Autonomous System (AS)
A group of networks under a single administrative control (e.g., ISP, enterprise).

### Interior Gateway Protocols (IGP)
Used within an AS:
- **Distance Vector** (e.g., RIP) – Shares routing tables with neighbors
- **Link State** (e.g., OSPF) – Shares full topology, faster convergence

### Exterior Gateway Protocols (EGP)
Used between ASs:
- **BGP (Border Gateway Protocol)** – The routing protocol of the global Internet

---

## IP Space & Standards

- **IANA** – Manages global IP and ASN allocation
- **RFCs** – Documents defining Internet standards (e.g., RFC 1918)

### Non-Routable Address Space (RFC 1918)

- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

These addresses are used internally and are not routed on the public Internet.

### NAT (Network Address Translation)

NAT allows private IP addresses to communicate with the Internet by translating them into public IP addresses.

---

## Final Takeaway

This revision covers:
- Layered networking models
- IP addressing and subnetting
- Binary logic and subnet masks
- IP datagrams, fragmentation, and encapsulation
- Routing, routing tables, and protocols
- Internet standards and private addressing

These fundamentals are essential for IT support, networking, cybersecurity, and systems engineering roles.
```

---



