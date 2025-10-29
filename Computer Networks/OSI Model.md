# 🧱 OSI Model Overview

The **OSI (Open Systems Interconnection)** Model is a **conceptual framework** that standardizes the functions of a telecommunication or computing system into **seven abstraction layers**.  
Each layer **serves the layer above it** and is **served by the layer below it**.

---

## **Layer 7 - Application Layer**
**Function:** User interface and network services  
**Protocols:** HTTP, HTTPS, FTP, SMTP, DNS  
**Examples:** Web browsers, email clients  

---

## **Layer 6 - Presentation Layer**
**Function:** Data formatting, encryption, compression  
**Responsibilities:**  
- Data translation  
- Encryption / Decryption  
- Compression / Decompression  

---

## **Layer 5 - Session Layer**
**Function:** Session management and control  
**Responsibilities:**  
- Session establishment  
- Session maintenance  
- Session termination  

---

## **Layer 4 - Transport Layer**
**Function:** End-to-end communication and error recovery  
**Protocols:** TCP, UDP  
**Responsibilities:**  
- Segmentation  
- Error detection and correction  
- Flow control  

---

## **Layer 3 - Network Layer**
**Function:** Routing and logical addressing  
**Protocols:** IP, ICMP, ARP  
**Responsibilities:**  
- Path determination  
- Logical addressing  
- Packet forwarding  

---

## **Layer 2 - Data Link Layer**
**Function:** Physical addressing and error detection  
**Protocols:** Ethernet, PPP  
**Responsibilities:**  
- Frame formatting  
- Physical addressing (MAC)  
- Error detection  

---

## **Layer 1 - Physical Layer**
**Function:** Physical transmission of raw bits  
**Components:** Cables, fiber optics, wireless signals  
**Responsibilities:**  
- Bit transmission  
- Physical topology  
- Signal encoding  

---

## **📧 Real-World Example: Sending an Email**

| **Layer** | **Process** |
|------------|-------------|
| **Application** | You compose email in Gmail (HTTP) |
| **Presentation** | Email encrypted with SSL |
| **Session** | Login session established |
| **Transport** | TCP ensures reliable delivery |
| **Network** | IP routes packet to destination |
| **Data Link** | Ethernet frames sent to router |
| **Physical** | Electrical signals through cable |

---
