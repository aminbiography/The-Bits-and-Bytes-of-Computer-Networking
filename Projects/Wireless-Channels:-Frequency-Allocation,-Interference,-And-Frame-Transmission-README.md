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

