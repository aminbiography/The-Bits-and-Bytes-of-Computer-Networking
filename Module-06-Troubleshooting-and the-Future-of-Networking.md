# Core Networking Troubleshooting Concepts

## Troubleshooting & Future of Networking

### Networking Complexity
- Modern networks involve many layers, protocols, and devices → failures are normal.

### Error Detection
- **Definition:** Mechanism to identify that a problem occurred.  
- **Example:** CRC (Cyclic Redundancy Check) verifies data integrity.

### Error Recovery
- **Definition:** Mechanism to correct or compensate for detected errors.  
- **Example:** Transport layer resends data if corruption/loss is detected.

### CRC Behavior
- If CRC ≠ payload data → data is discarded.  
- Then the transport layer decides on retransmission.

### Common Causes of Network Issues
- Misconfigurations  
- Hardware failures  
- System incompatibilities  
- Data corruption

### Troubleshooting Focus
- Learn standard techniques and tools.  
- Goal: Detect and fix common connectivity problems.

### Key Operating Systems for Troubleshooting
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
- **Type (8 bits):** Message category  
- **Code (8 bits):** Specific reason  
- **Checksum (16 bits):** Error check  
- **Rest of Header (32 bits):** Optional data  
- **Payload:** Original IP header + first 8 bytes of data

---

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
- **Windows:** 4 pings by default  
- **Linux/macOS:** Continuous until `Ctrl + C`

### Ping Customization
Flags allow changes to:
- Packet count  
- Packet size  
- Send interval  

Useful for latency tests and stability checks.

---

# Command Line Troubleshooting Tools

## Software & Hardware Troubleshooting

### File Operations
- `copy` / `cp` → basic file copy  
- `xcopy` → copy with subdirectories and large-file support  
- `robocopy` → secure, permission-preserving copy

### Disk & System Health
- `chkdsk` / `fsck` → scan and repair file system errors  
- `sfc` → repair corrupted Windows system files  
- `format` → erase and reset a drive  
- `diskpart` / `fdisk` → manage disk partitions

### System Info
- `shutdown` → shutdown/restart systems (`/fw` to firmware)  
- `winver` → show Windows version

---

## Networking Troubleshooting

### Configuration & Connectivity
- `ipconfig` / `ip` → view IP configuration (`/all` for details)  
- `ping` → test reachability and latency  
- `tracert` / `traceroute` → view packet route  
- `pathping` → detect packet loss per hop  
- `hostname` → show device name

### Diagnostics
- `netstat` → show active connections and ports  
- `nslookup` → query DNS records

---

## User & Group Management

### Users
- `net user` → add/modify/delete accounts  
- `net use` → manage shared resource connections

### Group Policy
- `gpupdate` → refresh policies  
- `gpresult` → view applied policies (RSOP)

---

# Traceroute

## Purpose
Shows the path to a destination and helps locate which router causes delay or failure.

- **Ping =** reachability  
- **Traceroute =** path + latency per hop

## Key Mechanism: TTL Manipulation
- Packets sent with TTL = 1, 2, 3…  
- Each router decrements TTL by 1  
- TTL = 0 → router drops packet and returns ICMP Time Exceeded

## Hop Discovery Process
- TTL=1 reveals hop 1  
- TTL=2 reveals hop 2  
- Continues until destination replies

## Per-Hop Measurements
- 3 probes per hop  
- Displays hop number, RTT, IP, hostname  
- Multiple RTT values detect jitter

## Platform Behavior
- Linux/macOS `traceroute` → UDP  
- Windows `tracert` → ICMP Echo

## Advanced Tools
- **MTR:** Real-time updates  
- **Pathping:** ~50s test then aggregated stats

### Why Use MTR/Pathping
- Better for intermittent issues  
- Reveal packet loss patterns

### Platform Differences

| OS / Tool | Protocol | Continuous |
|----------|----------|------------|
| Linux/macOS traceroute | UDP | No |
| Windows tracert | ICMP | No |
| MTR | ICMP/UDP | Yes |
| Pathping | ICMP | Yes |

---

# Testing Port Connectivity

## Goal
Verify if a specific service/port is reachable.

## Netcat (nc) — Linux/macOS
- Swiss Army Knife for TCP/UDP  
- `nc host port`  
- `-z` scan mode  
- `-v` verbose  
- `nc -zv host port` confirms open/closed ports

## Test-NetConnection — Windows
- Detailed diagnostics  
- `-Port` tests specific port  
- Output: `TcpTestSucceeded`  
- Shows routing/link-layer info

### Comparison

| OS | Command | Advantage |
|----|--------|----------|
| Linux/macOS | nc | Lightweight, manual data send |
| Windows | Test-NetConnection | Detailed routing info |

---

# Name Resolution Tools (nslookup)

- Converts domain names to IPs  
- `nslookup domain.com` → A record + DNS server  
- Interactive mode supported  
- `server <address>` change DNS  
- `set type=` query record types  
- `set debug` for full DNS response

---

# Public DNS Servers

## Service Models
- ISP DNS  
- Internal DNS  
- DNS as a Service  
- Public DNS (for testing)

## Public Providers
- Google: 8.8.8.8 / 8.8.4.4  
- Level 3: 4.2.2.1–4.2.2.6

## Troubleshooting Tip
If ping to 8.8.8.8 works but websites fail → DNS issue likely.

## Risks
- DNS hijacking  
- Use reputable providers

## Best Practice
Use ISP/internal DNS daily; public DNS for testing.

## Anycast
Routes queries to nearest server.

---

# DNS Registration and Expiration

- ICANN manages global hierarchy  
- Registrars sell/manage domains  
- Domains must be unique

### Workflow
1. Check availability  
2. Choose term  
3. Pay and register

### Authoritative DNS
- Registrar-managed  
- Self-managed

### Transfers
- Verified with authorization string (TXT record)

### Expiration
- Domains are leased  
- Non-renewal → downtime risk

---

# Hosts Files

- Local name resolution mapping  
- Checked before DNS  
- Device-local only

### Loopback
- IPv4: 127.0.0.1  
- IPv6: ::1

### Uses
- Force domain mapping  
- DNS workaround  
- Legacy apps

### Risks
- Malware modification

---

# The Cloud

## Definition
Delivery model for compute, storage, services.

## Virtualization
- Host  
- Guest VM  
- Hypervisor

## Concepts
- Resource pooling  
- Decoupling

## Benefits
- Pay-as-you-use  
- Rapid provisioning  
- Built-in services

### Deployment Models

| Model | Description |
|------|------------|
| Public | Shared provider resources |
| Private | Single-organization use |
| Hybrid | Mix of both |

---

# Everything as a Service (XaaS)

## IaaS
User manages OS/apps.

## PaaS
User manages code/data.

## SaaS
Fully managed apps.

### Progression
IaaS → PaaS → SaaS  
(Control ↓ Convenience ↑)

---

# Cloud Storage

- Secure remote storage  
- Geographic redundancy  
- Scalable  
- Pay-as-you-go

### Use Cases
- Enterprise backup  
- Personal backup

---

# IPv6 Addressing & Subnetting

## Why IPv6
- IPv4 exhaustion  
- 128-bit addressing

## Format
8 groups of hex

### Shortening
- Remove leading zeros  
- `::` once

## Special Ranges
- 2001:db8::/32 documentation  
- FF00::/8 multicast  
- FE80::/10 link-local

## Structure
- 64-bit network  
- 64-bit host  
- /64 standard subnet

---

# IPv6 Headers

- Fixed 40 bytes  
- Efficient design

### Fields
- Version  
- Traffic Class  
- Flow Label  
- Payload Length  
- Next Header  
- Hop Limit  
- Source/Destination

### Comparison

| Feature | IPv4 | IPv6 |
|--------|------|------|
| Address | 32-bit | 128-bit |
| Header | 20–60B | 40B |
| Lifespan | TTL | Hop Limit |
| Options | Inline | Extension |

---

# IPv6 & IPv4 Transition

## IPv4-Mapped IPv6
- ::ffff:IPv4

## Tunneling
- Encapsulation in IPv4

## Tunnel Brokers
- Third-party endpoints

---

# Tunneling Protocols

| Protocol | Mechanism | Advantage | Disadvantage |
|---------|----------|----------|-------------|
| 6in4 | Direct | Fast | NAT issues |
| TSP | Negotiated | Flexible | Complex |
| AYIYA | Any-in-any | NAT friendly | Overhead |

---

# Top Professional Networking Terms

## Core Services
- DNS  
- DHCP  
- NTP  
- ISP

## DNS Ops
- A/AAAA  
- CNAME  
- MX  
- NS  
- TXT  
- FQDN  
- TTL  
- Zone files

## IP & Routing
- IP  
- Subnetting  
- NAT  
- RFC1918  
- Next hop  
- Router  
- BGP  
- ASN

## Transport
- TCP / UDP  
- Ports  
- TCP flags  
- Socket  
- ICMP  
- TTL

## LAN & Switching
- Ethernet  
- MAC/OUI  
- ARP  
- Switch  
- VLAN  
- Collision domain  
- Broadcast/Multicast/Unicast

## Security
- Firewall  
- VPN  
- 2FA  
- WPA  
- Proxy / Reverse proxy

## Wireless & Physical
- AP / WLAN  
- Channels  
- Twisted pair / Fiber  
- Patch panel  
- ONT

## Cloud
- IaaS / PaaS / SaaS  
- Virtualization / Hypervisor  
- Public / Private / Hybrid cloud

---

