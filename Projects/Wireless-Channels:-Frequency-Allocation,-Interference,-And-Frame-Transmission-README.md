## **Project Title** 
**Wireless Channels: Frequency Allocation, Interference and Frame Transmission**

---

## **Project Objective**

The objective of this project is to explain how **wireless frequency allocation**, **channel overlap**, and **frame transmission mechanisms** work together to affect Wi-Fi performance. The project also demonstrates how **encapsulation/de-encapsulation** and **802.11 MAC frame structure** support reliable wireless communication in shared radio environments.

---

## **Project Scenario**

You are working as an IT Support Specialist responsible for a small office WLAN operating in the **2.4 GHz band**.
Users report **slow speeds and intermittent connectivity**, especially during peak hours. To resolve this issue, you must analyze:

* Wi-Fi channel allocation and overlap
* Interference caused by shared collision domains
* Wireless frame transmission and addressing
* The encapsulation and de-encapsulation process

---

## **Project Description and Setup**

### **1. Wireless Frequency Allocation (2.4 GHz Band)**

![Image](https://extr-p-001.sitecorecontenthub.cloud/api/public/content/b97b5cdd7b28428cacf1946bdc3430aa?v=a61c0f2f)

![Image](https://www.researchgate.net/publication/328064410/figure/fig1/AS%3A677899539607552%401538635253259/Frequency-channel-distribution-for-the-24-GHz-band.ppm)

* The **2.4 GHz Wi-Fi band** spans approximately **2.400 GHz to 2.500 GHz**
* Channels are spaced **5 MHz apart**, but each channel occupies **~22 MHz**
* This causes **significant overlap** between adjacent channels
* Channel availability varies by country and regulatory domain

**Impact:**
Overlapping channels increase interference and reduce overall throughput.

---

### **2. Channel Overlap and Interference**

![Image](https://wifimetrix.com/nansupport.com/images/wifimetrix/overlapping-channels-1124x316b.png)

![Image](https://extr-p-001.sitecorecontenthub.cloud/api/public/content/b97b5cdd7b28428cacf1946bdc3430aa?v=a61c0f2f)

* Most 2.4 GHz channels overlap with one another
* **Channels 1, 6, and 11** are the only **non-overlapping channels**
* Using overlapping channels creates larger **collision domains**
* Collisions force devices to retransmit, increasing latency

**Recommended WLAN Setup:**

* Access Point 1 → Channel 1
* Access Point 2 → Channel 6
* Access Point 3 → Channel 11

This minimizes interference and improves stability.

---

### **3. Frame Transmission in Wireless Networks (802.11 MAC Frame)**

![Image](https://fr.mathworks.com/help/examples/wlan/win64/xxMACFrameFormat.png)

![Image](https://scaler.com/topics/images/mac-frame-structure.webp)

Wireless networks use **IEEE 802.11 MAC frames**, which are more complex than wired Ethernet frames due to the shared wireless medium.

Key components include:

* **Frame Control (16 bits):** Defines frame type and processing rules
* **Duration / ID:** Reserves the wireless medium
* **Four MAC Address Fields**:

  * Source address
  * Intended destination
  * Receiving address (Access Point)
  * Transmitter address
* **Sequence Control:** Maintains correct frame ordering
* **Data Payload:** Upper-layer data
* **Frame Check Sequence (FCS):** Error detection using CRC

**Why four addresses?**
Wireless frames may be relayed through access points, requiring separate identification of sender, receiver, and destination.

---

### **4. Encapsulation and De-encapsulation**

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2ASKGPlucmtWhASlZw7gpIeg.png)

![Image](https://static.afteracademy.com/images/what-is-data-encapsulation-in-networking-process-148532037a490a19.jpg)

* **Encapsulation:** Higher-layer data is wrapped with protocol headers and trailers before transmission
* **De-encapsulation:** The receiving device removes these headers to retrieve the original data
* This process ensures:

  * Correct protocol identification
  * Error detection
  * Data integrity

Encapsulation is fundamental to both wired and wireless communications, including WAN technologies such as PPP.

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

Wireless networking performance is strongly influenced by **frequency allocation**, **channel overlap**, and **frame transmission design**. Because Wi-Fi operates in a shared medium, improper channel selection leads to collisions and degraded performance. Understanding non-overlapping channels, 802.11 frame structure, and encapsulation processes enables IT professionals to design, troubleshoot, and optimize reliable wireless networks.

---

## **Project Credit**

**Executed and Documented By:** Mohammad Aminul Islam


---













































## **Project Title** 
### **Wireless Channels: Frequency Allocation, Interference, and Frame Transmission**

---

## **Project Objective**

To analyze how wireless channels are allocated in the 2.4 GHz Wi-Fi band, how channel overlap causes interference and collisions, and how wireless frame structure and encapsulation enable reliable data transmission over shared radio frequencies.

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

## **Project Conclusion**

Wireless networking performance depends heavily on effective **channel allocation**, **interference management**, and **frame handling**. In the 2.4 GHz band, selecting non-overlapping channels (1, 6, 11) is critical to minimizing collisions. Understanding 802.11 frame structure and encapsulation explains how reliable data transmission is achieved over a shared wireless medium. Proper planning and configuration significantly improve Wi-Fi stability and throughput.

---

## **Project Credit**

**Executed and Presented By:**
**Mohammad Aminul Islam**
SOC Analyst



