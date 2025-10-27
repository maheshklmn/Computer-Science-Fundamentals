# Transport Layer (Layer 4 of the OSI Model)

## Overview
The **Transport Layer** is the **fourth layer** of the **OSI (Open Systems Interconnection)** model.  
It is responsible for **end-to-end communication**, **error recovery**, **flow control**, and **ensuring complete data transfer** between applications.

### Key Purpose
Provides **reliable or unreliable data delivery services** to the **application layer**.

---

## Protocols

### TCP (Transmission Control Protocol)

#### Characteristics
- **Connection-oriented**: Requires connection establishment before data transfer  
- **Reliable**: Guarantees delivery with no loss or duplication  
- **Ordered**: Data arrives in the same order it was sent  
- **Flow Control**: Prevents overwhelming the receiver  
- **Congestion Control**: Adjusts the sending rate based on network conditions  

#### TCP Header Fields
- Source Port  
- Destination Port  
- Sequence Number  
- Acknowledgment Number  
- Window Size  
- Flags (SYN, ACK, FIN, RST)  

#### TCP 3-Way Handshake
1. **SYN** – Client sends a synchronization request  
2. **SYN-ACK** – Server acknowledges and synchronizes  
3. **ACK** – Client acknowledges, connection established  

#### Use Cases
- Web Browsing (HTTP/HTTPS)  
- Email (SMTP/IMAP)  
- File Transfer (FTP)

---

### UDP (User Datagram Protocol)

#### Characteristics
- **Connectionless**: No connection setup required  
- **Unreliable**: No delivery guarantees  
- **No Ordering**: Packets may arrive out of sequence  
- **No Flow Control**: Can overwhelm the receiver  
- **Faster**: Lower overhead compared to TCP  

#### UDP Header Fields
- Source Port  
- Destination Port  
- Length  
- Checksum  

#### Use Cases
- DNS (Domain Name System)  
- VoIP (Voice over IP)  
- Video Streaming  
- Online Gaming  

---

## Network Congestion

**Congestion** occurs when network resources are overloaded by too much data, resulting in **packet loss**, **delays**, and **poor performance**.

---

## TCP Congestion Control Algorithms

| Algorithm | Purpose | Mechanism | Phase |
|------------|----------|------------|--------|
| **Slow Start** | Gradually finds available bandwidth | cwnd doubles every RTT | Exponential growth until threshold |
| **Congestion Avoidance** | Conservatively increases throughput | cwnd increases by 1 MSS per RTT | Additive growth |
| **Fast Retransmit** | Detects lost packets faster | Retransmits after 3 duplicate ACKs | Avoids timeout delay |
| **Fast Recovery** | Resumes sending after loss | Reduces cwnd by half | Continues in avoidance phase |

**AIMD (Additive Increase Multiplicative Decrease)**  
- Increase: `cwnd += 1 MSS per RTT` (Additive)  
- Decrease: `cwnd = cwnd / 2` on packet loss (Multiplicative)

---

## Java Implementation Examples

### TCP Server
```java
import java.net.*;
import java.io.*;

public class TCPServer {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(8080)) {
            System.out.println("TCP Server started on port 8080");
            
            while (true) {
                Socket clientSocket = serverSocket.accept();
                System.out.println("Client connected: " + clientSocket.getInetAddress());
                
                new Thread(() -> handleClient(clientSocket)).start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
    private static void handleClient(Socket clientSocket) {
        try (BufferedReader in = new BufferedReader(
                new InputStreamReader(clientSocket.getInputStream()));
             PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true)) {
            
            String message;
            while ((message = in.readLine()) != null) {
                System.out.println("Received: " + message);
                out.println("Echo: " + message);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}



//TCP Client

import java.net.*;
import java.io.*;

public class TCPClient {
    public static void main(String[] args) {
        try (Socket socket = new Socket("localhost", 8080);
             PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
             BufferedReader in = new BufferedReader(
                 new InputStreamReader(socket.getInputStream()));
             BufferedReader stdIn = new BufferedReader(
                 new InputStreamReader(System.in))) {
            
            String userInput;
            while ((userInput = stdIn.readLine()) != null) {
                out.println(userInput);
                System.out.println("Server response: " + in.readLine());
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}


//UDP Server

import java.net.*;

public class UDPServer {
    public static void main(String[] args) {
        try (DatagramSocket socket = new DatagramSocket(8080)) {
            System.out.println("UDP Server started on port 8080");
            byte[] buffer = new byte[1024];
            
            while (true) {
                DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
                socket.receive(packet);
                
                String message = new String(packet.getData(), 0, packet.getLength());
                System.out.println("Received: " + message);
                
                InetAddress clientAddress = packet.getAddress();
                int clientPort = packet.getPort();
                byte[] response = ("Echo: " + message).getBytes();
                DatagramPacket responsePacket = new DatagramPacket(
                    response, response.length, clientAddress, clientPort);
                socket.send(responsePacket);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}


//UDP Client

import java.net.*;
import java.util.Scanner;

public class UDPClient {
    public static void main(String[] args) {
        try (DatagramSocket socket = new DatagramSocket();
             Scanner scanner = new Scanner(System.in)) {
            
            InetAddress serverAddress = InetAddress.getByName("localhost");
            byte[] buffer = new byte[1024];
            
            System.out.println("Enter messages to send (type 'exit' to quit):");
            while (true) {
                String message = scanner.nextLine();
                if ("exit".equalsIgnoreCase(message)) break;
                
                byte[] sendData = message.getBytes();
                DatagramPacket sendPacket = new DatagramPacket(
                    sendData, sendData.length, serverAddress, 8080);
                socket.send(sendPacket);
                
                DatagramPacket receivePacket = new DatagramPacket(buffer, buffer.length);
                socket.receive(receivePacket);
                String response = new String(receivePacket.getData(), 0, receivePacket.getLength());
                System.out.println("Server response: " + response);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}


