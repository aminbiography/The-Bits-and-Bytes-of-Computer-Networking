# ISP Connectivity and Edge Access

---

## Connecting to the Internet

---

## Internet Device Diversity
- **Internet Device Diversity:** The Internet connects a huge variety of devices, not just computers.
- **Examples of Connected Devices:** Connected devices include desktops/laptops, servers/data centers, routers/switches, tablets/phones, ATMs, industrial equipment, medical devices, and cars.
- **Beyond Cat 5/Cat 6 and Ethernet:** Internet connectivity is not limited to only Cat 5/Cat 6 cables and Ethernet.
- **Multiple Connectivity Technologies:** Real-world Internet connections use many different technologies.
- **Module Outcomes:** Module outcomes: explain Internet connectivity technologies, define WAN components, and outline wireless + cellular networking basics.
- **Core IT Support Skill:** Key IT support skill: ensuring users and devices can get online.

---

## Dial-up and Modems
- **Early Networking:** Early computer networks existed before Ethernet/TCP/IP and mainly connected nearby devices.
- **Long-Distance Networking (Late 1970s):** Duke University grad students used the public telephone network to connect computers over long distances.
- **PSTN / POTS:** Public Switched Telephone Network (PSTN) = Plain Old Telephone Service (POTS).
- **Usenet:** Their system became Usenet, a precursor to later dial-up networks (still partly used today).
- **Dial-Up Connection:** Uses POTS for data transfer; connection established by dialing a phone number.
- **Modems:** Data transfer over dial-up used modems (modulator/demodulator).
- **Modem Function:** Modems convert computer data into audible wavelengths for transmission over phone lines.
- **Concept Link (Line Coding):** Similar concept to line coding that carries bits over Ethernet.
- **Baud Rate:** How many bits can pass over a phone line per second.
- **Dial-Up Speed Progression:** ~110 bps (late 1950s) → ~300 bps (Usenet era) → 14.4 kbps (early 1990s).
- **Modern Status:** Dial-up is rare today due to broadband, but still exists in some rural areas.
- **Historical Importance:** Dial-up was the main long-distance computer communication method for decades.

---

## What is broadband?
- **Broadband:** Any connectivity technology that isn't dial-up Internet.
- Broadband is any high-speed, always-on Internet connectivity technology. Unlike dial-up, it does not require dialing and establishing a new connection each time you want to go online.

### Key Characteristics
- **Always-on connection:** The link stays active and available.
- **High speed:** Much faster than dial-up connections.
- **Supports modern Internet use:** Enables streaming, cloud services, video calls, and online learning.

### Historical Foundation: T-Carrier Technologies
Before broadband became common in homes, businesses used T-carrier systems.
- Originally developed by AT&T to carry multiple voice calls over one line.
- Later used for high-speed data transmission compared to dial-up.
- Requires dedicated lines, making it more expensive and mostly used by businesses.

### Why Broadband Speed Matters
Dial-up could not support modern file sizes and web content.
- **Example:** A 2 MB photo ≈ 16,777,216 bits  
- **At 14.4 kbps (dial-up):** ~20 minutes to download  
- **At modern broadband speeds:** downloads in seconds or less  

### Impact
Broadband made today’s Internet possible by supporting:
- Faster websites and media loading
- Music and video streaming
- Reliable access for many users at once
- Online platforms and services at scale

---

## T-Carrier Technologies

### T-Carrier Technologies: Evolution and Key Specifications
T-Carrier systems were originally developed by AT&T to support large-scale voice communication. They later became an important step in the evolution of high-speed data networking over copper infrastructure.

### T1 Lines (Core Standard)
**Original Purpose:**  
Designed to carry 24 simultaneous phone calls over a single twisted-pair copper connection.

**Technical Details:**
- 24 channels (timeslots)
- 64 Kbps per channel
- Total throughput: 1.544 Mbps

**Modern Usage:**  
Today, the term “T1” is often used to describe any copper link operating at 1.544 Mbps, even if it does not follow the original T1 specification exactly.

### T3 Lines (Higher Capacity)
**How it works:**  
A T3 line is created by multiplexing 28 T1 lines into one high-capacity link.

- Total throughput: 44.736 Mbps

**Historical role:**  
Commonly used by large businesses and ISPs that needed higher bandwidth before fiber became widely available.

### Deployment and Current Relevance
**Early use:**
- Connecting telecom company sites
- Interconnecting different telecom networks

**1990s expansion:**
- Adopted by businesses as a premium broadband option for office Internet access

**Today:**
- Small businesses: Mostly replaced by cable and fiber (cheaper and faster)
- ISP/backbone networks: Largely replaced by fiber-optic technologies for high-capacity long-distance transmission

---

## Digital Subscriber Lines

### DSL Technology: High-Frequency Data Over Legacy Copper
DSL (Digital Subscriber Line) modernized the public telephone network by using existing twisted-pair copper not just for analog voice, but for high-frequency digital transmission.

### Frequency Separation (Voice + Data Together)
Traditional voice calls operate in the 0–4 kHz range. DSL transmits data using higher frequency bands, allowing simultaneous voice and Internet on the same line without interference.

### Persistent Connectivity (Always-On Behavior)
Unlike dial-up, which creates a temporary switched connection, DSL is typically persistent.  
The link stays established between the customer modem and the DSLAM (Digital Subscriber Line Access Multiplexer) as long as the equipment remains powered.

### DSL Categories and Traffic Design
DSL types mainly differ in how the available spectrum is allocated for upstream vs. downstream bandwidth.

#### ADSL (Asymmetric Digital Subscriber Line)
- **Design:** More spectrum allocated to downstream than upstream
- **Use Case:** Best for home users in a client-server model
  - **Upload:** small requests (e.g., HTTP requests)
  - **Download:** large content (HTML, images, video)
- **Benefit:** Cost-efficient while matching typical user behavior

#### SDSL (Symmetric Digital Subscriber Line)
- **Design:** Equal spectrum allocation for upload and download
- **Use Case:** Suitable for businesses and advanced users needing strong upstream performance
  - Hosting services, VPNs, VoIP, remote access
- **Capacity:** Often capped around 1.544 Mbps, similar to a T1 line

#### HDSL (High-bit-rate Digital Subscriber Line)
- **Design:** Higher-speed evolution of symmetric DSL variants
- **Capability:** Provides speeds above 1.544 Mbps
- **Use Case:** Used where higher throughput is required over copper-based infrastructure

### Technical Constraints and Real-World Limitations
- **Distance sensitivity:** Higher frequencies attenuate quickly, so DSL speed depends heavily on the distance between the user and the DSLAM/central office.
- **Infrastructure value:** DSL extended the usefulness of legacy copper networks and delayed full fiber replacement by enabling broadband-grade data rates.

---

## Cable Broadband

### Cable Broadband Technology
Cable broadband uses the existing coaxial cable infrastructure originally deployed for cable television. Like DSL, it transmits data using frequency ranges that do not interfere with TV signals, allowing Internet and TV to coexist on the same line.

### Key Infrastructure & Hardware
Cable Internet works through a provider-managed architecture that connects the home to the ISP core network:
- **Cable Modem:** Customer-premises device that modulates/demodulates data over the coaxial cable.
- **CMTS (Cable Modem Termination System):** Provider-side system that aggregates many cable modem connections and links them into the ISP’s high-speed core network.

### Shared Bandwidth Model (Main Difference)
Cable broadband is primarily a shared-bandwidth technology:
- **Shared topology:** Many users share the same bandwidth pool before reaching the ISP core.
- **Neighborhood effect:** Bandwidth may be shared across a block, street, or subdivision depending on wiring design.
- **Performance impact:** Speeds may drop during peak hours due to congestion/contestion from many active users.

### Comparison with DSL / Point-to-Point Systems
- **DSL / Dial-up:** Typically connect directly to a Central Office (CO) → point-to-point behavior.
- **Cable:** Shared segment exists before ISP core → more likely to show peak-time slowdowns.

### Historical Context
- **TV evolution:** Wireless (towers/antennas) → wired (cable).
- **Networking evolution:** Wired origins → increasing shift toward wireless technologies.
- **1984 Cable Communications Policy Act (US):** Deregulated cable industry → major growth; by the 1990s, cable infrastructure became comparable in size to the public telephone system.

---

## Cable Broadband (Additional Notes)
- **Wired vs Wireless Evolution:** Telephone and computer networking began as wired communication, but modern trends are shifting more traffic to wireless.
- **TV to Cable Transition:** Television began as wireless tower broadcasts, and cable TV was introduced in the late 1940s to reach rural areas beyond tower range.
- **Cable TV History:** Cable TV began as a solution to deliver television to rural areas beyond tower range, then expanded rapidly after deregulation (1984), creating large-scale coaxial infrastructure.
- **Cable Broadband:** In the 1990s, cable providers realized coaxial cables could carry far more data than TV required, enabling high-speed Internet using non-interfering frequencies (cable broadband).
- **Shared Bandwidth Model:** Unlike DSL/dial-up point-to-point links to a central office (CO), cable Internet is typically shared bandwidth, so many users share capacity until reaching the ISP core network.
- **Cable Modem & CMTS:** Cable connections use a cable modem at the customer side, which connects to a CMTS that aggregates many users into the ISP network.

### Cable Broadband vs DSL Comparison Table

| Feature | Cable Broadband | DSL |
|---|---|---|
| Physical Media | Coaxial Cable | Twisted-Pair Copper |
| Connection Type | Shared Bandwidth | Point-to-Point |
| Termination Point | CMTS | DSLAM / Central Office (CO) |
| Common Issue | Congestion during peak hours | Speed drop over distance |

---

## Fiber Connections

### Fiber Optic Connectivity (FTTX)
Fiber Technology: Fiber transmits data using pulses of light, not electrical currents. It is the main backbone of the modern Internet due to its high speed, long range, and low signal loss.

### Distance and Signal Integrity
- **Copper (Electrical):** Signal degrades after a few thousand feet, often requiring repeaters.
- **Fiber (Light):** Signal can travel many miles before degradation becomes significant.

### Cost Factor
Fiber is more expensive to install than copper, so it was traditionally used mainly in ISP core networks and data centers. Today, fiber is being deployed closer to end users.

### FTTX: Fiber to the “X”
FTTX describes how close fiber reaches to the customer:
- **FTTN (Fiber to the Neighborhood):** Fiber reaches a local cabinet, then the last distance uses copper or coax.
- **FTTB (Fiber to the Building/Business/Basement):** Fiber reaches the building, then internal connections use twisted-pair copper.
- **FTTH (Fiber to the Home):** Fiber runs directly to each residence.
- **FTTP (Fiber to the Premises):** A general term that includes FTTB and FTTH.

### Hardware: ONT (Optical Network Terminator)
- **ONT Role:** The demarcation points for fiber service.
- **Function:** Converts optical (light) signals into electrical Ethernet signals that home/business networks can use.

### Quick Comparison

| Feature | Fiber Optic | Copper (DSL/Cable) |
|---|---|---|
| Medium | Light (Glass/Plastic) | Electricity (Copper) |
| Max Distance | Many miles | Thousands of feet |
| Endpoint Hardware | ONT | Modem (DSL/Cable) |
| Main Advantage | Highest speed, lowest degradation | Lower cost, widely available |

---

## Broadband Protocols

### Broadband Protocols: PPP and PPPoE
Broadband communication uses Data Link Layer (Layer 2) protocols to establish links, manage sessions, and support authentication for reliable data transfer.

### Point-to-Point Protocol (PPP)
PPP is a byte-oriented Layer 2 protocol used to transmit data between two directly connected endpoints. It is vendor-neutral, so different hardware vendors can communicate.

#### 1) PPP Configuration Features
- **Multilink:** Combines multiple PPP links to increase bandwidth and balance traffic.
- **Compression:** Reduces frame size to improve throughput.
- **Authentication:**
  - **PAP:** Password-based authentication (simple exchange).
  - **CHAP:** More secure 3-way handshake and periodically re-check’s identity.
- **Error Detection:**
  - **FCS:** Validates frame integrity to detect corruption/loss.
  - **Magic Numbers:** Detects looped links; matching numbers indicate a loop, so frames are discarded.

#### 2) PPP Sub-Protocols
- **LCP (Link Control Protocol):** Establishes, configures, tests, and terminates the PPP link (authentication, loop detection, etc.).
- **NCP (Network Control Protocol):** Negotiates settings for higher-layer protocols (example: IP); one NCP per network layer protocol.

### PPP Frame Structure & Encapsulation
PPP uses encapsulation to wrap data for transmission.
- **Flag:** Start/end of frame marker
- **Address / Control:** Standard bytes for broadcast and link control
- **Protocol:** Identifies the network layer protocol (1–3 bytes)
- **Data (Payload):** Actual data (up to 1500 bytes)
- **FCS:** 2–4 bytes for error checking

### Point-to-Point Protocol over Ethernet (PPPoE)
PPPoE allows PPP features (authentication, compression, encryption support) to work over Ethernet, which is multi-access (many devices share the same medium).

#### How PPPoE Works
- **Mechanism:** Encapsulates a PPP frame inside an Ethernet frame.
- **Discovery Stage:** Creates a Session ID so traffic reaches the correct device (MAC-based identification).
- **Common Use Case:** Popular in DSL broadband, enabling ISPs to authenticate users and manage sessions using Ethernet equipment.

### PPP vs PPPoE (Summary Table)

| Feature | PPP | PPPoE |
|---|---|---|
| Connection Type | Point-to-Point | Ethernet Multi-access |
| Authentication | PAP, CHAP | Often PAP |
| Addressing | Direct endpoint link | Session ID + MAC discovery |
| Common Use | Dedicated links | DSL and consumer broadband |

---

## Wide Area Network Technologies

### Wide Area Networks (WAN)
A WAN (Wide Area Network) connects networks across multiple physical locations (such as offices in different cities) while operating like one unified network. It becomes necessary when a LAN grows beyond a single site.

### The WAN Architecture
A typical WAN setup includes clear boundaries and ISP-managed infrastructure:
- **Demarcation Point (Demarc):** The point where the customer network ends and the ISP network begins.
- **Local Loop:** The physical connection from the demarc to the ISP’s regional facility (can be T-carrier or high-speed fiber/optical).
- **ISP Core Network:** The provider backbone that carries data between sites and connects to the Internet.

### Evolving From LAN to WAN
As a company expands, network requirements evolve in stages:
- **Stage 1 (Single Office LAN):** Uses private (non-routable) IPs, NAT, DHCP, local DNS, and one ISP Internet link.
- **Stage 2 (Remote Access):** Uses a VPN server (often reachable via port forwarding) so traveling employees can securely access internal resources.
- **Stage 3 (Multiple Offices):** Uses a WAN so an entire second office can access resources as if both offices are part of the same network.

### Data Link Layer in WANs
WANs often use different Layer 2 (Data Link) protocols than Ethernet:
- **WAN Layer 2 Protocols:** Used to transport data between sites over long distances through the ISP network.
- **Internet Core Similarity:** Some WAN transport protocols are also used inside the core of the Internet, not just private company networks.

### Quick Comparison: LAN vs WAN

| Feature | LAN (Local Area Network) | WAN (Wide Area Network) |
|---|---|---|
| Span | One building/campus | Multiple cities/countries |
| Typical Protocol | Ethernet | ISP/WAN Layer 2 protocols |
| Ownership | Owned by the organization | Leased/managed by ISP |
| Key Devices | Switches, Access Points | Routers + ISP link (local loop) |

---

## WAN Protocols
- **WAN (Wide Area Network):** Connects geographically separated LANs, often using ISP-provided links.
- **Regional WAN:** Multiple LAN sites connected using leased ISP equipment/cables.
- **WAN Security:** VPNs protect traffic when WAN links run over the public Internet.

### Physical vs Software-Based WANs
- **WAN Router (Edge/Border Router):** Hardware router connecting an organization’s LAN to a carrier network.
  - **WAN side:** Digital modem interface (OSI link layer)
  - **LAN side:** Ethernet interface
- **SD-WAN (Software-Defined WAN):** Software-based WAN solution designed for cloud environments.
  - Easier to implement/manage than traditional WANs
  - Often cheaper by reducing reliance on expensive leased ISP lines
  - Can work alone or alongside traditional WANs

### WAN Optimization Techniques
- **Compression:** Reduces file size to improve transmission efficiency (same algorithm needed at both ends).
- **Deduplication:** Stores only one copy of a file and uses pointers for duplicates (saves storage + improves backups).
- **Protocol Optimization:** Improves performance for apps needing high bandwidth + low latency.
- **Local Caching:** Keeps local copies of frequently accessed files to reduce repeated WAN transfers.
- **Traffic Shaping:** Controls traffic flow to improve performance:
  - Bandwidth throttling: Reduces traffic volume during peak times
  - Rate limiting: Caps maximum speed
  - Prioritization algorithms: Gives priority to critical traffic (example: internal WAN traffic over public Internet use)

### WAN Protocols / Technologies
- **Packet Switching:** Breaks messages into packets with headers for destination + reassembly; packets can be resent if corrupted.
- **Frame Relay:** Older WAN technology using packet switching at physical + data link layers.
  - **PVC (Permanent Virtual Circuit):** Always-on long-term connection
  - **SVC (Switched Virtual Circuit):** Temporary session-based connection
- **ATM (Asynchronous Transfer Mode):** Older tech using fixed-size cells; mostly replaced by IP-based networks.
- **HDLC (High-Level Data Link Control):** Data link encapsulation protocol with error control + flow control.
  - **NRM:** Primary must permit secondary to transmit
  - **ARM:** Secondary can initiate communication
  - **ABM:** Both sides can initiate freely
- **SONET/SDH:** Fiber-based protocols defining point-to-point transport over optical links.
- **MPLS (Multiprotocol Label Switching):** Improves routing using short labels instead of long IP table lookups.

---

## Point-to-Point VPNs
**Point-to-Point (Site-to-Site) VPNs:** A Site-to-Site VPN creates an encrypted tunnel between two physical networks (two offices/branches).

- **Device-Based VPN Tunnel:** The VPN tunnel is built and maintained by network devices such as routers or firewalls, not by individual employees.
- **Transparent User Access:** Users at both sites can access shared resources as if they are on the same internal network, without running VPN software on their computers.

### Why Businesses Use Site-to-Site VPNs Instead of Traditional WAN
- **Traditional WAN:** Best for very high-speed, guaranteed performance connections (but usually expensive).
- **Cloud Impact:** Many business systems are now hosted externally (Cloud providers).
  - Example: Instead of running an internal email server, companies use Email as a Service.
- **Result:** Since fewer services are hosted inside a single office, companies can rely on standard Cable/DSL/Fiber Internet links and secure inter-office communication using VPN tunnels.

### WAN vs Site-to-Site VPN (Quick Comparison)

| Feature | Traditional WAN | Site-to-Site VPN |
|---|---|---|
| Connection Type | Dedicated leased line | Encrypted tunnel over Internet |
| Cost | High | Lower |
| Speed | High and predictable | Depends on ISP performance |
| Management | ISP-managed | IT-managed |

---

## Wireless Networking Technologies (802.11 / Wi-Fi)
- **Wireless networking:** Networking without physical cables, using radio waves.
- **Wi-Fi standards:** Defined by IEEE 802.11 (the “802.11 family”).
- **Frequency band:** A specific range of radio spectrum used for communication (example: FM radio 88–108 MHz).
- **Common Wi-Fi bands:** 2.4 GHz and 5 GHz.
- **Common 802.11 versions (adoption order):** 802.11b, 802.11a, 802.11g, 802.11n, 802.11ac.
- **Improvement trend:** Newer 802.11 versions usually provide higher speeds and/or support more devices at once.
- **OSI layers:** 802.11 mainly operates at the Physical layer + Data Link layer.

### 802.11 Frame
- **Frame Control field (16 bits):** Tells how the frame should be processed (includes 802.11 version info).
- **Duration field:** Indicates how long the transmission lasts so receivers know how long to listen.
- **Four Address fields (each 6 bytes / MAC addresses):**
  - **Source Address:** MAC of the sending device
  - **Destination Address:** Intended destination on the network
  - **Receiver Address:** MAC of the access point that should receive the frame
  - **Transmitter Address:** MAC of the device that transmitted the frame
  - Often Destination = Receiver, and Source = Transmitter, but not always.
- **Access Point (AP):** Bridges the wireless network to the wired network.
- **Association:** Wireless devices connect to an AP (usually closest / strongest signal / less interference).
- **Sequence Control field (16 bits):** Holds a sequence number to keep frames in order.
- **Data Payload:** Contains higher-layer protocol data.
- **Frame Check Sequence (FCS):** Checksum for CRC error detection (similar to Ethernet).

---

## Wi-Fi 6
### Wi-Fi 6 (802.11ax) and Wi-Fi 6E

#### Wi-Fi 6 Overview
Wi-Fi 6 (802.11ax) represents a major shift in wireless networking, focusing on efficiency and high-density performance instead of only peak “hero speeds.” It is designed for environments where many devices connect at the same time.

#### Key Performance Benefits
- **Higher Throughput:** Wider channels and better client grouping enable faster upload/download speeds.
- **Capacity Expansion:** Channel width increased from 80 MHz (Wi-Fi 5) → 160 MHz (Wi-Fi 6).
- **More Streams:** Supports 8×8 streams (vs 4×4 in Wi-Fi 5) to serve more clients simultaneously.
- **Power Efficiency (TWT):** Target Wake Time (TWT) lets devices sleep and wake only when needed → improves battery life (especially for IoT/mobile devices).

#### Core Enabling Technologies (Layer 1 + Layer 2)
- **OFDMA:** Splits one channel into smaller sub-channels so the AP can communicate with multiple devices at the same time.
- **MU-MIMO:** Enables simultaneous data transfer for high-bandwidth apps (video calls, streaming).
- **1024-QAM:** Encodes more bits per signal → higher throughput than 256-QAM.
- **Transmit Beamforming:** Focuses signal toward a device instead of broadcasting equally → improves speed and range.
- **160 MHz Channel Utilization:** More bandwidth space for data transmission.

#### Wi-Fi 6E (6 GHz Extension)
Wi-Fi 6E extends Wi-Fi 6 into the 6 GHz band, adding more capacity and improving performance.
- **New Spectrum:** Adds 6 GHz alongside 2.4 GHz and 5 GHz.
- **More Channels:** Adds 14× 80 MHz channels and 7× 160 MHz channels.
- **Cleaner Band:** Older devices cannot use 6 GHz → less interference, ideal for VR/AR and HD streaming.

### Quick Comparison: Wi-Fi 5 vs Wi-Fi 6

| Feature | Wi-Fi 5 (802.11ac) | Wi-Fi 6 (802.11ax) |
|---|---|---|
| Max Channel Width | 80 MHz | 160 MHz |
| Modulation | 256-QAM | 1024-QAM |
| Efficiency | OFDM | OFDMA |
| Streams | 4×4 | 8×8 |
| Power Saving | Basic | Target Wake Time (TWT) |

---

## Alphabet Soup
### Wi-Fi Frequencies and 802.11 Standards (Alphabet Soup)

#### Core Idea
Wi-Fi operates mainly at the Physical Layer (Layer 1) and Data Link Layer (Layer 2) using microwave radio frequencies to transmit data.  
Understanding the 802.11 “alphabet soup” helps troubleshoot range, speed, congestion, and interference.

### 2.4 GHz vs 5 GHz (Quick Comparison)

| Feature | 2.4 GHz Band | 5 GHz Band |
|---|---|---|
| Range (Indoor) | ~150 ft (better wall penetration) | ~50 ft (blocked easily by walls) |
| Max Speed | Up to ~600 Mbps (best-case) | Over ~2 Gbps (ideal conditions) |
| Channels | Fewer (≈11–14 depending on country) | Many more channels available |
| Congestion / Interference | High (Bluetooth, microwaves, overlapping Wi-Fi) | Low (less congestion/interference) |
| Security Risk | Higher interception risk due to long range | Lower risk due to shorter range |

### Evolution of IEEE 802.11 Standards
IEEE updates Wi-Fi standards to improve bit rates, modulation, channel width, and efficiency.
- **802.11b (Wi-Fi 1)** → 2.4 GHz, 11 Mbps, overlapping channels (more interference)
- **802.11a (Wi-Fi 2)** → 5 GHz, 54 Mbps, shorter range
- **802.11g (Wi-Fi 3)** → 2.4 GHz, 54 Mbps (b-band with a-speed)
- **802.11n (Wi-Fi 4)** → 2.4/5 GHz, introduced MIMO + Channel Bonding, up to 600 Mbps
- **802.11ac (Wi-Fi 5)** → mainly 5 GHz, wider channels (80/160 MHz), DL MU-MIMO, multi-client sending
- **802.11ax (Wi-Fi 6)** → high-density optimization, OFDMA + MU-MIMO, better performance in crowded networks, requires WPA3
- **Wi-Fi 6E** → adds 6 GHz band, more channels, reduced interference, speeds up to 10 Gbps (shared)

### Top Technical Concepts
- **MIMO / MU-MIMO:** Multiple antennas improve throughput; MU-MIMO lets AP serve multiple clients at once
- **Channel Bonding:** Combines channels to increase throughput (40/80/160 MHz)
- **OFDMA:** Splits bandwidth efficiently so multiple devices can transmit with less congestion
- **DFS:** Required in parts of 5 GHz to avoid interference with radar/satellite systems
- **Infrastructure Mode:** Clients connect to a Wireless Access Point (WAP) that bridges to the wired Ethernet network

---

## IoT Data Transfer Protocols
### IoT Data Transfer Protocols (Application Layer – Layer 7)
IoT devices often operate in constrained environments (low power, limited memory, and unstable networks).  
To support reliable communication, IoT uses specialized Application Layer protocols to collect, format, and transfer data.

### Core Communication Models

#### 1) Request/Response Model
- **How it works:** A client requests data → server sends a response
- **Nature:** Direct and synchronous
- **Examples:** HTTP/HTTPS, CoAP

#### 2) Publish/Subscribe Model
- **How it works:** A publisher sends data to a broker → subscribers receive updates by topic/channel
- **Nature:** Asynchronous and decoupled
- **Examples:** MQTT, AMQP, DDS

### Primary IoT Application Layer Protocols

| Protocol | Model | Key Characteristics | Common Use Case |
|---|---|---|---|
| HTTP/HTTPS | Request/Response | ASCII formatting, larger overhead, uses TCP/UDP | Web dashboards, document-style communication |
| MQTT | Publish/Subscribe | Binary format, 2-byte header, supports QoS, uses TCP + SSL/TLS | Low-power telemetry, sensor-to-cloud messaging |
| CoAP | Request/Response | Lightweight HTTP-like REST protocol for constrained devices | Smart energy, building automation |
| AMQP | Publish/Subscribe | Open standard, reliable, secure, reduces vendor lock-in | Enterprise and cross-platform messaging |
| DDS | Publish/Subscribe | Middleware-based, data-centric, very low latency, scalable QoS control | Industrial IoT ecosystems requiring high performance |
| XMPP | Decentralized messaging | Extensible, flexible, built on Jabber | Chat, collaboration, presence systems |

### Efficiency & Security Highlights
- **Header Overhead:**
  - HTTP is heavier (text-based headers)
  - MQTT is efficient (binary + small headers) → saves bandwidth and battery
- **QoS (Reliability Control):**
  - MQTT/DDS support QoS settings (best effort vs guaranteed delivery)
- **Encryption:**
  - HTTPS + MQTT commonly secure traffic using SSL/TLS
  - Strong security is critical in industrial IoT where sensor data may trigger automated actions

### M2M Architecture Summary
- **REST:** Web-style communication (HTTP/CoAP)
- **SOA:** Common in industrial automation exchanges
- **Message-Oriented:** Asynchronous messaging for distributed systems

---

## Wireless Network Configurations
Wireless networks are classified based on their topology and how devices communicate with network infrastructure. Understanding Ad-hoc, WLAN (Infrastructure), and Mesh configurations is essential for selecting the correct wireless design based on scale, performance, and reliability requirements.

### 1. Ad-hoc Networks (Peer-to-Peer)
A basic wireless configuration where devices communicate directly with each other without fixed infrastructure such as routers or access points.

**Mechanics:**
- Every node functions as both a client and a relay, forwarding data for other nodes within range.

**Common Use Cases:**
- Direct Device Sharing: Smartphones exchanging files, photos, or contacts.
- Industrial/Warehouse Systems: Equipment communicating locally without internet access.
- Disaster Recovery: Emergency communication when traditional network infrastructure is unavailable.

**Limitation:**
- Poor scalability and performance degradation as the number of nodes increases.

### 2. Wireless LAN (WLAN / Infrastructure Mode)
The most common wireless configuration used in homes and enterprise environments.

**Mechanics:**
- Wireless devices associate with one or more Access Points (APs).
- APs are physically connected to a wired LAN that provides routing, DNS, DHCP, and internet access.

**Architecture:**
- The wired LAN handles core networking functions.
- APs bridge wired Ethernet (802.3) and wireless Wi-Fi (802.11).

**Performance Characteristics:**
- High reliability and throughput due to dedicated wired backhaul links.

### 3. Wireless Mesh Networks
A hybrid topology combining features of ad-hoc and infrastructure-based networks.

**Mechanics:**
- Multiple wireless access points interconnect wirelessly, forming a mesh.
- Only one or a few nodes require a wired connection to the internet.

**Key Advantages:**
- Self-Healing: Traffic automatically reroutes if a node fails.
- Scalable Coverage: Ideal for campuses, warehouses, and large buildings.
- Reduced Cabling Costs: No Ethernet required for every access point.

**Routing Behavior:**
- Uses dynamic routing algorithms to select the most efficient path to the wired gateway.

### Summary Table: Wireless Network Configurations

| Feature | Ad-hoc | WLAN (Infrastructure) | Mesh |
|---|---|---|---|
| Infrastructure | None | Wired Access Points | Interconnected APs |
| Backhaul | Peer-to-Peer | Wired Ethernet | Wireless (Multi-hop) |
| Resilience | Low | Medium | High (Self-healing) |
| Scalability | Poor | High | Excellent |

---

## Wireless Channels
- Channels are smaller subdivisions of a wireless frequency band used to reduce interference and collisions.
- Collision domains occur when multiple wireless devices transmit at the same time, causing collisions and slowing communication.
- Unlike wired networks (which use switches), wireless networks cannot fully eliminate collisions because devices share the airspace.
- Wi-Fi frequency bands (e.g., 2.4 GHz) are ranges of frequencies, not single values, and are divided into multiple channels.
- Channel width causes overlap between nearby channels; overlapping channels interfere with each other.
- In 2.4 GHz (802.11b), only channels 1, 6, and 11 do not overlap and are preferred for deployment.
- Channel availability varies by country due to regulatory rules.
- Modern access points can auto-select or dynamically change channels, but congestion can still occur in dense areas.
- Proper channel planning is essential for troubleshooting slow or unreliable wireless networks.
- Goal in wireless design: minimize channel overlap and collision domains for better performance.

---

## Wireless Security
### Wireless Security and Encryption
Wireless communication is broadcast through the air, so anyone in range can intercept signals. Unlike wired links, privacy must be created using encryption.

### Encryption Strength
Encryption protects data even if intercepted.  
Longer key length = exponentially harder to crack.

| Protocol | Key Length | Status |
|---|---:|---|
| WEP | 40-bit | Obsolete and insecure, crack able in minutes |
| WPA | 128-bit | Legacy, stronger than WEP |
| WPA2 | 256-bit | Current common standard, strong security |

### Core Concepts
- Wired = private point-to-point link
- Wireless = broadcast medium, requires encryption
- WEP failed due to very short keys
- WPA2 with 256-bit keys is effectively unbreakable with current computing power

### MAC Filtering (Access Control)
- Only allows listed device MAC addresses to connect
- Does not encrypt traffic
- MAC addresses can be spoofed, so this is only an extra barrier

### Best Practice
Use strong encryption (WPA2/WPA3) as primary security; treat MAC filtering only as a secondary control.

---

## Protocols & Encryption
### WPA3 Protocols and Encryption
- WPA3 is the newest Wi-Fi security standard, built to fix WPA2 weaknesses and resist modern high-power attacks.
- Focus areas: stronger authentication, stronger encryption, and protection even if passwords are weak.

### WPA3-Personal (Home/Individual Use)
- Uses SAE (Simultaneous Authentication of Equals) instead of WPA2-PSK.
  - Proves both client and access point know the key without sending it.
  - Blocks offline dictionary and brute-force attacks.
  - Mitigates KRACK attacks.
- Forward Secrecy: previously captured traffic stays encrypted even if the password is later exposed.
- Natural Passwords: easier human passwords are allowed without large security loss.

### WPA3-Enterprise (Business/High Security)
- GCMP-256 (AES-256): stronger integrity and confidentiality than WPA2 128-bit CCMP.
- OWE (Opportunistic Wireless Encryption): encrypts traffic on open/public Wi-Fi without shared passwords.
- DPP (Device Provisioning Protocol): secure onboarding via QR code or NFC; replaces WPS.
- 384-bit HMAC (SHA-384): verifies message integrity and detects tampering.

### Key Cryptographic Improvements
- ECDHE + ECDSA: modern key exchange and authentication with high security and better performance; protects against MitM attacks.
- Protected Management Frames (PMF): mandatory; prevents fake deauthentication/disconnect attacks.

### Practical Note
- WPA3 requires compatible hardware; mixed WPA2/WPA3 “transition mode” is often used for legacy devices.

---

## Cellular Networking
- Cellular (mobile) networks provide wireless Internet access over long distances using radio waves.
- They use dedicated frequency bands that can cover many kilometers or miles.
- The network is divided into “cells,” each served by a cell tower (similar to a large-range access point).
- Neighboring cells use non-overlapping frequencies to reduce interference.
- Many devices use cellular connectivity, including phones, tablets, laptops, and modern cars.

### Key Similarities & Differences with Wi-Fi

| Feature | Wi-Fi (802.11) | Cellular Networking |
|---|---|---|
| Medium | Radio Waves | Radio Waves |
| Range | Short (typically <100 meters) | Long (multiple kilometers/miles) |
| Interference Mitigation | Channels (e.g., 1, 6, 11) | Frequency bands assigned to cells |
| Mobility | Limited to local AP range | High; supports "handoffs" between cells |

---

## Mobile Device Networks
- **Multiple Radios:** Mobile devices use Wi-Fi, cellular, and Bluetooth to balance speed, cost, and battery life.
- **Radio Toggles:** Each radio can be turned on/off separately; airplane mode disables all at once.
- **First Troubleshooting Step:** Always check if the required radio is accidentally turned off.
- **Connection Priority:** Devices prefer the most reliable and least expensive network.
- **Metered vs Non-metered:** Cellular data is usually metered, so devices switch to Wi-Fi when available.
- **Manual Override:** Turn off Wi-Fi or cellular to force the device to use the other network.
- **Signal Attenuation:** Wireless signals weaken with distance from the access point or tower.
- **Interference/Obstacles:** Walls, metal, and even the human body can reduce signal strength.
- **Device Position:** How the device is held or worn can partially block the internal antenna.
- **Bluetooth (Short-Range PAN):** Used for peripherals like headphones, keyboards, and mice.
- **Pairing:** Devices exchange keys/PIN so they can recognize and auto-reconnect later.
- **Bluetooth Fix:** If unstable, turn Bluetooth on, “forget” the device, and pair again.

### Quick Support Checklist
- No connection → Check radio toggles and airplane mode
- Weak/unstable signal → Move closer, reduce obstacles/interference
- Blocked websites on Wi-Fi → Disable Wi-Fi to use cellular
- Bluetooth device not working → Forget and re-pair the device

---

## Mobile Device Networks (IoT Wireless Network Protocols)
- IoT devices choose wireless protocols based on range, power use, data rate, and need for Internet vs local communication.

### General / High-Bandwidth Connectivity
- **Wi-Fi (802.11):** Best for integrating IoT into existing IP/Internet networks.
  - 2.4 GHz: Longer range, more interference and congestion.
  - 5 GHz: Higher speed, more channels, shorter range.
- **Bluetooth:** Short-range PAN (~100 ft) for control, setup, and small data transfers.
- **NFC:** Very short range (<2 in), used for contactless payments, ID, and quick pairing; protect with RFID/NFC sleeves against skimming.

### Low-Power Mesh / Smart Device Protocols
- **IEEE 802.15.4:** Low-power, 128-bit encrypted base standard for many IoT meshes.
- **ZigBee:** Interoperable, self-healing mesh for smart homes and commercial IoT.
- **Z-Wave:** Low-power mesh on ~908 MHz (less interference), long indoor range.
- **Thread:** IPv6-based open mesh, no proprietary gateways required.
- **Wireless Mesh Networks (WMN):** Nodes relay traffic for each other; self-healing; can be full or partial mesh.

### Long-Range / Wide-Area IoT
- **LoRaWAN:** Very long-range, low-power protocol for widely dispersed, battery-powered sensors (e.g., city or agricultural IoT).

### Protocol Comparison

| Protocol | Range | Key Feature | Common Application |
|---|---|---|---|
| Wi-Fi | Medium | High Speed/IP Native | Security Cameras, Hubs |
| ZigBee/Z-Wave | Medium | Mesh/Self-Healing | Smart Bulbs, Sensors |
| Bluetooth | Short | PAN/Easy Pairing | Wearables, Thermostats |
| NFC | Very Short | Physical Proximity | Payments, Keycards |
| LoRaWAN | Very Long | Wide Area Coverage | Industrial/Outdoor IoT |

---

## Glossary terms: Wireless Networking, Broadband Internet, and Network Structures

### 1. Wireless Fundamentals (802.11 / Wi-Fi)
Wireless networks use radio waves instead of cables.
- **WLAN:** Wireless devices connect through Wireless Access Points (APs) that bridge to the wired LAN.
- **Channels:** Subsections of a frequency band; choosing non-overlapping channels reduces interference and congestion.
- **Collision Domain:** All wireless devices share the air, so simultaneous transmissions collide and must be retried.
- **Security:**
  - **WEP:** Obsolete, weak 40-bit encryption.
  - **WPA/WPA2:** Stronger encryption (128/256-bit).
  - **MAC Filtering:** Only approved device MAC addresses can join (access control, not encryption).

### 2. Broadband Internet Technologies
Broadband = always-on, high-speed Internet (not dial-up).
- **DSL:** Internet over phone lines without blocking voice calls.
  - **ADSL:** Faster download than upload.
  - **SDSL:** Equal upload and download.
  - **DSLAM:** ISP device that aggregates many DSL lines.
- **Cable Internet:** Home cable modem connects to ISP CMTS; bandwidth is shared in the local area.
- **T-Carrier (e.g., T1):** Early dedicated high-speed business links.

### 3. Fiber (FTTx)
Fiber uses light, supports very high speed and long distance.
- **FTTH/FTTP:** Fiber directly to the home/premises.
- **FTTB:** Fiber to a building, copper inside.
- **FTTN:** Fiber to a neighborhood cabinet, copper for the last stretch.
- **ONT:** Converts fiber signals to standard Ethernet for local devices.

### 4. Network Topology and Mobility
- **WAN:** Connects multiple sites over ISP infrastructure.
- **Ad-Hoc Network:** Devices communicate directly without infrastructure.
- **Mesh Network:** Nodes relay traffic for each other; self-healing and extends coverage.
- **Bluetooth:** Short-range PAN for peripherals; requires device pairing.
- **Metered vs Non-metered:** Cellular data is usage-limited; Wi-Fi is usually unlimited.

### 5. 802.11 Wireless Frame Fields
- **Frame Control:** How the frame should be handled.
- **Duration:** How long the channel will be busy.
- **Sequence Control:** Keeps frames in correct order.
- **Addresses:** Include source, destination, transmitter, and receiver (often the AP).

