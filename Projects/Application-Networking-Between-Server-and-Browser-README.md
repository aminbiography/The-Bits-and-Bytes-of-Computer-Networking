# Application Networking Between Server and Browser
  
---

### This presentation is based on **"All the Layers Working in Unison"** from **"The Bits and Bytes of Computer Networking"**

---

## End-to-end web request (Computer 1 → Computer 2)

A full network communication requires every layer (Physical → Data Link → Network → Transport → Application) to work together to deliver a TCP segment from a client to a server.

**Example:** Computer 1 (10.1.1.100) opens a browser to reach Computer 2 (172.16.1.100:80) across Router A and Router B.

---

## Phase 1: Topology and Local Decision (Computer 1)

**When the user enters an IP into a browser, the OS networking stack performs a logical comparison.**

**Subnet Check:** Computer 1 compares its IP (10.1.1.100) and subnet (/24) to the destination (172.16.1.100). Since they do not match, it realizes the packet must go to the Default Gateway (10.1.1.1).

**ARP Discovery:** Computer 1 broadcasts an ARP Request to find the MAC address of the gateway. Router A responds with its hardware address.

**Socket Creation:** The OS opens a socket using an Ephemeral Port (e.g., 50,000) to represent the web browser’s end of the connection.

### Images (Phase 1)

#### Image 01 — Network Topology Overview
![Phase 1 - Network Topology Overview](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-01-Network-Topology-Overview.jpg)

#### Image 02 — Topology With Router A
![Phase 1 - Topology With Router A](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-02-Topology-With-Router-A.jpg)

#### Image 03 — Topology With Router A and Router B
![Phase 1 - Topology With Router A and Router B](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-03-Topology-With-Router-A-and-Router-B.jpg)

#### Image 04 — Full Topology With All Interfaces
![Phase 1 - Full Topology With All Interfaces](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-04-Full-Topology-With-All-Interfaces.jpg)

#### Image 05 — Client and Server Identified
![Phase 1 - Client and Server Identified](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-05-Client-and-Server-Identified.jpg)

#### Image 06 — Browser Starts TCP Connection
![Phase 1 - Browser Starts TCP Connection](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-06-Browser-Starts-TCP-Connection.jpg)

#### Image 07 — Subnet Decision (Local or Remote)
![Phase 1 - Subnet Decision](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-07-Subnet-Decision-Local-or-Remote.jpg)

#### Image 08 — ARP Cache Check (Gateway MAC Unknown)
![Phase 1 - ARP Cache Check](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-08-ARP-Cache-Check-Gateway-MAC-Unknown.jpg)

#### Image 09 — ARP Request Broadcast
![Phase 1 - ARP Request Broadcast](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-09-ARP-Request-Broadcast.jpg)

#### Image 10 — ARP Reply (Gateway MAC Learned)
![Phase 1 - ARP Reply Gateway MAC Learned](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-10-ARP-Reply-Gateway-MAC-Learned.jpg)

#### Image 11 — TCP Connection Continues
![Phase 1 - TCP Connection Continues](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-11-TCP-Connection-Continues.jpg)

---

## Phase 2: Encapsulation (Layer by Layer)

**Before the data hits the wire, it is wrapped in headers at each layer of the stack:**

**Transport (TCP):** A segment is created with Source Port 50,000, Destination Port 80, and the SYN flag set.

**Network (IP):** The segment is placed in a datagram with Source IP 10.1.1.100, Destination IP 172.16.1.100, and a TTL of 64.

**Data Link (Ethernet):** The datagram is placed in a frame with Computer 1’s MAC as source and Router A’s MAC as the destination.

### Images (Phase 2)

#### Image 12 — TCP Segment Created
![Phase 2 - TCP Segment Created](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-12-TCP-Segment-Created.jpg)

#### Image 13 — IP Packet Created
![Phase 2 - IP Packet Created](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-13-IP-Packet-Created.jpg)

#### Image 14 — IP and TCP Encapsulation
![Phase 2 - IP and TCP Encapsulation](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-14-IP-and-TCP-Encapsulation.jpg)

#### Image 15 — Ethernet Frame Created
![Phase 2 - Ethernet Frame Created](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-15-Ethernet-Frame-Created.jpg)

#### Image 16 — Ethernet, IP, and TCP Ready to Send
![Phase 2 - Ethernet IP TCP Ready to Send](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-16-Ethernet-IP-TCP-Ready-to-Send.jpg)

---

## Phase 3: Routing (Router A → Router B)

**Routers act as the middlemen that bridge different networks.**

**De-encapsulation:** Router A receives the frame, verifies the checksum, and strips the Ethernet header to look at the IP datagram.

**Routing Table Lookup:** It sees the destination 172.16.1.0/24 is reachable via Router B (192.168.1.1).

**TTL Decrement:** The router reduces the Time To Live (TTL) by 1 and recalculates the checksum.

**Re-encapsulation:** Router A creates a new Ethernet frame using Router B’s MAC address as the destination.

### Images (Phase 3)

#### Image 17 — Frame Leaves Client to Router A
![Phase 3 - Frame Leaves Client to Router A](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-17-Frame-Leaves-Client-to-Router-A.jpg)

#### Image 18 — Router A Receives Frame
![Phase 3 - Router A Receives Frame](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-18-Router-A-Receives-Frame.jpg)

#### Image 19 — Router A Processes IP (TTL 64)
![Phase 3 - Router A Processes IP TTL 64](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-19-Router-A-Processes-IP-TTL-64.jpg)

#### Image 20 — Router A Decrements TTL and Updates Checksum
![Phase 3 - Router A Decrements TTL and Updates Checksum](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-20-Router-A-Decrements-TTL-and-Updates-Checksum.jpg)

#### Image 21 — Router A Builds New Frame to Router B
![Phase 3 - Router A Builds New Frame to Router B](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-21-Router-A-Builds-New-Frame-to-Router-B.jpg)

#### Image 22 — Router A Forwards to Router B
![Phase 3 - Router A Forwards to Router B](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-22-Router-A-Forwards-to-Router-B.jpg)

---

## Phase 4: Final Delivery (Router B → Computer 2)

**Arrival at Router B:** Router B receives the frame from Router A and strips the Ethernet header to inspect the IP packet.

**TTL Decrement:** Router B decrements the TTL and updates the IP header checksum.

**Local Delivery Decision:** Router B identifies that 172.16.1.100 belongs to its directly connected network (Network C).

**Re-encapsulation:** Router B builds a new Ethernet frame for the final hop to Computer 2.

**Verification:** Computer 2 verifies Ethernet, IP, and TCP checksums.

**Socket Match:** The OS identifies Port 80 and matches it to a socket in the LISTEN state (Apache).

**State Tracking:** Computer 2 records the TCP sequence number from the SYN packet to prepare the SYN-ACK response.

### Images (Phase 4)

#### Image 23 — Router B Receives IP/TCP
![Phase 4 - Router B Receives IP TCP](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-23-Router-B-Receives-IP-TCP.jpg)

#### Image 24 — Router B Validates Destination IP
![Phase 4 - Router B Validates Destination IP](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-24-Router-B-Validates-Destination-IP.jpg)

#### Image 25 — Router B Builds Frame to Server
![Phase 4 - Router B Builds Frame to Server](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-25-Router-B-Builds-Frame-to-Server.jpg)

#### Image 26 — Packet Delivered to Server
![Phase 4 - Packet Delivered to Server](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-26-Packet-Delivered-to-Server.jpg)

#### Image 27 — Server Validates TCP Checksum and Sequence
![Phase 4 - Server Validates TCP Checksum and Sequence](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-27-Server-Validates-TCP-Checksum-and-Sequence.jpg)

---

## Professional Troubleshooting Insight

This scenario highlights why pinging is so useful. If **the user can ping Computer 2 from Computer 1**, it confirms that **Layers 1–3 (Physical, Data Link, and Network)** and all routing hops in between are functioning correctly.

If the web page still does not load, the user can focus troubleshooting on:

- **Layer 4** (for example, **Port 80 blocked by a firewall**)
- **Layer 7** (for example, the **Apache service is not running or has crashed**)

---

## Where:

### Default gateway routing

**If the destination IP is outside the local subnet, the computer sends traffic to its default gateway for routing to other networks.**

**Example:** Computer 1 sees 172.16.1.100 is not in 10.1.1.0/24, so it forwards the packet to gateway 10.1.1.1.

### ARP (Address Resolution Protocol)

**ARP maps a local IP address to a MAC address so Ethernet frames can be delivered on the local network.**

**Example:** Computer 1 broadcasts an ARP request for 10.1.1.1 and Router A replies with MAC 00:11:22:33:44:55.

### Ephemeral port + socket (client side)

**The OS selects a temporary high-numbered port (ephemeral port) and opens a socket so the client application can establish a TCP connection.**

**Example:** Computer 1 selects ephemeral port 50,000 and opens a socket for the web browser.

### TCP SYN segment (connection start)

**TCP begins a connection by sending a SYN segment with source/destination ports, sequence number, and checksum.**

**Example:** Computer 1 sends TCP SYN from port 50,000 to destination port 80.

### IP datagram creation (Network layer encapsulation)

**The IP layer wraps the TCP segment inside an IP header containing source IP, destination IP, and TTL.**

**Example:** IP header includes source 10.1.1.100, destination 172.16.1.100, TTL 64.

### Ethernet frame creation (Data Link encapsulation)

**Ethernet wraps the IP datagram into a frame using source and destination MAC addresses for delivery on the local link.**

**Example:** Destination MAC is Router A’s MAC 00:11:22:33:44:55 so the frame reaches the gateway.

### Switch forwarding (Layer 2 delivery)

**A switch forwards frames based on the destination MAC address to the correct port.**

**Example:** The switch sends the frame only to the interface connected to Router A.

### Router processing (decapsulation + routing decision)

**Routers remove the Ethernet frame, inspect the IP header, validate checksums, and forward the packet toward the destination network.**

**Example:** Router A strips Ethernet, checks IP, and routes toward 172.16.1.0/24 via Router B (192.168.1.1).

### TTL decrement + checksum update

**Each router reduces the IP TTL by 1 and recalculates the IP header checksum before forwarding.**

**Example:** Router A decrements TTL (64 → 63), Router B decrements again (63 → 62).

### Re-encapsulation at each hop

**Every time a packet crosses into a new network segment, it is placed into a new Ethernet frame with new source/destination MAC addresses.**

**Example:** Router A builds a new frame on Network B to Router B; Router B builds a new frame on Network C to Computer 2.

### Server port listening (destination socket)

**The server delivers TCP traffic to the correct application by checking if a socket is listening on the destination port.**

**Example:** Computer 2 receives destination port 80 and confirms Apache is listening in the LISTEN state.

### TCP connection handshake repetition across the path

**Every step of encapsulation, switching, routing, and checksum validation happens again for SYN/ACK and ACK packets during the handshake.**

**Example:** SYN travels to Computer 2, then SYN/ACK travels back to Computer 1, then ACK travels again to Computer 2.

---

## **Project Credit**

- **Executed and Presented By:** Mohammad Aminul Islam _(SOC Analyst)_
- **Project Reference Source:** _The Bits and Bytes of Computer Networking_ — Google IT Support Professional Certificate Program _(Coursera)_
- **Project Implementation and Documentation:** Mohammad Aminul Islam
- **Copyright and Trademarks:** © 2022 Google LLC. Google and the Google logo are trademarks of Google LLC. All other product and company names may be trademarks of their respective owners.

---
