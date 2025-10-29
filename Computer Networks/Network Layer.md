# 🌐 Network Layer (Layer 3 of the OSI Model)

## 🧩 What is the Network Layer?

The **Network Layer** is **Layer 3** in the **OSI model** responsible for **logical addressing**, **routing**, and **packet forwarding** between different networks.

**Key Purpose:** Enables **end-to-end delivery** of packets across multiple networks.

---

## ⚙️ IPv4 (Internet Protocol Version 4)

- **Address Size:** 32-bit (≈ 4.3 billion addresses)  
- **Format:** Dotted-decimal notation (e.g., `192.168.1.1`)

### **Address Classes**
| Class | Range | Usage |
|--------|--------|--------|
| **A** | 1.0.0.0 – 126.255.255.255 | Large networks |
| **B** | 128.0.0.0 – 191.255.255.255 | Medium networks |
| **C** | 192.0.0.0 – 223.255.255.255 | Small networks |
| **D** | 224.0.0.0 – 239.255.255.255 | Multicast |
| **E** | 240.0.0.0 – 255.255.255.255 | Experimental |

---

## 🌍 IPv6 (Internet Protocol Version 6)

- **Address Size:** 128-bit (≈ 340 undecillion addresses)  
- **Format:** Hexadecimal notation (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`)

### **Benefits**
- Larger address space  
- Built-in security (**IPsec**)  
- Better header format  
- Auto-configuration  
- Improved multicast  

---

## 🚦 What is Routing?

**Routing** is the process of **selecting paths** in a network to send data from source to destination.

---

## 🧭 Routing Protocols

### **1. Distance Vector Protocols**
- **How it works:** Routers share entire routing tables with neighbors  
- **Algorithm:** Bellman-Ford  
- **Examples:** RIP, IGRP  
- **Advantage:** Simple to implement  
- **Disadvantage:** Slow convergence, count-to-infinity problem  

### **2. Link State Protocols**
- **How it works:** Routers share info about directly connected links  
- **Algorithm:** Dijkstra (Shortest Path First)  
- **Examples:** OSPF, IS-IS  
- **Advantage:** Fast convergence, loop prevention  
- **Disadvantage:** Higher CPU and memory usage  

### **3. Path Vector Protocols**
- **How it works:** Shares complete path information  
- **Example:** BGP (Border Gateway Protocol)  
- **Use Case:** Internet backbone routing  

---

## 🖧 Key Network Layer Devices

### **Router**
- **Operates at:** Layer 3  
- **Function:** Connects different networks, makes routing decisions  
- **Uses:** IP addresses for forwarding  

### **Layer 3 Switch**
- **Combines:** Switching (Layer 2) + Routing (Layer 3)  
- **Use Case:** Faster inter-VLAN routing  

---

## 💻 Java Implementation

### **Getting IP Address Information**

```java
import java.net.*;

public class NetworkLayerDemo {
    public static void main(String[] args) {
        try {
            // Get local host information
            InetAddress localHost = InetAddress.getLocalHost();
            System.out.println("Local Host: " + localHost.getHostName());
            System.out.println("IP Address: " + localHost.getHostAddress());
            
            // Check IPv4 vs IPv6
            byte[] address = localHost.getAddress();
            if (address.length == 4) {
                System.out.println("IPv4 Address");
            } else if (address.length == 16) {
                System.out.println("IPv6 Address");
            }
            
            // Get all IP addresses for a host
            InetAddress[] googleIPs = InetAddress.getAllByName("www.google.com");
            for (InetAddress ip : googleIPs) {
                System.out.println("Google IP: " + ip.getHostAddress());
            }
            
        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
    }
}
