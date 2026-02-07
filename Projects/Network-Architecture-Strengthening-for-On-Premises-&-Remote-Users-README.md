# Network Architecture Strengthening for On-Premises & Remote Users
  
---

## Project Scenario

An organization operates an on-premises office network that supports daily business operations such as email, web access, file sharing, and internal applications. As the company grows, more users and devices are added, and remote employees and other authorized remote users also require secure access to internal resources. The organization needs a strengthened network architecture that improves connectivity, security, scalability, and remote access protection.

---    

## Project Objective

To strengthen the network architecture for both on-premises and remote users by achieving the following goals:

- Provide stable Internet connectivity for office users
- Secure the network by blocking unwanted and malicious traffic
- Enable multiple internal devices to share one public IP address
- Automatically assign correct network settings to endpoints
- Ensure websites open properly using domain names (DNS resolution)
- Build a reliable and high-speed internal LAN environment
- Enable secure remote access for authorized remote users

---

## Main Physical Devices

![Main Physical Devices Hardware](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-04-Network-Architecture-Strengthening-for-On-Premises-%26-Remote-Users-Main-Physical-Endpoints.png)

* **Cloud Servers / Applications** *(remote servers in data centers)*
* **Network Cable** *(Ethernet Cat5e/Cat6 or Fiber Optical Cable)*
* **ISP Connection Box** *(Modem / ONU / ONT)*
* **Router** *(Gateway device)* + **Switch** *(LAN Switch — optional / for expanding LAN ports)*
* **User Devices** *(PCs / Laptops / Printers / Tablets / Smartphones / IoT Devices)*

---

## Server-to-User Network Flow (On-Premises: Public + Private)

```text
Internet / Public Servers (Public Network)
            |
           NAT
            |
      ROUTER / FIREWALL
     (Gateway + Security)
            |
     Office LAN (Private Network)
            |
         SWITCH
        /         \
[User Devices]   Network Services
(PCs/Laptops)   (DHCP + DNS)
```

---

## Cloud Server-to-Remote User Network Flow (Public + Private)

```text
Cloud Servers (Public Network)
            |
     Internet (Public Network)
            |
       VPN (Encrypted Tunnel)
            |
   ROUTER / FIREWALL (VPN Gateway)
            |
 Office LAN (Private Network)
            |
   [Remote User Devices (PCs/Laptops)]
```

---

## Cellular User-to-Office Network Flow (4G/5G: Public + Private)

```text
[Internal Hosts] (Servers, PCs)
            |
          SWITCH
            |
     Office LAN (Private Network)
            |
   ROUTER / FIREWALL (Enterprise Gateway)
            |
      VPN Gateway (Optional)
            |
     Internet (Public Network)
            |
   Mobile Core Network (4G/5G Core)
(SGW, PGW, UPF, Authentication, NAT/CGNAT)
            |
   Mobile Radio Access Network (RAN)
(BTS / NodeB / eNodeB / gNodeB)
            |
Cellular User Devices (Smartphone / Laptop with SIM)
```

---

## Cellular VPN Remote Access Flow (4G/5G: Public + Private)

```text
Internal Resources (Servers, Databases, Internal Apps)
            |
     Office LAN (Private Network)
            |
   ROUTER / FIREWALL (VPN Gateway)
            |
     VPN Tunnel (IPsec / SSL)
            |
      Internet (Public Network)
            |
     Mobile Core Network
            |
   Mobile Base Station (eNodeB / gNodeB)
            |
Cellular User Device (4G/5G)
```

---

## WLAN (Wireless LAN) Network Flow (Private + Public)

```text
Internet (Public Network)
        |
   ROUTER / FIREWALL
 (WAN Gateway + NAT + Security)
        |
Office LAN (Private Network)
        |
     SWITCH (LAN)
        |
 Wireless Access Point (Wi-Fi AP)
        |
Wireless Devices (Private Network Clients)
(Laptops / Smartphones / Tablets / IoT)
```

---

## Satellite WAN Connectivity Flow (Public + Private)
```text
Cloud Servers / Applications (Public Network)
            |
      Internet Backbone (Public)
            |
     Satellite ISP Gateway / NOC
            |
      Satellite Uplink (Earth Station)
            |
     Satellite (LEO/MEO/GEO Orbit)
            |
   Satellite Downlink (User Location)
            |
Satellite Dish + Modem (VSAT Terminal)
            |
   ROUTER / FIREWALL (NAT + Security)
            |
 Office LAN (Private Network)
            |
     SWITCH / Wi-Fi AP
            |
   User Devices (Private Clients)
```

---

## Cloud Server-to-User Devices Connection Flow (Real Example: Public + Private)

```text
[Cloud Servers / Applications] (Public Network)
     |
Internet (Public Network)
     |
[ISP DNS / ISP Servers] (Public Network)
     |
   ISP Network (Public Network)
     |
[ISP Connection Box / Modem / ONU]
     |
 WAN Cable (Public/WAN)
     |
   [Router] (Gateway)
     |
 Ethernet Cable (Private/LAN)
     |
[User Devices (PCs/Laptops)] (Private Network)
```

---

## Project Description (Steps)

### Step 1: Provide Internet Connectivity for On-Premises Users

**Device/Service:** **ROUTER**

* Configure the router to connect the internal office LAN to the Internet.
* Ensure the router functions as the default gateway for internal devices.

A **Router** is the **main gateway device** that connects the **local network (LAN)** to the **Internet (WAN)** and routes traffic between them.

**Inside a typical router, these built-in functions may exist:**

* **Routing (Gateway):** Sends traffic between LAN and WAN
* **NAT:** Allows many devices to share one public IP address
* **Basic Firewall:** Blocks or allows traffic using simple security rules
* **DHCP Server:** Assigns IP address, gateway, subnet mask, and DNS automatically
* **DNS Forwarding (DNS Relay):** Forwards DNS requests to ISP or public DNS servers
* **LAN Switch Ports:** Provides Ethernet ports for wired devices
* **Wi-Fi Access Point (Wireless routers):** Provides wireless connectivity

---

### Step 2: Strengthen Network Security and Block Unwanted Traffic

**Device/Service:** **FIREWALL**

* Deploy a firewall at the network edge to inspect inbound and outbound traffic.
* Apply security rules to allow trusted services and block unauthorized or suspicious connections.
* Reduce the risk of malware, intrusion attempts, and data exposure by enforcing controlled access policies.

**Firewall Snippet (Linux – UFW):**

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw enable
```

**Firewall Snippet (Windows – PowerShell):**

```powershell
Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled True
New-NetFirewallRule -DisplayName "Allow SSH" -Direction Inbound -Protocol TCP -LocalPort 22 -Action Allow
```

A **Firewall (Network Firewall)** exists on the network security device positioned between the **private network (LAN)** and the **public Internet (WAN)** to inspect, filter, and control inbound and outbound traffic.

**Firewall commonly exists on:**

1. Between the Internet (WAN) and the Office Network (LAN) *(most common)*
2. Between internal network segments (LAN-to-LAN / VLAN-to-VLAN)
3. In front of critical servers (DMZ / server zone)
4. On individual devices (host-based firewall)
5. In cloud environments (cloud firewall / security groups)

---

### Step 3: Enable Shared Internet Access Using a Single Public IP

**Device/Service:** **NAT (Network Address Translation)**

* Configure NAT on the network edge (gateway) to translate private LAN IP addresses into one public IP address.
* Allow multiple internal devices to access the Internet securely and efficiently through a single public-facing IP.

**NAT Snippet (Linux Gateway – iptables):**

```bash
sudo sysctl -w net.ipv4.ip_forward=1

sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
sudo iptables -A FORWARD -i eth0 -o eth1 -m state --state RELATED,ESTABLISHED -j ACCEPT
```

**NAT Snippet (Windows Server – PowerShell):**

```powershell
New-NetNat -Name "OfficeNAT" -InternalIPInterfaceAddressPrefix "192.168.10.0/24"
```

**NAT (Network Address Translation)** exists on the network device that sits between the **private network (LAN)** and the **public Internet (WAN)**.

**NAT commonly exists on:**

1. Router *(home and small office networks)*
2. Firewall *(business/enterprise networks)*
3. Layer 3 switch *(if used as the gateway)*
4. Server acting as a gateway *(Linux/Windows)*
5. Cloud gateway services *(NAT Gateway)*

---

### Step 4: Automate Network Configuration for Endpoints

**Device/Service:** **DHCP (Dynamic Host Configuration Protocol)**

* Enable DHCP to automatically assign:

  * IP Address
  * Subnet Mask
  * Default Gateway
  * DNS Server
* Reduce manual configuration errors and improve efficiency for new device connections.

**DHCP** exists on the network service/device that automatically assigns IP configuration to client devices inside the LAN.

**DHCP commonly exists on:**

1. Router
2. Windows Server
3. Linux Server
4. Dedicated DHCP Server / Appliance
5. Firewall
6. Cloud virtual networks (built-in DHCP)

---

### Step 5: Ensure Domain Name Access Works Correctly

**Device/Service:** **DNS (Domain Name System)**

* Configure DNS services so users can access websites by name (example: **google.com**).
* Resolve issues where websites do not open by domain name, but work by IP address.

**DNS (Domain Name System)** exists on the network service/server that translates domain names into IP addresses so devices can access websites and services correctly.

**DNS commonly exists on:**

1. ISP DNS Servers
2. Public DNS Services
3. Router DNS forwarding
4. Windows Server DNS
5. Linux DNS server
6. Cloud DNS services

---

### Step 6: Improve Internal LAN Connectivity and Performance

**Device/Service:** **SWITCH**

* Install and configure switches to connect multiple computers and network devices.
* Ensure fast and reliable communication inside the office network.

A **Switch** exists inside the LAN to connect multiple devices and enable fast internal communication.

**Switch commonly exists in:**

1. Office LAN / On-Premises Network
2. Data centers / server rooms
3. Network closets / floor distribution
4. Home networks *(optional)*

---

### Step 7: Enable Secure Remote Access for Authorized Remote Users

**Device/Service:** **VPN (Virtual Private Network)**

* Deploy a VPN solution to allow authorized remote users to securely access internal office resources over the Internet.
* Encrypt all remote-access traffic to protect data confidentiality and prevent interception on public networks (Wi-Fi, ISP, or cellular).
* Enforce access control by allowing only authenticated users and approved devices to connect to the private network.
* Route remote user traffic into the Office LAN securely through the VPN gateway (router/firewall/server).

**VPN Snippet (WireGuard – Linux VPN Gateway Example):**

```bash
sudo apt update
sudo apt install wireguard -y
```

**Example WireGuard Server Config (`/etc/wireguard/wg0.conf`):**

```ini
[Interface]
Address = 10.10.10.1/24
ListenPort = 51820
PrivateKey = <SERVER_PRIVATE_KEY>

[Peer]
PublicKey = <CLIENT_PUBLIC_KEY>
AllowedIPs = 10.10.10.2/32
```

A **VPN (Virtual Private Network)** exists on a VPN gateway (router/firewall/server) and creates an encrypted tunnel across the Internet, allowing authorized remote users to access internal resources as if they were inside the office network.

**VPN commonly exists on:**

1. Firewall appliance (enterprise VPN gateway)
2. Router with VPN support
3. Dedicated VPN server (Linux/Windows)
4. Cloud VPN gateway services
5. Client devices (VPN client software for users)

---

## Project Conclusion

This project successfully strengthened the network architecture for on-premises and remote users by implementing routing, firewall protection, NAT, DHCP automation, DNS resolution, LAN switching, and VPN remote access. The improved design ensures secure connectivity, efficient network operations, and reliable access to internal resources for both office-based and remote users.

### Summary of Implemented Network Components

1. **Connect the Internet / Provide network access** — **ROUTER**
2. **Secure the network / Block unwanted traffic** — **FIREWALL**
3. **Allow many devices to share one public IP** — **NAT**
4. **Automatically assign IP, Gateway, Subnet Mask, DNS** — **DHCP**
5. **Fix website not opening by name (google.com), but IP works** — **DNS**
6. **Connect many computers inside the office LAN** — **SWITCH**
7. **Allow remote employees to access office network securely** — **VPN**

---

## Project Credit

* **Executed and Presented By:** Mohammad Aminul Islam *(SOC Analyst)*
* **Project Reference:** *The Bits and Bytes of Computer Networking* — Google IT Support Professional Certificate Program *(Coursera)*
* **Project Implementation and Documentation:** Mohammad Aminul Islam
* **Copyright and Trademarks:** © 2022 Google LLC. Google and the Google logo are trademarks of Google LLC. All other product and company names may be trademarks of their respective owners.

---
