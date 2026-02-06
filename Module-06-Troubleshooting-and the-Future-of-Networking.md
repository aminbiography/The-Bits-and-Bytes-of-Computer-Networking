# Network Reliability, Troubleshooting, and Future Architectures

---

## Troubleshooting & Future of Networking

---

- **Networking Complexity**
  - Modern networks involve many layers, protocols, and devices → failures are normal.

- **Error Detection**
  - A mechanism used to identify that a problem has occurred.
  - **Example:** CRC (Cyclic Redundancy Check) verifies data integrity.

- **Error Recovery**
  - A mechanism used to correct or compensate for detected errors.
  - **Example:** The transport layer resends data if corruption or loss is detected.

- **CRC Behavior**
  - If CRC ≠ payload data → data is discarded.
  - Then transport layer decides on retransmission.

- **Common Causes of Network Issues**
  - Misconfigurations
  - Hardware failures
  - System incompatibilities
  - Data corruption

- **Troubleshooting Focus**
  - Learn standard techniques and tools.
  - Goal: Detect and fix common connectivity problems.

- **Key Operating Systems for Troubleshooting**
  - Windows
  - macOS
  - Linux

---

# ICMP & Ping

## Connectivity Troubleshooting

- Most common issue: cannot reach a host (server, website, Internet).
- ICMP helps diagnose why connectivity fails.

## ICMP (Internet Control Message Protocol)

- Network “feedback” protocol for error reporting.
- Used by routers/hosts to notify senders of failures.

### Common ICMP Messages

- **Destination Unreachable** — no route or host/port unreachable.
- **Time Exceeded** — TTL reached zero (loop prevention).
- **Port Unreachable** — target application port closed.

### ICMP Packet Fields

- **Type (8 bits):** Message category.
- **Code (8 bits):** Specific reason.
- **Checksum (16 bits):** Error check.
- **Rest of Header (32 bits):** Optional data.
- **Payload:** Original IP header + first 8 bytes of data.

## Ping Utility

- Human-usable ICMP tool to test reachability.
- Sends Echo Request and receives Echo Reply.

### Ping Shows

- Replying IP address
- Round-Trip Time (latency)
- TTL value
- Packet size
- Packet loss and averages

### OS Behavior

- **Windows:** 4 pings by default.
- **Linux/macOS:** Continuous until `Ctrl + C`.

### Ping Customization

Flags allow changes to:
- Packet count
- Packet size
- Send interval

Useful for latency tests and stability checks.

---

# Command Line Troubleshooting Tools

## Software & Hardware Troubleshooting

- **File operations**
  - `copy` / `cp` → basic file copy.
  - `xcopy` → copy with subdirectories and large-file support.
  - `robocopy` → secure, permission-preserving copy.

- **Disk & system health**
  - `chkdsk` / `fsck` → scan and repair file system errors.
  - `sfc` → repair corrupted Windows system files.
  - `format` → erase and reset a drive.
  - `diskpart` / `fdisk` → manage disk partitions.

- **System info**
  - `shutdown` → shutdown/restart systems (`/fw` to firmware).
  - `winver` → show Windows version.

## Networking Troubleshooting

- **Configuration & connectivity**
  - `ipconfig` / `ip` → view IP configuration (`/all` for details).
  - `ping` → test reachability and latency.
  - `tracert` / `traceroute` → view packet route.
  - `pathping` → detect packet loss per hop.
  - `hostname` → show device name.

- **Diagnostics**
  - `netstat` → show active connections and ports.
  - `nslookup` → query DNS records.

## User & Group Management

- **Users**
  - `net user` → add/modify/delete accounts.
  - `net use` → manage shared resource connections.

- **Group policy**
  - `gpupdate` → refresh policies.
  - `gpresult` → view applied policies (RSOP).

### Command Line Troubleshooting Tools Reference Guide (PDF)

- **PDF:** https://drive.google.com/file/d/1jbGWD9ilDyBpv7S2Gb15Nw08Uswf6hox/view?usp=sharing

---

# Traceroute

- **Purpose:** Shows the path to a destination and helps locate which router causes delay or failure.
  - Ping = reachability
  - Traceroute = path + latency per hop

- **Key Mechanism: TTL Manipulation**
  - Packets sent with TTL = 1, 2, 3…
  - Each router decrements TTL by 1.
  - TTL = 0 → router drops packet and returns ICMP Time Exceeded.

- **Hop Discovery Process**
  - TTL=1 reveals hop 1
  - TTL=2 reveals hop 2
  - Continues until destination replies.

- **Per-Hop Measurements**
  - Sends 3 probes per hop.
  - Displays hop number, RTT (latency), IP, and hostname (if resolved).
  - Multiple RTT values help detect jitter.

- **Platform Behavior**
  - Linux/macOS traceroute → UDP (high ports)
  - Windows tracert → ICMP Echo

- **Advanced Tools**
  - MTR: Real-time, continuous updates.
  - Pathping: Runs ~50s, then shows aggregated stats.

- **Why Use MTR/Pathping?**
  - Better for intermittent issues.
  - Reveal packet loss patterns over time (e.g., 10% drop at a router).

### Platform Differences and Advanced Tools

| OS / Tool                   | Protocol Used         | Continuous Monitoring?              |
|----------------------------|-----------------------|-------------------------------------|
| Linux/macOS (traceroute)   | UDP (high ports)      | No                                  |
| Windows (tracert)          | ICMP Echo Requests    | No                                  |
| MTR (Linux/macOS)          | ICMP or UDP           | Yes (Real-time updates)             |
| Pathping (Windows)         | ICMP                  | Yes (Runs for 50s, then aggregates) |

---

# Testing Port Connectivity

## Transport Layer Port Connectivity

- **Goal:** Verify if a specific service/port is reachable (Transport Layer), not just host reachability.

## Netcat (nc) — Linux/macOS

- “Swiss Army Knife” for TCP/UDP testing.
- Syntax: `nc host port` → attempts TCP connection.
- `-z` = scan mode (no data sent).
- `-v` = verbose, human-readable result.
- Common check: `nc -zv host port` → confirms open/closed port.
- Can also manually send data to services.

## Test-NetConnection — Windows (PowerShell)

- More detailed than ping.
- `Test-NetConnection host` → ICMP test + interface/source info.
- `-Port` flag → tests specific port.
- Key output: `TcpTestSucceeded` (True/False).
- Shows routing and link-layer details.

### Comparison of Tools

| OS          | Command             | Advantage                                                                 |
|-------------|---------------------|---------------------------------------------------------------------------|
| Linux/macOS | `nc`                | Extremely lightweight; can be used to send actual data to a port manually. |
| Windows     | `Test-NetConnection`| Provides detailed info about the Data Link layer and specific routing paths. |

## Testing Port Connectivity (Summary)

- Netcat (nc) and Test-NetConnection are tools for testing network connectivity and communication between devices.
- They operate at the transport layer, which manages connections and communication between hosts.
- These tools are used to check port connectivity on specific ports.
- They help verify whether services on certain ports are reachable.
- Reference guides provide commands and examples for testing different ports.

### Testing Port Connectivity (PDF)

- **PDF:** https://drive.google.com/file/d/1w4GgfP5VsXzMOjTOaWwONBS89vrSTNwt/view?usp=drive_link

---

# Name Resolution Tools (nslookup)

- Name resolution: Converts domain names to IP addresses; usually handled automatically by the OS.
- `nslookup`: Common command-line tool (Linux, macOS, Windows) to query DNS records.
- Basic use: `nslookup domain.com` → returns IP (A record) and DNS server used.
- Interactive mode: Run `nslookup` alone → allows multiple queries and settings.
- Change DNS server: `server <address>` → use a specific DNS server.
- Query record types: `set type=<record>` → e.g., A, AAAA, MX, TXT.
- Debug mode: `set debug` → shows full DNS response details (TTL, cache info, zone data).
- Use case: Helpful for DNS troubleshooting and verifying name resolution.

---

# Public DNS Servers

## Public DNS & Troubleshooting

- DNS = backbone of network usability  
  Translates names to IPs for both Internet and internal resources.

### DNS Service Models

- ISP DNS: Default, adequate for normal use
- Internal DNS: Resolves local devices (e.g., printers, laptops)
- DNS as a Service: Cloud-managed, high availability
- Public DNS: Free resolvers mainly for troubleshooting

### Key Public DNS Providers

- Google DNS: 8.8.8.8 / 8.8.4.4 (official, supported)
- Level 3: 4.2.2.1–4.2.2.6 (historically used, unofficial)

### Troubleshooting Tip

- If ping to 8.8.8.8 works but websites fail → likely DNS issue, not connectivity.

### Security Risks

- DNS hijacking can redirect users to malicious sites
- Use only reputable DNS providers

### Best Practice

- Use ISP/internal DNS for daily operations; public DNS as backup or for testing.

### Anycast

- Public DNS often uses anycast to route queries to the nearest server for lower latency.

---

# DNS Registration and Expiration

- DNS is globally managed in a hierarchy with ICANN at the top; domain names must be globally unique.
- A registrar is an organization that assigns domain names to individuals or businesses.
- Global Uniqueness: Domain names must be unique; the global DNS hierarchy coordinated by ICANN ensures no collisions.
- Registrars: ICANN-accredited companies that sell and manage domain registrations; today there are hundreds worldwide.

## Registration Workflow

- Check name availability
- Choose a fixed registration term (years)
- Pay to secure the domain

## Authoritative DNS Choice

- Registrar-managed: registrar hosts your DNS records
- Self-managed: point to your own authoritative name servers

## Domain Transfers

- Possible between owners or registrars
- Verified using an authorization string, often placed in a DNS TXT record

## Expiration

- Domains are leased, not owned permanently
- Non-renewal leads to expiration and public availability
- Risks include downtime, brand loss, and malicious reuse

---

# Hosts Files

- Hosts file = local name resolution file mapping IP addresses to hostnames (one line per mapping).  
  Example: `1.2.3.4 webserver`
- Processed by the OS networking stack, so mappings apply system-wide (browser, ping, etc.).
- Hosts file lookup happens before DNS, allowing manual override of DNS resolution.
- Local Impact: It only affects the device where it resides (not global like DNS).
- Resolution Order: The OS checks the hosts file before DNS. If a match exists, DNS is bypassed.

## Loopback & Localhost

- IPv4: 127.0.0.1 localhost
- IPv6: ::1 localhost
- Loopback traffic never leaves the device.

## Troubleshooting Uses

- Force domains to specific IPs for testing
- Temporary workaround for DNS failures
- Required by some legacy/specialized software

## Security Risk

- Malware can modify hosts files to redirect or block traffic (DNS hijacking).

## Modern Relevance

- Rarely used for general resolution today but still important for IT support and diagnostics.

---

# The Cloud

- Cloud computing = delivery model, not a single tech  
  Provides on-demand, shared access to compute (CPU), memory (RAM), storage, and services over a network.

## Foundation: Hardware Virtualization

- Host: Physical server supplying resources.
- Guest (VM): Virtual machine running its own OS on the host.
- Hypervisor: Software layer that creates and manages VMs, abstracting hardware from the OS.

## Core Idea

- Resource pooling: Many physical servers form clusters that share resources across many VMs.
- Decoupling: Logical servers are not tied to specific hardware.

## Why the Cloud (Efficiency)

- Traditional model requires buying for peak demand, causing idle resources.
- Cloud model allocates resources dynamically, improving utilization and reducing waste.
- Pay-as-you-use cost structure.

## Operational Benefits

- Rapid provisioning: Deploy servers in minutes via web console.
- Hardware transparency: Failures handled by migrating VMs to healthy hosts.
- Built-in services: Backup, load balancing, security, and monitoring.

## Cloud Deployment Models

| Model        | Description |
|-------------|-------------|
| Public Cloud | Resources are owned and operated by a third-party provider (e.g., AWS, Google Cloud) and shared among many different customers. |
| Private Cloud| Virtualization technology used exclusively by a single organization, typically hosted on their own physical premises. |
| Hybrid Cloud | A mix of both; sensitive data stays on a private cloud, while less sensitive or high-scale apps run on a public cloud. |

## Big Picture

- Cloud computing improves scalability, flexibility, and overall resource utilization while reducing capital and operational overhead.

---

# Everything as a Service

## XaaS (Everything as a Service)

- XaaS Concept
  - Cloud evolved from just VMs to layered services.
  - Lets organizations choose how much of the stack they manage.

## IaaS (Infrastructure as a Service)

- Provides: Virtual servers, storage, networking.
- User Manages: OS, applications, data, patches.
- Benefit: No physical hardware ownership.

## PaaS (Platform as a Service)

- Provides: Runtime platform (web server, DB, dev environment).
- User Manages: Application code and data.
- Benefit: Developers focus on coding, not infrastructure.

## SaaS (Software as a Service)

- Provides: Fully managed software via internet.
- User Role: Just use the app.
- Examples: Google Workspace, Microsoft 365, Salesforce.
- Benefit: No maintenance; subscription-based.

## Abstraction Progression

- IaaS → PaaS → SaaS  
  (Control decreases, convenience increases)

## Modern Network Impact

- Business networks increasingly exist mainly to provide reliable internet access for cloud services.

---

# Cloud Storage

- Cloud storage: A service where a provider stores customer data so it is secure, accessible, and available over the internet.
- Data types: Can store documents, media files, and large database backups.
- Reduced hardware burden: Provider manages physical storage hardware and failures.
- Geographic redundancy: Data can be replicated across regions for availability and disaster protection.
- Scalability: Storage grows with demand; users typically pay for what they use.
- Data protection: Distributed storage reduces risk of total data loss.
- Pay-as-you-go model: Users pay for actual usage, turning large capital costs into predictable operational costs.

## Common Use Cases

- Enterprise backups and archival
- Personal backups (photos, documents, device sync)

---

# IPv6 Addressing & Subnetting

- Why IPv6 exists
  - IPv4 = 32-bit → ~4.2B addresses → exhausted.
  - IPv6 = 128-bit → ~3.4×10³⁸ addresses.

- IPv5 Trivia
  - Experimental, connection-oriented.
  - Never widely adopted; name skipped for new protocol.

- IPv6 Format
  - Written as 8 groups of 16 bits (hexadecimal).
  - Example form: `xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx`

- Shortening Rules
  - Remove leading zeros in any group.
  - Replace consecutive zero groups with `::` (only once).

- Documentation Range
  - `2001:0db8::/32` reserved for docs and education.

- Loopback Address
  - IPv6 loopback = `::1`

- Special Ranges
  - `FF00::/8` → Multicast.
  - `FE80::/10` → Link-local unicast (auto-configured, local segment).

- Link-Local Addressing
  - Derived from MAC using algorithm (48-bit → 64-bit ID).
  - Used for local communication and auto-configuration.

- Reserved Ranges
  - `2001:db8::/32` → Documentation/education.
  - `FF00::/8` → Multicast.
  - `FE80::/10` → Link-local unicast (auto-configured, local segment).

- Address Structure
  - First 64 bits = Network ID
  - Last 64 bits = Host ID
  - One IPv6 network supports ~9 quintillion hosts.

- Subnetting
  - Uses CIDR notation.
  - `/64` is the standard subnet size.
  - No class-based addressing in IPv6.

---

# IPv6 Headers

- IPv6 header is simpler and more efficient than IPv4, designed to improve performance.
- Version (4 bits): Identifies IP version (IPv6).
- Traffic Class (8 bits): Indicates traffic type and priority for QoS.
- Flow Label (20 bits): Helps routers manage QoS for specific traffic flows.
- Payload Length (16 bits): Size of the data payload.
- Next Header: Points to the following header (extension or transport); enables optional header chaining.
- Hop Limit (8 bits): Same purpose as IPv4 TTL; decremented at each hop.
- Source & Destination Addresses: Each is 128 bits.
- Optional fields moved to extension headers to keep the main IPv6 header compact.

## IPv4 vs. IPv6 Header Comparison

| Feature        | IPv4 Header              | IPv6 Header                          |
|---------------|---------------------------|--------------------------------------|
| Address Size  | 32 bits                    | 128 bits                             |
| Header Size   | Variable (20–60 bytes)     | Fixed (40 bytes)                     |
| Lifespan Field| Time to Live (TTL)         | Hop Limit                            |
| Options       | Embedded in main header    | Abstracted into "Extension Headers"  |

---

# IPv6 and IPv4

- Full IPv6 switch is gradual: The Internet cannot move to IPv6 all at once due to legacy devices and infrastructure.
- Coexistence is required: IPv4 and IPv6 must operate together during transition.

## Transition Reality

- A full Internet-wide switch to IPv6 cannot happen at once due to legacy systems.
- Coexistence mechanisms allow gradual migration.

## IPv4-Mapped IPv6 Addresses

- Represent IPv4 addresses inside IPv6.
- Structure: 80 zeros + 16 ones (FFFF) + 32-bit IPv4 address.
- Example: `::ffff:192.168.1.1`
- Purpose: Lets IPv6 systems communicate with IPv4 nodes.

## IPv6 Tunneling

- Used when IPv6 traffic must cross IPv4 infrastructure.
- Method: Encapsulation of IPv6 packets inside IPv4 datagrams.
- Tunnel Servers: Handle encapsulation and de-encapsulation.

## Tunnel Brokers

- Third-party providers offering IPv6 tunnel endpoints.
- Remove need for in-house tunnel infrastructure.
- Transitional technology that will fade as IPv6 becomes native.

## Future Direction

- Goal: Native IPv6 networking.
- Long term: No need for tunnels or mapping.

## Summary of Transition Tools

| Technology          | Primary Function |
|--------------------|------------------|
| IPv4-Mapped Address| Represents an IPv4 address in an IPv6 format. |
| IPv6 Tunneling     | Encapsulates IPv6 packets to travel over IPv4 infrastructure. |
| Tunnel Broker      | A third-party service providing tunnel endpoints for easier adoption. |

---

# IPv6 and IPv4 Harmony

- IPv4 vs IPv6 size
  - IPv4 = 32-bit (~4.2 billion addresses)
  - IPv6 = 128-bit (~340 undecillion addresses)
  - IPv6 created to solve IPv4 exhaustion.

- Different “languages”
  - IPv4 and IPv6 datagrams have different structures.
  - They are not directly compatible.

- Why coexistence is needed
  - The Internet cannot switch to IPv6 all at once.
  - Many networks and devices still rely on IPv4.

- Tunneling concept
  - Carries IPv6 traffic over IPv4 networks.
  - IPv6 packets are encapsulated inside IPv4 datagrams.
  - Receiving tunnel server de-encapsulates and forwards IPv6 traffic.

- Common tunneling protocols
  - **6in4 (Manual)**
    - Direct IPv6-in-IPv4 encapsulation
    - Predictable, easy to debug
    - Often fails behind NAT
  - **TSP (Tunnel Setup Protocol)**
    - Negotiates tunnel parameters
    - Supports multiple methods
    - More flexible deployment
  - **AYIYA**
    - Encapsulates any protocol in any protocol
    - Good for tunnel brokers
    - Works well through NAT and dynamic IPs

## Common Tunneling Protocols (Trade-offs)

| Protocol | Mechanism | Key Advantage | Key Disadvantage |
|---------|-----------|---------------|------------------|
| 6in4 (Manual) | Direct encapsulation without extra headers. | High performance; easy to debug. | Does not work well with NAT; requires manual setup. |
| TSP (Tunnel Setup Protocol) | Negotiates parameters between endpoints. | Supports multiple encapsulation methods. | More complex setup than 6in4. |
| AYIYA (Anything in Anything) | Encapsulates any protocol within another. | Works behind NAT and with dynamic IP addresses. | Introduced for tunnel brokers; adds more overhead. |

- Key takeaway
  - Tunneling enables IPv6 adoption during the transition from IPv4.
  - Multiple protocols exist, each with trade-offs.

---

# Top Professionally Used Networking Terms

## Core Network Services

- **DNS (Domain Name System):** Resolves names ↔ IPs; foundational for almost all services.
- **DHCP:** Automatic IP configuration (IP, gateway, DNS).
- **NTP servers:** Time synchronization across systems (vital for security/logging).
- **ISP:** Upstream Internet connectivity provider.

## DNS Operations (Very Common in Practice)

- **A / AAAA records:** Map names to IPv4/IPv6.
- **CNAME:** Alias one name to another.
- **MX record:** Directs email delivery.
- **NS record:** Delegates DNS authority.
- **TXT record:** Verification, SPF, DKIM, policies.
- **FQDN:** Full domain path used in configs and certs.
- **TTL (DNS):** Cache lifetime for records.
- **Zone files:** Authoritative DNS configurations.

## IP Addressing & Routing

- **IP (Internet Protocol):** Core network-layer protocol.
- **Subnetting / Subnet mask:** Network segmentation and planning.
- **NAT / IP masquerading:** Private ↔ public translation.
- **Non-routable address space:** RFC1918 private ranges.
- **Next hop:** Routing table forwarding target.
- **Router:** Interconnects networks.
- **BGP:** Inter-domain routing on the Internet.
- **ASN:** Identifier for routing domains.

## Transport & Connectivity

- **TCP:** Reliable, connection-oriented transport.
- **UDP:** Lightweight, connectionless transport.
- **Ports (source/destination):** Service endpoints (e.g., 22, 53, 80, 443).
- **TCP flags (SYN, ACK, FIN, RST, PSH, URG):** Connection control and troubleshooting.
- **Socket:** Endpoint of a TCP/UDP connection.
- **ICMP:** Errors/diagnostics (ping, traceroute).
- **TTL (packet):** Hop limit to prevent loops.

## LAN & Switching

- **Ethernet / Ethernet frame:** Dominant LAN technology.
- **MAC address / OUI:** Layer-2 hardware identifiers.
- **ARP / ARP table:** IP ↔ MAC resolution.
- **Network switch:** Forwards frames by MAC.
- **VLAN / VLAN header:** Logical segmentation on switches.
- **Collision domain:** Scope of shared media contention.
- **Broadcast / Multicast / Unicast:** Traffic delivery modes.

## Security & Access

- **Firewall:** Policy-based traffic filtering.
- **VPN (site-to-site / point-to-point):** Encrypted tunnels for private access.
- **Two-factor authentication (2FA):** Stronger identity verification.
- **WPA:** Common Wi-Fi security standard.
- **Proxy / Reverse proxy:** Access control, caching, load distribution.

## Wireless & Physical

- **Wireless access point / WLAN:** Bridges wireless to wired networks.
- **Channels / Frequency bands:** RF planning for Wi-Fi.
- **Twisted pair / Fiber:** Common cabling media.
- **Patch panel:** Cable termination/organization.
- **Optical Network Terminator (ONT):** Fiber-to-Ethernet conversion.

## Cloud & Modern Infra

- **Cloud computing (IaaS / PaaS / SaaS):** Service-based compute models.
- **Virtualization / Hypervisor:** Multiple VMs on shared hardware.
- **Public / Private / Hybrid cloud:** Deployment models.

---
