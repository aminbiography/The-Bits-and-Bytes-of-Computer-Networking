# Project Title

## IPv4 to IPv6 Transition: Addressing, Header Structure, and Tunneling

---

# Project Objective

To evaluate IPv4 to IPv6 transition concepts by analyzing:

* IPv4 limitations and address exhaustion
* IPv6 addressing formats and compression
* IPv6 base header structure
* IPv4-mapped IPv6 addresses
* IPv6-over-IPv4 tunneling mechanisms

This project demonstrates conceptual understanding of IPv6 adoption in modern networks.

---

# Project Scenario

With global IPv4 exhaustion, organizations are transitioning to IPv6.
A network/SOC analyst must understand:

1. IPv4 limitations
2. IPv6 addressing and structure
3. Transition and coexistence mechanisms
4. Tunneling techniques

This project explores these areas using structured technical analysis.

---

# Project Description

---

# IPv4 Background (Context)

---

## Step V4-1 - Limited Address Space

IPv4 uses a 32-bit address space.

* ~4.3 billion total addresses
* Heavy reliance on NAT
* Address exhaustion globally

### Interpretation

IPv4 limitations are the primary driver for IPv6 adoption.

---

## Step V4-2 - Simpler but Constrained Design

IPv4 header includes:

* Variable header length
* Broadcast traffic
* Limited scalability

### Interpretation

IPv4 works but cannot support modern Internet growth alone.

---

# IPv6 Addressing Analysis

---

## Step A1 - IPv6 Address Space (128-bit)

IPv6 uses 128-bit addressing.

### Screenshot Evidence

![IPv6 Space](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-05-Total-IPv6-Address-Space-(2¹²⁸).png)

### Interpretation

Provides enormous scalability for future networks.

---

## Step A2 - Full IPv6 Notation

Example:

```
2001:0db8:0000:0000:0000:ff00:0012:3456
```

### Screenshot Evidence

![Full IPv6](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-06-Example-Full-IPv6-Address-(Documentation-Prefix-2001db8).png)

---

## Step A3 - Leading Zero Suppression

```
2001:db8:0:0:0:ff00:12:3456
```

### Screenshot Evidence

![Zero Removal](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-07-IPv6-Address-with-Leading-Zeros-Removed-(Shortened-Form).png)

---

## Step A4 - IPv6 Compression (::)

```
2001:db8::ff00:12:3456
```

### Screenshot Evidence

![Compressed](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-08-IPv6-Address-in-Fully-Compressed-()-Notation.png)

---

## Step A5 - Loopback Address

```
::1
```

### Screenshot Evidence

![Loopback](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-09-IPv6-Loopback-Address-(Expanded-and-Compressed-Form).png)

---

# IPv6 Header Structure

---

## Step H1 - Fixed 40-Byte Header

Fields include:

* Version
* Traffic Class
* Flow Label
* Payload Length
* Next Header
* Hop Limit
* Source & Destination

### Screenshot Evidence

![Header](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-10-IPv6-Base-Header-Structure-Diagram.png)

### Interpretation

Fixed size improves routing efficiency.

---

# Transition Mechanisms

---

## Step T1 - IPv4-Mapped IPv6

```
192.168.1.1 → ::ffff:c0a8:0101
```

### Screenshot Evidence

![Mapped](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-11-IPv4-Mapped-IPv6-Address-Representation-(192.168.1.1).png)

---

## Step T2 - IPv6 over IPv4 Tunneling

### Screenshot Evidence

![Tunnel](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-12-IPv6-over-IPv4-Tunneling-Between-Two-IPv6-Networks.png)

---

## Step T3 - Encapsulation Process

### Screenshot Evidence

![Encap](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-13-IPv6-over-IPv4-Tunneling-(Encapsulation-and-De-encapsulation).png)

---

# Project Conclusion

This evaluation shows:

* IPv4 is limited and exhausted
* IPv6 solves scalability issues
* Compression improves usability
* Fixed header improves efficiency
* Tunneling enables gradual transition

Understanding these is essential for modern network and SOC roles.

---

# References

These resources were used for conceptual understanding.

* IETF RFC 8200 — Internet Protocol Version 6 (IPv6)
* IPv6 Addressing Architecture (RFC 4291)
* Networking course materials and lab notes

---

# Project Credit

* **Executed and Presented By:** Mohammad Aminul Islam (SOC Analyst)
* **Learning Reference:** The Bits and Bytes of Computer Networking — Google IT Support Professional Certificate (Coursera)
* **Implementation and Documentation:** Mohammad Aminul Islam
* **Trademark Notice:** Google and the Google logo are trademarks of Google LLC.

---

