## **Project Title** 
### **Wireless Channels: Frequency Allocation, Interference and Frame Transmission**

---

## **Project Objective**

The objective of this project is to explain how **wireless frequency allocation**, **channel overlap**, and **frame transmission mechanisms** work together to affect Wi-Fi performance. The project also demonstrates how **encapsulation/de-encapsulation** and **802.11 MAC frame structure** support reliable wireless communication in shared radio environments.

---
 
## **Project Scenario**

A small office network experiences degraded Wi-Fi performance due to congestion and interference from nearby wireless networks operating in the same 2.4 GHz frequency band. Multiple access points and devices compete for airtime, resulting in collisions and retransmissions. This project studies wireless channel behavior, frame transmission, and encapsulation concepts to understand and mitigate these issues.

---

## **Project Description & Setup**

---

### **1. Non-Overlapping Channels in the 2.4 GHz Wi-Fi Band**

![Non-Overlapping Channels (1, 6, 11)](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-05-01-166-2.4-Non-Overlapping-Channels-in-the-2.4-GHz-Wi-Fi-Band-\(1%2C%206%2C%2011\).png)

The 2.4 GHz Wi-Fi band is divided into multiple channels, but most of them overlap.
Only **channels 1, 6, and 11** are fully non-overlapping.

**Key points:**

* Overlapping channels increase interference and collisions
* Collisions force devices to stop transmitting and retry
* Using channels **1, 6, and 11** minimizes interference in dense environments

---

### **2. 802.11 Wireless MAC Frame Structure**

![802.11 Wireless MAC Frame Structure](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-05-02-802.11-Wireless-MAC-Frame-Header-and-Payload-Structure.png)

Wireless communication relies on structured frames defined by IEEE 802.11.

**Important frame fields:**

* **Frame Control** – defines frame type and processing rules
* **Duration/ID** – controls how long the medium is reserved
* **Address Fields (1–4)** – identify sender, receiver, access point, and destination
* **Sequence Control** – maintains correct frame ordering
* **Data Payload** – carries upper-layer data
* **Frame Check Sequence (FCS)** – detects transmission errors

The presence of **four MAC addresses** allows frames to be properly forwarded in wireless infrastructure networks.

---

### **3. 2.4 GHz Wi-Fi Channel Frequencies**

![2.4 GHz Wi-Fi Channel Frequencies](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-05-03a-2.4-GHz-Wi-Fi-Channel-Frequencies.png)

Each Wi-Fi channel has a center frequency, but the signal spreads across a wider bandwidth.

**Why this matters:**

* Channel bandwidth causes overlap with adjacent channels
* Regional regulations determine available channels
* Improper channel selection leads to congestion and poor performance

---

### **4. Encapsulation and De-encapsulation**

![Encapsulation and De-encapsulation](https://github.com/aminbiography/The-Bits-and-Bytes-of-Computer-Networking/blob/main/Graph-Bar-Chart-Images/M-05-03b-Encapsulation-De-encapsulation.png)

Encapsulation is the process of wrapping data with protocol headers before transmission.

**Process overview:**

* Application data is encapsulated inside a data-link frame
* Headers and trailers provide addressing, sequencing, and error detection
* At the destination, de-encapsulation removes these fields to recover the original data

This process ensures reliable communication across wireless and wired networks.

---

## **Interference and Performance Analysis**

| Issue                        | Cause                  | Resolution                         |
| ---------------------------- | ---------------------- | ---------------------------------- |
| Slow Wi-Fi during peak hours | Channel overlap        | Use channels 1, 6, 11              |
| High retransmissions         | Large collision domain | Reduce overlap                     |
| Strong signal, poor speed    | Interference           | Switch to non-overlapping channels |
| Unstable connections         | Congested spectrum     | Prefer 5 GHz where possible        |

---
  
## **Project Conclusion**

Wireless networking performance depends heavily on effective **channel allocation**, **interference management**, and **frame handling**. In the 2.4 GHz band, selecting non-overlapping channels (1, 6, 11) is critical to minimizing collisions. Understanding 802.11 frame structure and encapsulation explains how reliable data transmission is achieved over a shared wireless medium. Proper planning and configuration significantly improve Wi-Fi stability and throughput.

---

## Project Credit

* **Executed and Presented By:** Mohammad Aminul Islam *(SOC Analyst)*
* **Project Reference:** *The Bits and Bytes of Computer Networking* — Google IT Support Professional Certificate Program *(Coursera)*
* **Project Implementation and Documentation:** Mohammad Aminul Islam
* **Copyright and Trademarks:** © 2022 Google LLC. Google and the Google logo are trademarks of Google LLC. All other product and company names may be trademarks of their respective owners.

---


