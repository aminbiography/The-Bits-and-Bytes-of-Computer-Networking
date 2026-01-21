# Network Services 

---

This topic is based on key network services like **DNS, DHCP, NAT, VPNs, and proxies**, and how they improve **usability** and **security**.

---

## Table of Contents
- [Why DNS is important](#why-dns-is-important)
- [The Four Pillars of Modern Network Configuration](#the-four-pillars-of-modern-network-configuration)
- [DNS and Name Resolution](#dns-and-name-resolution)
  - [DNS Server Types (Core Roles)](#dns-server-types-core-roles)
  - [Caching and TTL (Time to Live)](#caching-and-ttl-time-to-live)
  - [DNS Hierarchy (Full Lookup Path)](#dns-hierarchy-full-lookup-path)
  - [Anycast (Why Root/TLD Servers Stay Fast)](#anycast-why-roottld-servers-stay-fast)
  - [DNS Transport Layer: UDP vs TCP](#dns-transport-layer-udp-vs-tcp)
  - [DNS Resource Record Types](#dns-resource-record-types)
  - [Domain Name Parts (Example: wwwgooglecom)](#domain-name-parts-example-wwwgooglecom)
  - [DNS Zones and Administrative Delegation](#dns-zones-and-administrative-delegation)
  - [Reverse Lookups (IP → Name)](#reverse-lookups-ip--name)
- [Overview of DHCP](#overview-of-dhcp)
  - [DHCP in Action](#dhcp-in-action)
- [Basics of NAT](#basics-of-nat)
  - [Technical Note: Network Address Translation (NAT)](#technical-note-network-address-translation-nat)
  - [NAT and the Transport Layer](#nat-and-the-transport-layer)
- [Supplemental Reading for IPv4 Address Exhaustion](#supplemental-reading-for-ipv4-address-exhaustion)
- [Virtual Private Networks](#virtual-private-networks)
- [Proxy Services](#proxy-services)
- [Most Common Glossary Terms](#most-common-glossary-terms)
- [Quick Troubleshooting Cheat Sheet](#quick-troubleshooting-cheat-sheet)

---

## Why DNS is important
- Computers communicate using numbers (binary), but humans remember words better.
- DNS converts domain names (like www.weather.com) into IP addresses (like 184.29.131.121).
- This conversion process is called name resolution.
- DNS allows organizations to change server IPs behind the scenes without users needing to memorize new IP addresses.
- DNS can also return different IPs based on user location, helping global companies deliver faster access using nearby servers.

---

## The Four Pillars of Modern Network Configuration
For a host to work predictably on a network, these four items are typically configured:
- **IP Address**: Logical address that identifies the device on a network.
- **Subnet Mask**: Separates the network portion and host portion of the IP address.
- **Default Gateway**: The router used to reach destinations outside the local network.
- **DNS Server**: Resolves human-friendly domain names into IP addresses.

---

## DNS and Name Resolution
DNS (Domain Name System) converts domain names (example: www.weather.com) into IP addresses (example: 184.29.131.121).  
This conversion process is called name resolution.

DNS is critical because:
- Humans remember names better than numbers.
- Organizations can change IP addresses behind the scenes without users changing behavior.
- DNS can provide different IPs depending on geographic region for better performance.

---

### DNS Server Types (Core Roles)
There are five primary DNS server roles:
- **Caching name server**: Stores previous lookup results temporarily.
- **Recursive name server (resolver)**: Performs the full lookup process on behalf of the client.
- **Root name server**: Directs queries to the correct TLD name server.
- **TLD name server**: Handles top-level domains like .com, .org, .edu.
- **Authoritative name server**: Provides the final answer for a domain controlled by an organization.

A single DNS server can perform more than one of these roles.

---

### DNS Lookup Process (Recursive Resolution)

![DNS Lookup Process](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-01a-DNS-Lookup-Process-(Recursive-Resolver-to-Root%2C-TLD-and-Authoritative-Name-Servers).png)

![DNS Lookup Process (Packet Count)](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-01b-DNS-Lookup-Process-(Recursive-Resolver-to-Root%2C-TLD-and-Authoritative-Name-Servers).png)

![DNS Lookup Process (Step-by-step)](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-01c-DNS-Lookup-Process-(Recursive-Resolver-to-Root%2C-TLD-and-Authoritative-Name-Servers).png)

---

### Caching and TTL (Time to Live)
- DNS results are stored in a cache to avoid repeating full DNS resolution.
- Every DNS record has a TTL (Time to Live) value (in seconds).
- When TTL expires, the server must discard the cached entry and perform a fresh look up.
- Longer TTLs reduce lookup traffic but make DNS changes take longer to spread globally.

---

### DNS Hierarchy (Full Lookup Path)
When a full recursive lookup is required, the general sequence is:
1. Recursive resolver → Root server
2. Root server → TLD server
3. TLD server → Authoritative server
4. Authoritative server → Final IP answer returned

This strict hierarchy supports stability and reduces the risk of malicious redirection.

---

### Anycast (Why Root/TLD Servers Stay Fast)
Root and TLD services often use anycast, meaning:
- Multiple physical servers share the same IP address.
- Traffic is routed to the “best” destination based on factors like location, congestion, or link health.
- This improves performance, resilience, and global availability.

---

### DNS Transport Layer: UDP vs TCP
DNS usually uses UDP on port 53 because:
- UDP is connectionless (no handshake or teardown).
- DNS queries and responses often fit into one UDP datagram.
- DNS is frequent, so minimizing overhead matters.

Packet comparison (full recursive example)
- UDP (~8 packets): simple request/response at each step. If a response is missing, the resolver asks again.
- TCP (~44 packets minimum): includes handshakes, ACKs, and connection teardown across multiple lookup stages.

When DNS uses TCP
DNS can switch to TCP when:
- The response is too large to fit into a single UDP datagram.
- The client then retries the lookup using TCP.

---

### Other Essential Network Services (High-Level)
- DHCP: Automatically assigns the four configuration pillars (IP, subnet mask, gateway, DNS).
- NAT: Translates private IPs to public IPs, preserving address space and adding basic isolation.
- VPNs and Proxies: Help users connect securely and access resources through controlled paths.

---

### DNS Resource Record Types
- **A record**: Maps a domain name to an IPv4 address.  
  Example: www.microsoft.com → 10.1.1.1
- **DNS Round Robin (multiple A records)**: A single domain can have multiple A records to balance traffic across several IPs.  
  Example IP list: 10.1.1.1, 10.1.1.2, 10.1.1.3, 10.1.1.4  
  Each lookup may return the same IPs but in a rotating order, so different clients try different servers first.
- **AAAA (Quad A) record**: Same idea as A record, but returns an IPv6 address (not IPv4).
- **CNAME record (Canonical Name)**: Redirects one domain to another domain.  
  Example: microsoft.com → www.microsoft.com  
  Benefit: You only update the main A/AAAA record in one place (single source of truth).
- **MX record (Mail Exchange)**: Tells where email for a domain should be delivered.  
  Web traffic and mail traffic can go to different servers/IPs.
- **SRV record (Service Record)**: Like MX, but for many service types (not only mail).  
  Example service: caldav (calendar/scheduling).
- **TXT record**: Free-form text data.  
  Originally for human notes, now commonly used to store service configuration data (example: email service provider settings).

Summary Table

| Record Type | Full Name | Primary Purpose |
|---|---|---|
| A | Address | Links a domain to an IPv4 address. |
| AAAA | Quad A | Links a domain to an IPv6 address. |
| CNAME | Canonical Name | Creates an alias (redirects one domain to another). |
| MX | Mail Exchange | Directs email traffic to the correct server. |
| SRV | Service Record | Locates specific services (like calendars or chat). |
| TXT | Text Record | Stores arbitrary text for configuration or verification. |

---

### Domain Name Parts (Example: www.google.com)
A domain name has three primary parts:
1. **TLD (Top-Level Domain)** = last part  
   Example: .com  
   - Common TLDs: .com, .net, .edu  
   - Country TLDs: .de (Germany), .cn (China)  
   - Vanity TLDs: .museum, .pizza  
   - Managed by ICANN (with IANA) for global DNS + IP coordination.
2. **Domain** = second part  
   Example: google  
   - This is where control moves from the TLD name server to the authoritative name server.  
   - Domains must end with a valid TLD and can be registered by individuals/companies.
3. **Subdomain / Hostname** = first part  
   Example: www  
   - Can be freely created by whoever controls the domain.

When all parts are combined, it is called a Fully Qualified Domain Name (FQDN):  
Example: www.google.com

Technical Restrictions & Limits

| Feature | Limit / Restriction |
|---|---|
| Hierarchy Depth | Up to 127 levels of subdomains (e.g., a.b.c...domain.com). |
| Section Length | Each individual part (label) can be maximum 63 characters. |
| Total FQDN Length | The entire name cannot exceed 255 characters. |
| Characters allowed | Generally restricted to letters, numbers, and hyphens. |

---

### DNS Zones and Administrative Delegation
DNS is not just a giant list; it is a delegated hierarchy. Zones are the administrative boundaries that define who is responsible for which part of that hierarchy.

Hierarchical Responsibility
- Root Zone: Managed by Root Servers.
- TLD Zones: Managed by TLD Servers (e.g., the .com zone).
- Lower-level Zones: Managed by organizations (e.g., the google.com zone).

Non-Overlapping Authority (Delegation)  
A critical rule of DNS is that authority is “handed off.” The .com server knows where the google.com server is, but it does not know the internal IP addresses of Google’s specific web servers. This prevents any single server from needing to store the entire Internet’s DNS data.

Scaling Through Sub-Zones  
Large companies split domains into sub-zones (like la.largecompany.com) so local IT teams can manage their own records without affecting the main corporate domain.

The Zone File: The “Source of Truth”  
A Zone File is the configuration file stored on an Authoritative Name Server.
- SOA (Start of Authority): The “ID card” of the zone. It must be present and defines the primary server and contact information for that zone.
- NS (Name Server) Records: Essential for redundancy. By listing multiple physical servers, DNS ensures that if one server goes down, the zone remains reachable.
- Record Variety: Zone files contain records such as A (IPv4), AAAA (IPv6), CNAME (aliasing), and TTL (Time to Live) settings that control caching duration.

---

### Reverse Lookups (IP → Name)
Standard DNS works like a phone book (Name → Number). A Reverse Lookup is the opposite (Number → Name).
- PTR (Pointer) Records: The primary records used in reverse lookup zones.

Why it matters: PTR records are frequently used in security and email verification. For example, a mail server may check the PTR record of an incoming connection to confirm the IP address matches the domain it claims to be from.

---

## Overview of DHCP
DHCP Purpose: To eliminate the tedious and error-prone task of manually configuring IP addresses, subnet masks, gateways, and DNS servers for every device.

The DORA Process: The four-step handshake (Discover, Offer, Request, Acknowledgment) that allows a client to obtain an IP from the server.

Allocation Types:
- Dynamic: The IP changes (best for mobile clients).
- Automatic: The server tries to remember the device (best for desktops).
- Fixed: Strict MAC-to-IP mapping (best for printers/servers).

NTP (Network Time Protocol): One of the additional services DHCP can configure to keep all network devices synchronized.

---

### DHCP Overview Images

![DHCP Overview](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-02a-DHCP.png)

![DHCP Across Networks](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-02b-DHCP.png)

![DHCP Dynamic Allocation](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-02c-DHCP.png)

---

## DHCP in Action
DHCP Discovery (DORA - Discovery, Offer, Request, Acknowledgment)  
DHCP is an application layer protocol that automatically provides a host with network settings before it has an IP address by using broadcast messages on the local LAN.

Ports (UDP):
- DHCP Server: UDP 67
- DHCP Client: UDP 68

DHCP Discovery Steps (DORA):
1. Discover: Client broadcasts to find a DHCP server  
   - Src IP: 0.0.0.0 → Dst IP: 255.255.255.255
2. Offer: Server broadcasts an offered IP + config (includes client MAC)
3. Request: Client broadcasts acceptance of the offered IP
4. ACK: Server broadcasts confirmation and final lease details

DHCP Lease: The IP is assigned for a limited time. After expiration, the client must renew/re-run discovery. The client may also release the IP when disconnecting.

![DHCP Discover](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-03-DHCP-Discover.png)

![DHCP Offer](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-04a-DHCP-Offer-Message.png)

![DHCP Request](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-04b-DHCP-Request-Message.png)

![DHCP ACK](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-04c-DHCP-ACK.png)

---

## Basics of NAT

NAT Packet Flow: Step-by-Step  
Using the example of Computer 1 (Network A) communicating with Computer 2 (Network B) through a NAT-enabled router:

| Packet Stage | Source IP | Destination IP | Note |
|---|---|---|---|
| 1. Outbound (Internal) | 10.1.1.100 | 192.168.1.100 | Packet leaves Computer 1. |
| 2. After NAT Rewrite | 192.168.1.1 | 192.168.1.100 | Router replaces source with its own interface IP. |
| 3. Inbound Response | 192.168.1.100 | 192.168.1.1 | Computer 2 responds to the Router. |
| 4. After NAT Restore | 192.168.1.100 | 10.1.1.100 | Router restores the original destination IP. |

![NAT Overview](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-05a-NAT.png)

![NAT Source Rewrite](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-05b-NAT.png)

---

### Network Address Translation (NAT)
NAT is a technique used by gateways (routers/firewalls) to map one IP address space into another by modifying network address information in the IP header of packets while they are in transit.

Core Functions
1) IP Masquerading  
The process of hiding internal IP addresses from the outside world. This acts as a security safeguard because external entities only see the gateway's IP, making it impossible to establish an unsolicited connection directly to an internal host.

2) One-to-Many NAT  
A common implementation where hundreds of private internal IPs are translated to a single public IP. This is the primary method used today to preserve the limited IPv4 address space.

NAT vs. Traditional Routing

Standard Router
- Decrements TTL
- Recalculates checksum
- Forwards the packet without changing the IP headers

NAT Router
- Performs all the tasks of a standard router
- Rewrites the Source IP (outbound) or Destination IP (inbound)
- Maintains a translation table to ensure data returns to the correct internal machine

Professional Significance  
In IT support, NAT is critical for understanding why an internal server might not be reachable from the internet. Without specific Port Forwarding or Destination NAT rules, the masquerading function of NAT will block all incoming attempts to reach internal nodes.

---

### NAT and the Transport Layer
While NAT works at the Network Layer (IP addresses), it relies on the Transport Layer (ports) to manage traffic for many internal devices using one external IP. These are the two most critical techniques for troubleshooting NAT behavior:

1) Port Preservation (Outbound Traffic)  
When multiple devices on a private network share a single public IP, the router uses source ports to track which internal host should receive return traffic.

How it works:
- A client (10.1.1.100) sends outbound traffic using an ephemeral source port (example: 51,300).
- The NAT router replaces the source IP with its own public IP, but may preserve the source port.
- The router stores this mapping in a NAT translation table.

Conflict (Port Translation):
- Two internal computers can choose the same ephemeral port at the same time.
- To avoid collisions, the router performs port translation by assigning an unused external port to one of them.
- This is commonly called PAT (Port Address Translation) or NAT overload.

Return traffic:
- The external server replies to the router’s public IP and the mapped port (example: 51,300).
- The router checks the NAT table and forwards the response to the correct internal host (10.1.1.100).

![Port Preservation](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-06b-Port-Preservation.png)

2) Port Forwarding (Inbound Traffic)  
Port forwarding allows external users to access internal services (web, mail, SSH) without knowing private IP addresses.

How it works:
- You configure the router:  
  “Traffic arriving on the public IP at port 80 → forward to internal 10.1.1.5”

Example (multiple services, one public IP):

| External IP (Router) | External Port | Internal Service | Internal IP |
|---|---:|---|---|
| router_public_ip | 80 | Web Server | 10.1.1.5 |
| router_public_ip | 25 | Mail Server | 10.1.1.6 |
| router_public_ip | 22 | SSH / Management | 10.1.1.7 |

This allows one public IP / DNS name to support multiple internal services using different ports.

![Port Forwarding](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-06a-Port-Forwarding.png)

![Port Forwarding (Multiple Services)](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-06c-Port-Forwarding.png)

Overview
- IP Masquerading: hides internal private IP addresses from the outside world.
- Source Port: identifies outbound sessions (helps NAT return traffic to the right client).
- Destination Port: identifies inbound services (used for port forwarding).
- PAT / NAT Overload: enables many internal devices to share one external IP using ports.
- One Source of Truth: external users only need one public IP/DNS name to reach multiple services.

---

## Supplemental Reading for IPv4 Address Exhaustion

IPv4 Address Exhaustion & the Rise of IPv6  
The rapid expansion of the Internet has created a serious shortage of IPv4 addresses, which are the numerical identifiers used to locate devices online. This note summarizes how IP resources are managed and why IPv6 is the long-term solution.

1) Global IP Management Hierarchy  
IP addresses are distributed through a strict global-to-regional hierarchy:
- IANA (Internet Assigned Numbers Authority):  
  The global authority that allocates massive blocks of IP addresses to regional organizations.
- RIRs (Regional Internet Registries):  
  Organizations responsible for managing Internet number resources within specific geographic regions.

Your device does not receive an IP directly from IANA — it gets one indirectly through your ISP, which receives allocations through this registry system.

RIR Name | Geographical Region
---|---
AFRINIC | Africa
ARIN | USA, Canada, parts of the Caribbean
APNIC | Most of Asia, Australia, New Zealand, Pacific Island nations
LACNIC | Central/South America and parts of the Caribbean
RIPE | Europe, Russia, Middle East, portions of Central Asia

![RIR World Map](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-07-Regional-Internet-Registries-(RIRs)-World-Map.png)

2) The Exhaustion Timeline  
IPv4 uses a 32-bit addressing scheme, allowing approximately 4.2 billion possible addresses.  
Because of the explosive growth of connected devices, this pool has effectively run out:
- Feb 3, 2011: IANA assigned the last unallocated IPv4 /8 blocks.
- Regional depletion followed:
  - APNIC reached its final /8 (April 2011)
  - RIPE reached its final /8 (September 2012)
  - LACNIC reached its final /10 (June 2014)
  - ARIN exhausted free IPv4 addresses (September 2015)
  - AFRINIC entered IPv4 Exhaustion Phase 2 (January 2020)

Current state: Many “new” IPv4 assignments are now recycled/reused addresses.

3) The Solution: IPv6  
IPv6 was designed to overcome IPv4 limitations using 128-bit addresses.
- IPv4 capacity: 2^32 ≈ 4.2 billion
- IPv6 capacity: 2^128 ≈ 3.4 × 10^38 (practically inexhaustible)

Key idea: IPv6 provides enough address space to support long-term Internet growth without constant address scarcity.

Reality today: Even though IPv6 is the future, about 99% of devices still rely on IPv4 in practice, so both must be understood during the transition period.

Why This Matters for IT Support and Troubleshooting
- Recycled IPv4 addresses: A “new” IPv4 may have history (including reputation issues) because it was previously assigned elsewhere.
- Dual-stack era: Many environments run IPv4 and IPv6 simultaneously, which affects troubleshooting steps and routing behavior.
- Long-term impact: As IPv6 adoption increases, dependence on IPv4 workarounds (like NAT) will reduce because more devices can have globally unique addresses again.

Key Takeaways
- IPv4 has nearly exhausted its available address space (~4.2 billion).
- IANA distributes address blocks to five RIRs, which manage IPs regionally.
- IPv6 provides vastly more addresses and is the long-term solution, but IPv4 remains dominant today.

---

## Virtual Private Networks
Tunneling (Core idea): A VPN takes a packet meant for a private network and hides it inside another packet, allowing it to “tunnel” securely through the public internet using encryption.

Virtual Interface (Virtual network card): When you connect to a VPN, your computer creates a virtual interface (a “fake” network adapter) and gets an IP address that belongs to the office network, not your home network. This makes your device behave like it is inside the company LAN.

2FA (Something you know + Something you have): VPNs usually require strong authentication. 2FA combines your password with a rotating short-lived code from an app or a hardware token to prevent unauthorized access.

Site-to-Site vs. Remote Access:
- Remote Access VPN: Designed for individual users (work-from-home, travel) to securely reach internal company resources.
- Site-to-Site VPN: Connects two full office networks together so they can share services (servers, printers, internal tools) as if they were in the same building.

![VPN Connection](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-08a-VPN-Connection.png)

![VPN Tunnel Packet](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-08b-VPN-Connection.png)

![VPN Internal Access](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-08c-VPN-Connection.png)

![Site-to-Site VPN](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-08d-VPN-Connection.png)

---

## Proxy Services
Proxy (General):  
A proxy is an intermediary server that sits between a client and another server to provide benefits like security, anonymity, filtering, performance, or control.

1) Forward Proxy (Client-side Proxy)
- Acts on behalf of the client
- Common uses:
  - Content filtering (block sites like social media during work hours)
  - Anonymity / privacy (hides the client from the destination server)
  - Traffic inspection and control

2) Reverse Proxy (Server-side Proxy)
- Acts on behalf of the server
- Makes multiple backend servers appear as one server to users
- Common uses:
  - Load balancing (distributes traffic so one server is not overwhelmed)
  - Hides internal server architecture (adds security and abstraction)
  - Improves reliability and scaling for high-traffic sites

3) SSL/TLS Offloading
- A professional efficiency technique where the reverse proxy handles encryption/decryption
- This reduces CPU load on backend servers so they can focus on serving content

4) Caching (Classic Web Proxy Use)
- Older proxies improved performance by caching web pages
- Less useful today because:
  - Internet is faster
  - Websites are highly dynamic and personalized (example: social media)
- Still important historically and conceptually for understanding proxy benefits

![Proxy Server](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-09-Proxy-Server.png)

![Reverse Proxy](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-10a-Reverse-Proxy.png)

![Reverse Proxy Decryption](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-10b-Reverse-Proxy-Decryption.png)

---

## Most Common Glossary Terms

The Connectivity “Pillars” (DHCP & DNS)  
If a user cannot get online, the problem is usually one of these two services.
- DHCP (Dynamic Host Configuration Protocol): The automation service. It provides the IP Address, Subnet Mask, Gateway, and DNS Server automatically.
- DORA Process: The 4-step handshake used to get an IP: Discovery → Offer → Request → Acknowledge.
- DNS (Domain Name System): The “phonebook” of the internet. It translates human-readable names (like google.com) into machine-readable IPs.
  - A Record: Maps name → IPv4
  - AAAA Record: Maps name → IPv6
  - CNAME: Alias record (one name points to another)
  - MX Record: Directs email traffic

Network Boundaries & Security (NAT & VPN)  
These technologies control how data enters and leaves a private company network.
- NAT (Network Address Translation): Allows many private IPs inside an office to share one public IP.
  - IP Masquerading: Hides internal IPs from the outside world for security
  - Port Forwarding: Rules that allow external traffic to reach a specific internal server (example: a web server)
- VPN (Virtual Private Network): An encrypted tunnel. It makes a remote computer (at home) act like it is physically plugged into the office network.
  - Two-Factor Authentication (2FA): Password + secondary token (example: a code on your phone)

Intermediaries & Traffic Flow (Proxies)
- Forward Proxy: Acts for the client (example: a company blocking Twitter to keep employees productive).
- Reverse Proxy: Acts for the server. It handles:
  - Load balancing (spreading traffic across many servers)
  - Decryption so web servers do not get overwhelmed

Technical “Rules of the Road” (TCP/IP Fundamentals)
- IP Datagram & TCP Segment: The “envelopes” data travels in.
- TTL (Time-To-Live): A safety counter. Every time a packet hits a router, TTL decreases. If it reaches 0, the packet is deleted so it does not loop forever.
- Ports: 16-bit service numbers (0–65,535), like “apartment numbers” for services (example: Port 80 for web, Port 25 for mail).
- Handshake (SYN/ACK): How TCP confirms both computers are ready before real data is sent.

---

## Quick Troubleshooting Cheat Sheet

| If the problem is… | Look at these terms |
|---|---|
| “I have no internet connection” | DHCP, IP Address, Gateway, Subnet Mask |
| “I can ping the IP but not the website” | DNS, A Record, Name Resolution |
| “I cannot access company files from home” | VPN, Tunneling, 2FA |
| “The website is slow because of too many users” | Reverse Proxy, Load Balancing, Round Robin |
