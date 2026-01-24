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

## Project Description (Steps)

### Step 1: Provide Internet Connectivity for On-Premises Users

**Device/Service:** ROUTER

* Configure the router to connect the internal office LAN to the Internet.
* Ensure the router functions as the default gateway for internal devices.

---

### Step 2: Strengthen Network Security and Control Traffic

**Device/Service:** FIREWALL

* Deploy a firewall to monitor and filter inbound and outbound traffic.
* Block unauthorized connections and enforce security policies.

---

### Step 3: Enable Shared Internet Access Using a Single Public IP

**Device/Service:** NAT *(Network Address Translation)*

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

NAT (**Network Address Translation**) exists on the **network device that sits between your private network (LAN) and the public Internet (WAN)**.

**NAT commonly exists on:**

1. **Router** *(most common in home and small office networks)*
2. **Firewall** *(very common in business/enterprise networks)*
3. **Layer 3 Switch** *(sometimes, if it is used as the gateway)*
4. **Server acting as a gateway** *(Linux/Windows running routing + NAT software)*
5. **Cloud gateway devices/services** *(NAT Gateway in cloud environments)*

**Key point**

NAT is a **feature/service**, not a standalone device.
It exists on **whatever device is acting as the Internet gateway** for the network.

---

### Step 4: Automate Network Configuration for Endpoints

**Device/Service:** DHCP

* Enable DHCP to automatically assign:

  * IP Address
  * Subnet Mask
  * Default Gateway
  * DNS Server
* Reduce manual configuration errors and improve efficiency for new device connections.

---

### Step 5: Ensure Domain Name Access Works Correctly

**Device/Service:** DNS

* Configure DNS services so users can access websites by name (example: **google.com**).
* Resolve issues where websites do not open by domain name, but work by IP address.

---

### Step 6: Improve Internal LAN Connectivity and Performance

**Device/Service:** SWITCH

* Install and configure switches to connect multiple computers and network devices.
* Ensure fast and reliable communication inside the office network.

---

### Step 7: Enable Secure Remote Access for Remote Users

**Device/Service:** VPN

* Configure VPN access for remote users to connect to the office network securely.
* Encrypt traffic to protect sensitive data and internal resources from exposure.

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
