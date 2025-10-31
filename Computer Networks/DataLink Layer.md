# 🧩 Data Link Layer – Overview and Java Implementation

## 🌐 What is the Data Link Layer?

The **Data Link Layer** is **Layer 2** in the OSI model responsible for **node-to-node data transfer** between directly connected devices on the same network.  
It handles **framing**, **physical addressing**, **error detection**, and **flow control**.

### 🔑 Key Purpose
> Provides **reliable data transfer** across the physical network medium.

---

## ⚡ What is Ethernet?

**Ethernet** is the most common LAN technology that operates at the Data Link Layer.  
It defines **wiring**, **signaling**, and **frame structure** for local area networks.

### 🧱 Ethernet Frame Structure


| **Field** | **Description** |
|------------|----------------|
| **Preamble** | Synchronization and start frame delimiter |
| **MAC Addresses** | Source and destination hardware addresses |
| **Type/Length** | Identifies upper-layer protocol or frame length |
| **Data** | Payload (46–1500 bytes) |
| **FCS** | Frame Check Sequence for error detection |

---

## 🧾 MAC Address (Media Access Control)

A **48-bit hardware address**, for example:  
`00:1A:2B:3C:4D:5E`

| **Bits** | **Purpose** |
|-----------|-------------|
| First 24 bits | Manufacturer ID (OUI) |
| Last 24 bits | Device-specific identifier |

Each network interface has a **unique worldwide MAC address**.

---

## 🔄 CSMA/CD (Carrier Sense Multiple Access with Collision Detection)

**Used in:** Traditional (half-duplex) Ethernet

### Process:
1. **Carrier Sense** – Check if medium is free  
2. **Multiple Access** – Multiple devices can transmit  
3. **Collision Detection** – Detect and handle collisions  

> 🧠 Modern Ethernet uses **full-duplex** with switches, eliminating collisions.

---

## ⚙️ Error Control Policies

**Purpose:** Detect and correct errors in data transmission.

### 1️⃣ Parity Check
- Simple error detection
- Adds an extra bit to make total 1s **even** or **odd**
- ⚠️ Detects only **single-bit errors**

### 2️⃣ Checksum
- **Sender:** Calculates sum of data bits and sends complement  
- **Receiver:** Recalculates sum and checks against received checksum  
- **Used in:** TCP, UDP, IP headers

### 3️⃣ CRC (Cyclic Redundancy Check)
- Most reliable error detection
- Uses **polynomial division** to generate check bits  
- **Used in:** Ethernet frames (FCS field)  
- Can detect **burst errors up to 32 bits**

---

## 🚦 Flow Control Policies

**Purpose:** Prevent a fast sender from overwhelming a slow receiver.

### 1️⃣ Stop-and-Wait ARQ
- Simple flow control  
- Process: Send one frame → Wait for ACK → Send next frame  
- ✅ Simple to implement  
- ❌ Poor utilization (half-duplex)

### 2️⃣ Sliding Window Protocol
- Efficient and reliable flow control  
- **Window Size:** Number of frames that can be sent without ACK

#### Types:
- **Go-Back-N:** Resend all frames from lost frame onward  
- **Selective Repeat:** Resend only the lost frames

#### Example:

---

## 💻 Java Example – Network Interface

```java
import java.net.*;
import java.util.Enumeration;

public class DataLinkLayerDemo {
    public static void main(String[] args) {
        try {
            Enumeration<NetworkInterface> interfaces = NetworkInterface.getNetworkInterfaces();
            
            while (interfaces.hasMoreElements()) {
                NetworkInterface ni = interfaces.nextElement();
                System.out.println("Interface: " + ni.getDisplayName());
                System.out.println("Name: " + ni.getName());
                
                byte[] mac = ni.getHardwareAddress();
                if (mac != null) {
                    System.out.print("MAC Address: ");
                    for (int i = 0; i < mac.length; i++) {
                        System.out.format("%02X%s", mac[i], (i < mac.length - 1) ? ":" : "");
                    }
                    System.out.println();
                }
                
                System.out.println("MTU: " + ni.getMTU());
                System.out.println("Is Up: " + ni.isUp());
                System.out.println("Is Loopback: " + ni.isLoopback());
                System.out.println("----------");
            }
        } catch (SocketException e) {
            e.printStackTrace();
        }
    }
}


public class ErrorDetection {
    
    // Simple Checksum implementation
    public static short calculateChecksum(byte[] data) {
        int sum = 0;
        for (byte b : data) {
            sum += (b & 0xFF);  // Convert to unsigned
        }
        // Wrap around carry and take complement
        while (sum >>> 16 != 0) {
            sum = (sum & 0xFFFF) + (sum >>> 16);
        }
        return (short) ~sum;
    }
    
    // Verify checksum
    public static boolean verifyChecksum(byte[] data, short checksum) {
        int sum = 0;
        for (byte b : data) {
            sum += (b & 0xFF);
        }
        sum += (checksum & 0xFFFF);  // Add the checksum
        
        while (sum >>> 16 != 0) {
            sum = (sum & 0xFFFF) + (sum >>> 16);
        }
        return sum == 0xFFFF;
    }
    
    public static void main(String[] args) {
        String message = "Hello Data Link Layer!";
        byte[] data = message.getBytes();
        
        short checksum = calculateChecksum(data);
        System.out.println("Checksum: " + Integer.toHexString(checksum & 0xFFFF));
        
        boolean isValid = verifyChecksum(data, checksum);
        System.out.println("Data integrity: " + isValid);
        
        // Simulate data corruption
        data[0] = (byte) (data[0] + 1);  // Corrupt first byte
        boolean isStillValid = verifyChecksum(data, checksum);
        System.out.println("After corruption: " + isStillValid);
    }
}


✅ Summary
Concept	Purpose
Data Link Layer	Node-to-node communication
Ethernet	Defines LAN frame and transmission rules
MAC Address	Unique hardware identifier
CSMA/CD	Manages access and collision detection
Error Detection	Ensures data integrity (Parity, Checksum, CRC)
Flow Control	Balances sender and receiver speeds
