## Project Title: **Network Architecture Strengthening for On-Premises & Remote Users**

---

## Project Scenario

An organization operates an on-premises office network that supports daily business operations such as email, web access, file sharing, and internal applications. As the company grows, more users and devices are added, and remote users also need secure access to internal resources. The organization requires a strengthened network architecture that improves connectivity, security, scalability, and remote access protection.

---

## Project Objective

To strengthen the network architecture for both on-premises and remote users by achieving the following goals:

* Provide stable Internet connectivity for office users
* Secure the network by blocking unwanted and malicious traffic
* Enable multiple internal devices to share one public IP address
* Automatically assign correct network settings to endpoints
* Ensure websites open properly using domain names (DNS resolution)
* Build a reliable and high-speed internal LAN environment
* Enable secure remote access for authorized remote users

---

## Server-to-User Network Flow (On-Premises)

```text
Internet / Servers (Public Network)
            |
           NAT
            |
      ROUTER / FIREWALL
     (Gateway + Security)
            |
   DHCP + DNS (Network Services)
            |
          SWITCH
            |
[User Devices / PCs / Laptops]
```

---


## Cloud Server-to-Remote User Network Flow

```text
Cloud Servers (Public Network)
            |
     Cloud Firewall / Security
            |
     Internet (Public Network)
            |
            VPN
            |
   ROUTER / FIREWALL (VPN Gateway)
            |
      [Remote User / Laptop]
```

---

## Cloud Server-to-Laptop Connection Flow (Real Example)

```text
[Cloud Servers / Websites]
     |
Internet (Public Network)
     |
[ISP DNS / ISP Servers]
     |
   ISP Network
     |
[ISP Connection Box / Modem / ONU]
     |
 WAN Cable
     |
   [Router]
     |
 Ethernet Cable (LAN)
     |
[User Laptop]
```

---


## Project Description (Steps)

#### Network Services Flow (End-to-End)

```text
1) ROUTER (Routes traffic between LAN and WAN) → Connect the Internet / Provide network access
      |
2) FIREWALL (Filters traffic using security rules) → Secure the network / Block unwanted traffic
      |
3) NAT (Network Address Translation) → Allow many devices to share one public IP
      |
4) DHCP (Dynamic Host Configuration Protocol) → Automatically assign IP, Gateway, Subnet Mask, DNS
      |
5) DNS (Domain Name System) → Fix website not opening by name (google.com), but IP works
      |
6) SWITCH (Connects devices inside the LAN) → Connect many computers inside the office LAN
      |
7) VPN (Virtual Private Network) → Allow remote employees to access office network securely
```

### Step 1: Provide Internet Connectivity for On-Premises Users

**Device/Service:** **ROUTER**

* Configure the router to connect the internal office LAN to the Internet.
* Ensure the router functions as the default gateway for internal devices.

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
**FIREWALL (Network Firewall) exists on the network security device positioned between the private network (LAN) and the public Internet (WAN) to inspect, filter, and control inbound and outbound traffic.**

**Firewall commonly exists on:**

1. **Between the Internet (WAN) and the Office Network (LAN)** *(most common)*

   * Protects the internal network from external threats.

2. **Between Internal Network Segments (LAN to LAN / VLAN to VLAN)**

   * Controls traffic between departments (example: HR vs IT vs Finance).

3. **In front of Critical Servers (Server Network / DMZ)**

   * Protects services like web servers, email servers, and application servers.

4. **On Individual Devices (Host-Based Firewall)**

   * Example: Windows Defender Firewall on a laptop or server.

5. **In Cloud Environments (Cloud Firewall / Security Groups)**

   * Controls access to cloud servers and services.

**Simply:** A **firewall** exists on the **network edge and security zones** to **filter traffic and block unauthorized access**.


---

### Step 3: Enable Shared Internet Access Using a Single Public IP

**Device/Service:** **NAT** *(Network Address Translation)*

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

**NAT** (**Network Address Translation**) exists on the **network device that sits between your private network (LAN) and the public Internet (WAN)**.

**NAT commonly exists on:**

1. **Router** *(most common in home and small office networks)*
2. **Firewall** *(very common in business/enterprise networks)*
3. **Layer 3 Switch** *(sometimes, if it is used as the gateway)*
4. **Server acting as a gateway** *(Linux/Windows running routing + NAT software)*
5. **Cloud gateway devices/services** *(NAT Gateway in cloud environments)*

**Simply:**
NAT is a **feature/service**, not a standalone device.
It exists on **whatever device is acting as the Internet gateway** for the network.

---

### Step 4: Automate Network Configuration for Endpoints

**Device/Service:** **DHCP**

* Enable DHCP to automatically assign:

  * IP Address
  * Subnet Mask
  * Default Gateway
  * DNS Server
* Reduce manual configuration errors and improve efficiency for new device connections.

**DHCP exists on the **network service/device** that automatically assigns IP configuration to client devices inside the LAN.**

**DHCP commonly exists on:**

1. **Router** *(home and small office networks)*
2. **Windows Server** *(enterprise environments using Active Directory)*
3. **Linux Server** *(ISC DHCP / dnsmasq, etc.)*
4. **Dedicated DHCP Server / Appliance**
5. **Firewall** *(many firewalls include DHCP service)*
6. **Cloud DHCP Service** *(built into cloud virtual networks, such as VPC/VNet)*

**Simply: DHCP (Dynamic Host Configuration Protocol) exists on the network service that automatically assigns IP address, subnet mask, default gateway, and DNS settings to client devices on the LAN.**

---

### Step 5: Ensure Domain Name Access Works Correctly

**Device/Service:** **DNS**

* Configure DNS services so users can access websites by name (example: **google.com**).
* Resolve issues where websites do not open by domain name, but work by IP address.

***DNS (Domain Name System)*** exists on the **network service/server** that translates **domain names** (like `google.com`) into **IP addresses** (like `142.250.x.x`) so devices can access websites and services correctly.

1. **ISP DNS Servers** *(public Internet DNS provided by your Internet provider)*
2. **Public DNS Services** *(example: Google DNS, Cloudflare DNS)*
3. **Router** *(small networks often forward DNS requests)*
4. **Windows Server DNS** *(enterprise networks, often with Active Directory)*
5. **Linux DNS Server** *(BIND, dnsmasq, Unbound, etc.)*
6. **Cloud DNS Services** *(DNS managed in cloud environments)*

**Simply: DNS (Domain Name System) exists on a DNS server/service that resolves domain names into IP addresses to ensure users can access websites and network services by name.**

---

### Step 6: Improve Internal LAN Connectivity and Performance

**Device/Service:** **SWITCH**

* Install and configure switches to connect multiple computers and network devices.
* Ensure fast and reliable communication inside the office network.

A **switch** exists inside the **Local Area Network (LAN)** to connect multiple devices and enable fast internal communication.

***Switch commonly exists in:***

1. **Office LAN / On-Premises Network** *(most common)*
2. **Data Centers / Server Rooms** *(to connect servers, storage, and core devices)*
3. **Network Closets / Floor Distribution Areas** *(access switches for each floor)*
4. **Home Networks** *(optional, to add more Ethernet ports)*

**Simply: SWITCH exists within the internal LAN to connect computers, printers, and servers, allowing devices to communicate efficiently using Ethernet switching.**


---

### Step 7: Enable Secure Remote Access for Remote Users

**Device/Service:** **VPN**

* Configure VPN access for remote users to connect to the office network securely.
* Encrypt traffic to protect sensitive data and internal resources from exposure.

A **VPN** exists on the **remote access gateway** that allows remote users to connect securely to the private network over the Internet.

***VPN commonly exists on:***

1. **Firewall Appliance** *(most common in enterprise networks)*
2. **Router** *(many routers support VPN features)*
3. **Dedicated VPN Server** *(Windows Server / Linux server running VPN software)*
4. **Cloud VPN Gateway** *(VPN service in cloud environments)*
5. **Client Devices (VPN Client Software)** *(laptop/phone uses VPN app to connect)*

**Simply: VPN exists on a VPN gateway (router/firewall/server) that creates an encrypted tunnel over the Internet, allowing authorized remote users to securely access internal network resources.**


---

## Project Conclusion

This project successfully strengthened the network architecture for on-premises and remote users by implementing routing, firewall protection, NAT, DHCP automation, DNS resolution, LAN switching, and VPN remote access. The improved design ensures secure connectivity, efficient network operations, and reliable access to internal resources for both office-based and remote users.

---

## **Project Credit**

* **Executed and Presented By:** Mohammad Aminul Islam *(SOC Analyst)*
* **Project Reference Source:** *The Bits and Bytes of Computer Networking* — Google IT Support Professional Certificate Program *(Coursera)*
* **Project Implementation and Documentation:** Mohammad Aminul Islam
* **Copyright and Trademarks:** © 2022 Google LLC. Google and the Google logo are trademarks of Google LLC. All other product and company names may be trademarks of their respective owners.

---
