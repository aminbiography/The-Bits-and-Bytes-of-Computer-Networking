# **Project Title**

## **Cross-Platform CLI-Based Network Analysis and Troubleshooting**

---

# **Project Objective**

To demonstrate systematic network analysis and troubleshooting using command-line tools across Windows and Linux environments for:

* Connectivity testing
* Routing path analysis
* Port reachability validation
* DNS resolution verification

This project simulates real-world workflows used by network and SOC analysts to diagnose connectivity and service-related issues.

---

# **Project Scenario**

A user experiences intermittent connectivity and service-access issues.
A network/SOC analyst performs structured analysis to verify:

1. Internet connectivity
2. Routing paths
3. Service port availability
4. DNS resolution

Command-line tools are used to isolate issues methodically.

---

# **Project Description**

---

# **Windows PowerShell / Command Prompt Analysis**

---

## **Step W1 — Connectivity Test (Ping)**

### Command

```powershell
ping 8.8.8.8
```

### Output

```powershell
Reply from 8.8.8.8: bytes=32 time=3–5ms TTL=56  
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

### Interpretation

Confirms external network reachability and latency.

---

---

# **Linux CLI / VS Code Bash Analysis**

---

## **Step L1 — Connectivity Test**

### Command

```bash
ping 8.8.8.8
```

### Output

```bash
19 packets transmitted, 19 received, 0% packet loss  
rtt avg ≈ 4 ms
```

### Interpretation

Indicates stable connectivity and low latency.

### Screenshot Evidence

![Ping Test](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-01-Successful-Ping-Test-to-8.8.8.8-(Linux-Terminal).png)

---

## **Step L2 — Routing Path Analysis**

### Command

```bash
traceroute google.com
```

### Interpretation

Shows hop-by-hop routing path to the destination.

### Screenshot Evidence

![Traceroute](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-02-Traceroute-Command-Output-Showing-Network-Hops-to-google.com.png)

---

## **Step L3 — Port Reachability**

### Command

```bash
nc -z -v google.com 80
```

### Output

```bash
Connection to google.com 80 port succeeded!
```

### Interpretation

Confirms TCP port 80 is reachable.

### Screenshot Evidence

![Netcat Port Test](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-03-netcat-successful-port-80-connection.png)

---

## **Step L4 — DNS Resolution**

### Command

```bash
nslookup twitter.com
```

### Interpretation

Verifies domain-to-IP resolution.

---

## **Step L5 — MX Record Lookup**

### Command

```bash
nslookup  
set type=MX  
google.com
```

### Interpretation

Displays mail exchanger records.

### Screenshot Evidence

![MX Lookup](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-06-04-Nslookup-MX-Record-Results-for-google.com-in-Interactive-Mode.png)

---

## **Step L6 — Interface Information**

### Command

```bash
ip a
```

### Purpose

Displays IP addressing and interface states.

---

## **Step L7 — Active Connections**

### Command

```bash
ss -tuln
```

### Purpose

Shows listening and active sockets.

---

## **Step L8 — Routing Table**

### Command

```bash
ip route
```

### Purpose

Displays routing paths and gateways.

---

# **Project Conclusion**

The analysis confirms:

* Reliable internet connectivity
* Functional routing paths
* Accessible service ports
* Proper DNS resolution
* Valid mail routing configuration

This project demonstrates practical, cross-platform CLI-based network analysis and troubleshooting applicable to real-world SOC and network operations.

---

# **References**

*These resources were used for conceptual understanding and lab preparation.*

### Command Line Troubleshooting Tools Reference Guide

[https://drive.google.com/file/d/1jbGWD9ilDyBpv7S2Gb15Nw08Uswf6hox/view?usp=sharing](https://drive.google.com/file/d/1jbGWD9ilDyBpv7S2Gb15Nw08Uswf6hox/view?usp=sharing)

### Testing Port Connectivity

[https://drive.google.com/file/d/1w4GgfP5VsXzMOjTOaWwONBS89vrSTNwt/view?usp=drive_link](https://drive.google.com/file/d/1w4GgfP5VsXzMOjTOaWwONBS89vrSTNwt/view?usp=drive_link)

---

# **Project Credit**

* **Executed and Presented By:** Mohammad Aminul Islam (SOC Analyst)
* **Project Reference Source:** *The Bits and Bytes of Computer Networking — Google IT Support Professional Certificate (Coursera)*
* **Implementation and Documentation:** Mohammad Aminul Islam
* **Trademark Notice:** © 2022 Google LLC. Google and the Google logo are trademarks of Google LLC. All other product and company names may be trademarks of their respective owners.

---
