# Transport and Application Layers

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00a-Transport-and-Application-Layers.png)

---

**Transport layer:** Allows traffic to be directed to specific network applications.  
**Example:** TCP uses port 443 to send incoming data to a web browser handling HTTPS traffic.

**Application layer:** Allows applications to communicate in a way they understand.  
**Example:** HTTP defines how a web browser and a web server request and deliver web pages.

---

# The Transport Layer

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00b-Multiplex-and-Demultiplex-01.jpg)

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00c-Multiplexing-and-Demultiplexing-02.jpg)

**Transport layer:** Provides reliable communication by managing multiplexing, demultiplexing, connection handling, and data integrity through error checking and verification.  
**Example:** TCP establishes long-running connections and verifies data delivery.

**Multiplexing:** Allows a single networked device to send traffic to multiple services simultaneously.  
**Example:** One server handling web, email, and file transfer services at the same time.

**Demultiplexing:** Directs incoming traffic destined for one device to the correct receiving service.  
**Example:** Incoming packets are delivered to the correct application based on port number.

**Ports:** 16-bit numbers used by the transport layer to identify specific services on a computer.  
**Example:** HTTP uses port 80; FTP uses port 21.

**Server (service):** A program that runs on a computer and waits for incoming network requests.  
**Example:** A web server waiting for HTTP requests on port 80.

**Client:** A program that initiates a request for data from a server.  
**Example:** A web browser requesting a web page from a web server.

**Socket address (socket number):** A combination of an IP address and a port number that uniquely identifies a network service.  
**Example:** 10.1.1.100:80 identifies a web server running on that host.

**Server and client model:** Servers listen on specific ports for requests, while clients initiate connections to those ports.  
**Example:** A web browser (client) requests a webpage from a web server (server) listening on port 80.

**Multi-service servers:** A single computer can host many services simultaneously due to ports and multiplexing.  
**Example:** One server running a website, email server, file server, and print server at the same time.

**Practical implication:** A single physical server can host many network services simultaneously due to transport-layer multiplexing and demultiplexing.  
**Example:** One machine acting as a web server, mail server, file server, and print server.

---

# Dissection of a TCP Segment

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00e-TCP-Segments-.png)

## Encapsulation Context

To understand the TCP segment, we must look at how it fits into the overall data package:

- **Ethernet Frame:** Encapsulates the IP Datagram.
- **IP Datagram:** Encapsulates the TCP Segment.
- **TCP Segment:** Consists of the TCP Header and the Data Section (Application Layer payload).

## TCP Segment

A TCP segment is the transport-layer unit responsible for reliable, ordered, and verified data delivery.  
**Example:** A web page is broken into multiple TCP segments before being sent across the network.

## TCP Header

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00d-TCP-Header.jpg)

The TCP header contains control and management fields required for connection handling, sequencing, flow control, and integrity checking.  
**Example:** Sequence numbers and acknowledgments ensure data arrives in order and without loss.

| Field | Description | Technical Detail / Example |
|---|---|---|
| Source Port | A high-numbered ephemeral port chosen by the sender. | Ensures the response goes to the web browser, not a different app like Word. |
| Destination Port | The port of the service intended to receive the data. | e.g., Port 80 for a web server. |
| Sequence Number | A 32-bit number used to order segments. | Used to reassemble data split to fit the 1,518-byte Ethernet MTU. |
| Acknowledgment Number | The number of the next segment expected. | If Seq is 1, Ack is 2, meaning “I got 1, send me 2 next.” |
| Data Offset | A 4-bit field indicating the length of the TCP header. | Tells the receiver exactly where the data section (payload) begins. |
| TCP Window | A 16-bit number managing flow control. | Specifies how much data can be sent before waiting for an acknowledgment. |
| Checksum | A 16-bit integrity check. | Computed across the whole segment to detect corruption during transit. |

---

# TCP Control Flags and the Three-way Handshake

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00f-Three-Way-Handshake.jpg)

## TCP (Transmission Control Protocol): Purpose

TCP establishes reliable, connection-oriented communication to send long chains of data segments between applications.  
**Example:** A web browser maintains a TCP connection while loading a full webpage, unlike IP or Ethernet which send independent packets.

## TCP Control Flags: Manage connection behavior

TCP uses six control flags in its header to establish, maintain, and terminate connections.  
**Example:** SYN and ACK flags are exchanged to start a connection.

**URG (Urgent) flag:** Marks urgent data  
Indicates that a segment is urgent and that the urgent pointer field contains relevant information.  
**Example:** Rarely used in modern networks.

**ACK (Acknowledgment) flag:** Confirms received data  
Signals that the acknowledgment number field is valid and confirms receipt of data.  
**Example:** Every TCP segment received is acknowledged with an ACK.

**PSH (Push) flag:** Forces immediate delivery  
Requests the receiver to immediately pass buffered data to the application.  
**Example:** Sending a small command that requires an immediate response.

**RST (Reset) flag:** Resets a broken connection  
Indicates that the connection cannot recover due to missing or malformed segments and must restart.  
**Example:** Sent when unexpected or corrupted data is received.

**SYN (Synchronize) flag:** Initiates a connection  
Used during connection setup to synchronize sequence numbers.  
**Example:** First packet sent when opening a TCP connection.

**FIN (Finish) flag:** Closes a connection  
Indicates that the sender has no more data to transmit and wants to close the connection.  
**Example:** Sent when a file download is complete.

## The Three-Way Handshake (Establishing Connection)

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00g-SYN-ACK-Pairs.jpg)

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00j-SYN-ACK-Pairs-Ordered.jpg)

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00k-SYN-ACK-Pairs-Out-of-Order.jpg)

This process ensures both sides are ready and synchronized before data transfer begins.

- **SYN:** Computer A sends a SYN to Computer B (requesting a connection).
- **SYN/ACK:** Computer B responds with SYN and ACK (accepting the request and acknowledging A’s sequence).
- **ACK:** Computer A sends a final ACK (confirming the connection is open).

**Status:** Once complete, the connection is Full Duplex, meaning both sides can send and receive data simultaneously.  
**Example:** Happens every time a TCP connection is opened.

## The Four-Way Handshake (Closing Connection)

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00h-Four-Way-Handshake.jpg)

Closing a connection requires a separate goodbye from both sides to avoid cutting off data.

- **FIN:** Computer A signals it has finished sending data.
- **ACK:** Computer B acknowledges the request.
- **FIN:** Computer B signals it has also finished sending data.
- **ACK:** Computer A acknowledges the final closure.

**Example:** Occurs when a web session ends.

## Full Duplex Communication

After connection establishment, both devices can transmit data at the same time.  
**Example:** A client sends requests while receiving responses simultaneously.

---

# Connection-Oriented vs. Connectionless

- **TCP:** A connection-oriented protocol that tracks the entire conversation from start to finish using handshakes and acknowledgments.
- **Comparison:** IP and Ethernet are connectionless and simply deliver packets without tracking state.

**Example:** TCP ensures reliable file transfer, while IP just moves packets without guarantees.

---

# TCP Socket States

## Understanding Sockets vs. Ports

- **Socket**  
  The instantiated endpoint of a TCP connection created by an actual program. A socket represents a real, active communication point.  
  **Example:** A web server process opens a socket on port 80 to accept HTTP requests.

- **Port**  
  A virtual identifier used to route traffic to a service. A port alone does nothing unless a program has opened a socket on it.  
  **Key Distinction:** Traffic can be sent to any port, but communication only occurs if a socket is actively listening.  
  **Example:** Sending traffic to port 22 only works if an SSH service has opened a socket on that port.

- **Port vs Socket**  
  A port is a virtual descriptor, while a socket exists only when a program actively opens it.  
  **Example:** Sending traffic to port 22 produces a response only if an SSH service has opened a socket on that port.

## Common TCP Socket States (Troubleshooting-Oriented)

- **LISTEN (Server)**  
  The socket is open and waiting for incoming connection requests.  
  **Professional Context:** If a service is not in LISTEN, clients will receive “Connection Refused.”

- **SYN_SENT (Client)**  
  The client has sent a SYN request and is waiting for a SYN/ACK response.  
  **Professional Context:** If stuck here, the server may be unreachable or a firewall may be blocking the connection.

- **SYN_RECEIVED (Server)**  
  A SYN has been received and a SYN/ACK sent, but the final ACK has not arrived.  
  **Professional Context:** Common during SYN flood attacks or unreliable network conditions.

- **ESTABLISHED (Client and Server)**  
  The three-way handshake is complete and data transfer is active.  
  **Professional Context:** This is the normal, healthy state of an active TCP connection.

- **FIN_WAIT (Client or Server)**  
  A FIN has been sent to close the connection, but the peer’s ACK has not yet been received.  
  **Professional Context:** Indicates an orderly shutdown is in progress.

- **CLOSE_WAIT (Client or Server)**  
  The TCP connection is closed, but the application has not released the socket.  
  **Professional Context:** Large numbers of sockets in CLOSE_WAIT often indicate application bugs or resource leaks.

- **CLOSED (Client and Server)**  
  The connection is fully terminated and the socket resources are released.  
  **Professional Context:** The socket is free for reuse by the operating system.

## Operating System Variations

- **Non-Universal Naming**  
  TCP behavior is universal, but socket state names and representations can vary by operating system.  
  **Example:** Linux, Windows, and macOS may display slightly different state labels.

- **Troubleshooting**  
  Always confirm socket state definitions using OS-specific tools such as netstat or ss.

- **TIME_WAIT State**  
  TIME_WAIT ensures delayed packets are handled before fully closing a connection.  
  **Operational Insight:** This is normal behavior but can cause port exhaustion on high-traffic systems if not properly managed.

---

# Connection-oriented and Connectionless Protocols

## Connection-Oriented Protocols (TCP)

**Definition:**  
TCP is a connection-oriented transport layer protocol designed to provide reliable, ordered, and error-checked delivery of data.

**Reliability:**  
TCP ensures that data arrives intact and in the correct order, even under adverse network conditions such as congestion or physical link failures. This reliability is achieved through acknowledgments, retransmissions, and sequencing.

**Acknowledgment (ACK) Mechanism:**  
Every TCP segment sent must be acknowledged by the receiving host. Missing acknowledgments indicate data loss and trigger retransmission.  
**Example:** If a segment is dropped due to congestion, TCP resends it after detecting the missing ACK.

**Error Handling at Layer 4:**  
Lower layers (Ethernet and IP) use checksums to detect corrupted data but simply discard invalid packets. TCP, operating at the transport layer, is responsible for detecting missing data and retransmitting it.  
**Example:** An IP packet that fails a checksum is dropped; TCP later resends the missing segment.

**Sequencing:**  
Because packets may arrive out of order, TCP uses sequence numbers to correctly reassemble data into its original form.  
**Example:** File download packets arriving in mixed order are reordered using sequence numbers.

**Trade-off (Overhead):**  
TCP reliability introduces overhead due to connection setup, constant acknowledgments, and connection teardown.  
**Example:** The three-way handshake and ACK traffic consume bandwidth but ensure data integrity.

## Connectionless Protocols (UDP)

**Definition:**  
UDP (User Datagram Protocol) is a connectionless transport layer protocol that prioritizes speed and efficiency over guaranteed delivery.

**“Fire and Forget” Model:**  
UDP does not establish connections and does not use acknowledgments. Data is sent without confirmation of receipt.  
**Example:** A UDP datagram is sent directly to a destination port without any handshake.

**No Retransmission:**  
Lost or corrupted packets are not resent. Reliability is left to the application, if needed.  
**Example:** A missing video frame is skipped rather than retransmitted.

**Efficiency:**  
By eliminating connection management and acknowledgments, UDP maximizes available bandwidth for payload data.  
**Example:** High-bitrate streaming benefits from reduced protocol overhead.

## Technical Comparison & Professional Use Cases

| Feature | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
|---|---|---|
| Connection Type | Connection-oriented | Connectionless |
| Reliability | Guaranteed, ordered delivery | Best-effort delivery |
| Retransmission | Yes | No |
| Overhead | High (handshakes, ACKs) | Low |
| Typical Use Case | Web traffic (HTTP, SMTP, FTP) | Streaming, VoIP, online gaming |

---

# Supplemental Reading for System Ports versus Ephemeral Ports

## TCP Ports and Sockets

**Transport Layer Role**  
At the Transport Layer, TCP segments manage the lifecycle of a connection by defining how data reaches a specific program.  
**Example:** TCP ensures that web traffic reaches a browser and not another application.

**Port**  
A port is a virtual 16-bit identifier used to direct network traffic to a specific service.  
**Example:** Port 80 directs traffic to an HTTP web service.

**Socket**  
A socket is an active port that has been instantiated (opened) by a service to listen for incoming requests. It represents the live implementation of a port.  
**Example:** A web server opens a socket on port 443 to accept HTTPS connections.

**TCP Reliability**  
TCP ensures data integrity through acknowledgments (confirming receipt) and checksums (verifying data was not corrupted in transit).  
**Example:** If a segment fails checksum validation, TCP resends it.

## Port Categories (IANA Standards)

The 65,535 available ports are categorized by the Internet Assigned Numbers Authority (IANA) to maintain consistency across the global Internet.

**System Ports (1–1023)**  
Reserved for core, well-known services.  
**Technical Detail:** Modern operating systems do not use system ports for outbound traffic.  
**Example:** FTP (21), HTTP (80).

**User Ports (1024–49151)**  
Registered by vendors for specific applications and services.  
**Example:** Vendor-specific application servers registered by companies such as Google, Microsoft or Valve.

**Ephemeral Ports (49152–65535)**  
Temporary, dynamically assigned ports used only by clients for private transfers.  
**Example:** A web browser uses an ephemeral port to connect to a server on port 443.

## Network Security and Ports

From an IT support and security perspective, ports are a primary attack vector.

**Port Scanning**  
A technique used by malicious actors to probe a range of ports to identify open or unsecured services.  
**Example:** An attacker scans ports 1–1023 to locate exposed system services.

**Malware Vector**  
Open, unprotected sockets can be exploited to inject malicious code into client or server programs.  
**Example:** An unsecured service listening on an unnecessary port.

**Port Security**  
Open ports can be exploited by attackers to deliver malware or probe for vulnerabilities.  
**Example:** A firewall blocks unused ports to prevent unauthorized access.

**Professional Mitigation**  
Use a firewall to strictly control which ports are open and ensure only necessary sockets are active.  
**Example:** Allow port 443 while blocking all unused inbound ports.

**Professional Context**  
**Principle of Least Privilege (Ports)**  
When hardening a system, close all ports by default and open only those explicitly required.  
**Example:** If a server is not intended to host a website, port 80 should be blocked, not merely unused.

---

# Firewalls

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00l-Firewall.jpg)

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00m-Built-in-Firewall.jpg)

**Firewall:** A device or program that blocks or allows network traffic based on defined criteria.  
**Example:** Blocking unwanted inbound traffic to protect a private network.

**Role of firewalls in security:** Firewalls are a primary mechanism for preventing unauthorized traffic from entering a network.  
**Example:** Stopping external users from accessing internal services.

**Firewall operation layers:** Firewalls can operate at multiple layers of the network stack, including the application layer and transport layer.  
**Example:** Inspecting application data or blocking traffic from specific IP address ranges.

**Transport-layer firewalls:** Most commonly used to allow or block traffic based on port numbers.  
**Example:** Allowing traffic on port 80 while blocking traffic on all other ports.

**Firewall placement:** Firewalls can be deployed at the network perimeter, on routers, or directly on individual hosts.  
**Example:** A home router acting as both router and firewall, or an operating system firewall blocking local ports.

## Host-Based Firewalls

Host-based firewalls are software firewalls built into modern operating systems and protect individual machines.  
**Example:** Windows Firewall blocking unauthorized inbound connections to a laptop.

## Network Layer Filtering

Controls traffic based on IP addresses or IP ranges.  
**Example:** Blocking traffic from known malicious IP addresses.

## Transport Layer Filtering

Controls traffic based on TCP or UDP port numbers.  
**Example:** Allowing email traffic on port 25 while blocking unused ports.

## Application Layer Inspection

Performs deep packet inspection to analyze actual data payloads for malicious content.  
**Example:** Detecting malware hidden inside HTTP traffic.

---

# The Application Layer

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00i-Application-Networking-Between-Server-and-Browse.jpg)

## The Role of the Application Layer

The Application Layer is where the actual work happens from a user perspective. It provides the interface through which programs (such as web browsers or email clients) access network services.  
**Example:** A web browser requesting a webpage from a web server.

## The Final Payload

The Application Layer generates the data that eventually becomes the data section (payload) of a TCP or UDP segment.  
**Example:** HTML content, video stream data, or a print document.

## Diverse Utility of the Application Layer

This layer supports a wide range of user-facing functions.  
**Example:**
- Streaming video (Netflix)
- Web content delivery
- File transfers
- Printing documents over a network

## Interoperability and Standardization

Unlike lower layers that rely on a few dominant protocols, the Application Layer contains thousands of protocols. These must be strictly standardized to ensure global interoperability.  
**Example:** Software from different vendors can communicate as long as they follow the same protocol specifications.

## The Concept of Interoperability

Interoperability allows different applications, built by different vendors, to communicate correctly by following shared protocol rules.  
**Example:** Any standards-compliant browser can communicate with any standards-compliant web server.

## Web Traffic Example

- **Clients:** Chrome, Safari, Firefox, Edge  
- **Servers:** Apache, Nginx, Microsoft IIS  
- **Protocol:** HTTP (Hypertext Transfer Protocol)  
- **Key Point:** Because HTTP is standardized, any browser can communicate with any web server.

## File Transfer Example

Many FTP clients exist, but they all communicate using the same standardized FTP protocol.  
**Example:** Different FTP applications connecting to the same FTP server.

## Protocol Stack Summary (5-Layer Model)

| Layer | Primary Function | Common Protocols |
|---|---|---|
| Application | Application-to-Application communication | HTTP, FTP, SMTP, DNS |
| Transport | Process-to-Process communication (Ports) | TCP, UDP |
| Network | Host-to-Host communication (Routing) | IP |
| Data Link | Node-to-Node communication (MAC) | Ethernet, Wi-Fi |
| Physical | Bit-to-Bit transmission | 10BASE-T, 802.11 |

## Professional Application (IT Support)

Understanding the Application Layer helps distinguish network issues from software issues.  
**Example:**
- Ping succeeds → Layers 1–3 are working
- Port is open → Layer 4 is working
- Webpage still fails → Application Layer issue (misconfigured web server or protocol handling bug)

---

# The Application Layer and the OSI Model

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00n-OSI-Model.jpg)

![](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-03-00o-OSI-Vs-TCP-IP.jpg)

## The OSI Model (Open Systems Interconnection)

The OSI model is a seven-layer networking framework that is more rigorously defined than the five-layer model. It is commonly used in academic environments and professional networking certifications.

## The Additional Layers in the OSI Model

While the five-layer model groups everything above the Transport layer into a single Application layer, the OSI model separates these responsibilities into three distinct layers.

### Layer 5: Session Layer

**Function:** Facilitates communication between applications and the transport layer.

**Technical Role:**  
The session layer manages the lifecycle of a communication session, including starting, maintaining, and restarting conversations. It takes unencapsulated data from lower layers and hands it off to the presentation layer.

### Layer 6: Presentation Layer

**Function:** Ensures that data is in a format the application can understand.

**Technical Role:**  
This layer handles data transformation tasks such as encryption, decryption, and compression. It acts as a translator between the raw data and the application.

### Layer 7: Application Layer

**Function:** Provides the interface where the actual application interacts with network data.

**Example:**  
Web browsers, email clients, and FTP clients operate at this layer.

## Comparison: 5-Layer vs. 7-Layer (OSI)

The primary difference lies in how the top-level functions are categorized.

| 5-Layer Model | OSI (7-Layer) Model | Key Functions |
|---|---|---|
| Application | 7. Application | User interface, HTTP, FTP |
|  | 6. Presentation | Encryption, Compression |
|  | 5. Session | Hand-offs, Session management |
| Transport | 4. Transport | TCP/UDP, Ports, Error checking |
| Network | 3. Network | IP, Routing |
| Data Link | 2. Data Link | Ethernet, MAC addresses |
| Physical | 1. Physical | Cables, Bits, Electrical signals |

## Why Use the Five-Layer Model?

Although the OSI model is precise, it can be overly complex for day-to-day IT support tasks.

**Encapsulation:**  
Layers 5, 6, and 7 do not add new headers, meaning no additional encapsulation occurs at these levels.

**Practicality:**  
In modern operating systems, session management and encryption are typically handled by applications or OS libraries. Grouping these functions into a single application layer simplifies troubleshooting.

---

# All the Layers Working in Unison

## End-to-end web request (Computer 1 → Computer 2)

**A full network communication requires every layer (Physical → Data Link → Network → Transport → Application) to work together to deliver a TCP segment from a client to a server.**  
**Example:** Computer 1 (10.1.1.100) opens a browser to reach Computer 2 (172.16.1.100:80) across Router A and Router B.

**Default gateway routing**  
**If the destination IP is outside the local subnet, the computer sends traffic to its default gateway for routing to other networks.**  
**Example:** Computer 1 sees 172.16.1.100 is not in 10.1.1.0/24, so it forwards the packet to gateway 10.1.1.1.

**ARP (Address Resolution Protocol)**  
**ARP maps a local IP address to a MAC address so Ethernet frames can be delivered on the local network.**  
**Example:** Computer 1 broadcasts an ARP request for 10.1.1.1 and Router A replies with MAC 00:11:22:33:44:55.

**Ephemeral port + socket (client side)**  
**The OS selects a temporary high-numbered port (ephemeral port) and opens a socket so the client application can establish a TCP connection.**  
**Example:** Computer 1 selects ephemeral port 50,000 and opens a socket for the web browser.

**TCP SYN segment (connection start)**  
**TCP begins a connection by sending a SYN segment with source/destination ports, sequence number, and checksum.**  
**Example:** Computer 1 sends TCP SYN from port 50,000 to destination port 80.

**IP datagram creation (Network layer encapsulation)**  
**The IP layer wraps the TCP segment inside an IP header containing source IP, destination IP, and TTL.**  
**Example:** IP header includes source 10.1.1.100, destination 172.16.1.100, TTL 64.

**Ethernet frame creation (Data Link encapsulation)**  
**Ethernet wraps the IP datagram into a frame using source and destination MAC addresses for delivery on the local link.**  
**Example:** Destination MAC is Router A’s MAC 00:11:22:33:44:55 so the frame reaches the gateway.

**Switch forwarding (Layer 2 delivery)**  
**A switch forwards frames based on the destination MAC address to the correct port.**  
**Example:** The switch sends the frame only to the interface connected to Router A.

**Router processing (decapsulation + routing decision)**  
**Routers remove the Ethernet frame, inspect the IP header, validate checksums, and forward the packet toward the destination network.**  
**Example:** Router A strips Ethernet, checks IP, and routes toward 172.16.1.0/24 via Router B (192.168.1.1).

**TTL decrement + checksum update**  
**Each router reduces the IP TTL by 1 and recalculates the IP header checksum before forwarding.**  
**Example:** Router A decrements TTL (64 → 63), Router B decrements again (63 → 62).

**Re-encapsulation at each hop**  
**Every time a packet crosses into a new network segment, it is placed into a new Ethernet frame with new source/destination MAC addresses.**  
**Example:** Router A builds a new frame on Network B to Router B; Router B builds a new frame on Network C to Computer 2.

**Server port listening (destination socket)**  
**The server delivers TCP traffic to the correct application by checking if a socket is listening on the destination port.**  
**Example:** Computer 2 receives destination port 80 and confirms Apache is listening in the LISTEN state.

**TCP connection handshake repetition across the path**  
**Every step of encapsulation, switching, routing, and checksum validation happens again for SYN/ACK and ACK packets during the handshake.**  
**Example:** SYN travels to Computer 2, then SYN/ACK travels back to Computer 1, then ACK travels again to Computer 2.

---

# Glossary terms

## The Transport Layer (Layer 4)

**Transport Layer:** Enables process-to-process communication by directing traffic to the correct application using ports, and (with TCP) supporting reliability and integrity.  
**Example:** A browser connects to a web server by targeting destination port 80 (HTTP) or 443 (HTTPS).

### Key Protocols

**TCP (Transmission Control Protocol):** Connection-oriented; uses a handshake, sequence numbers, acknowledgments (ACKs), and checksums to ensure reliable delivery.  
**Example:** Web browsing over TCP uses SYN → SYN/ACK → ACK to establish a connection, then ACKs confirm received segments.

**UDP (User Datagram Protocol):** Connectionless; sends datagrams without acknowledgments or connection state, reducing overhead.  
**Example:** Streaming video can use UDP so occasional packet loss does not interrupt playback as severely.

### Ports and Sockets

**Port:** A 16-bit identifier (0–65535) used to direct network traffic to a specific service.  
**Example:** Port 80 is traditionally used for HTTP.

**Socket:** An active endpoint instantiated by a program; often represented as IP address + port (and protocol).  
**Example:** 10.1.1.100:50000 (client ephemeral port) connecting to 172.16.1.100:80 (web server).

**Multiplexing/Demultiplexing:** Transport-layer capability to handle multiple services on one host by mapping traffic to ports.  
**Example:** One server can run HTTP on port 80 and FTP on port 21 at the same time.

### TCP Control Flags (“Signals”)

**SYN:** Initiates a TCP connection and synchronizes sequence numbers.  
**Example:** Client sends SYN to begin the three-way handshake.

**ACK:** Confirms receipt and indicates the acknowledgment number is valid.  
**Example:** Server replies with SYN/ACK to acknowledge the client’s SYN.

**FIN:** Gracefully closes a TCP connection.  
**Example:** A client sends FIN when it has no more data to send.

**RST:** Resets the connection due to errors or an invalid state.  
**Example:** A host sends RST if a segment arrives for a socket that is not open.

**PSH:** Requests immediate delivery of buffered data to the receiving application.  
**Example:** A small interactive message is sent with PSH to reduce perceived latency.

---

## Connection States (Troubleshooting Reference)

**LISTEN:** Server socket is waiting for incoming connections.  
**Example:** A web server is listening on port 80.

**SYN_SENT:** Client sent SYN and is waiting for SYN/ACK.  
**Example:** Client initiated the connection but it is not established yet.

**SYN_RECEIVED:** Server received SYN and sent SYN/ACK; waiting for final ACK.  
**Example:** Server is one step away from ESTABLISHED.

**ESTABLISHED:** Connection is active; both sides can exchange data.  
**Example:** Browser downloads a webpage after the handshake completes.

**FIN_WAIT / CLOSE_WAIT:** Shutdown in progress (FIN and ACK exchange occurring, or app not releasing socket).  
**Example:** A connection appears “stuck” if the app holds the socket in CLOSE_WAIT.

**CLOSE/CLOSED:** Connection fully terminated; no further communication possible.  
**Example:** Socket is removed from active state tables.

---

## The Application Layer (Layer 5 in 5-layer model / Layer 7 in OSI)

**Application Layer:** Defines how applications exchange data in a mutually understood format.  
**Example:** HTTP defines requests/responses between browser (client) and web server (server).

**Application Layer Payload:** The actual content applications want to send.  
**Example:** HTML, images, or streaming media data carried inside TCP/UDP payloads.

**Interoperability:** Standard protocols ensure different implementations can communicate.  
**Example:** Chrome can talk to Apache or nginx because all implement HTTP.

### OSI Model Extensions (between Transport and Application)

**Session Layer (OSI Layer 5):** Facilitates managing the communication session between applications and transport.  
**Example:** Coordinates the “dialogue” and session continuity between endpoints.

**Presentation Layer (OSI Layer 6):** Ensures application data is in a usable form (formatting, encryption, compression).  
**Example:** Data is decrypted or decompressed before the application processes it.

---

## Security: The Firewall

**Firewall:** A device or software that allows or blocks traffic based on rules, commonly using ports at the transport layer.  
**Example:** Allow inbound port 80 for a public website, but block inbound access to other ports from external IPs.

---

## Foundational Review (Layers 1–3)

**Physical Layer:** Moves bits over physical media (copper/fiber) using electrical or optical signaling.  
**Example:** Voltage modulation on a Cat6 cable transmits 1s and 0s.

**Data Link Layer:** Handles local delivery using frames and MAC addresses; includes mechanisms like ARP for IP-to-MAC resolution.  
**Example:** ARP finds the gateway MAC address so a host can send an Ethernet frame to it.

**Network Layer:** Routes IP datagrams across networks using routers and routing tables; TTL limits hop count.  
**Example:** Routers decrement TTL and forward packets toward the destination network.
