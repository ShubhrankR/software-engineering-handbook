# TCP/IP Fundamentals

Transmission Control Protocol (TCP) and Internet Protocol (IP) are the foundational protocols of the Internet, forming the TCP/IP suite. Together, they ensure that data is transmitted reliably and reaches the correct destination.

## Internet Protocol (IP)

*   **Role**: Routing and Addressing.
*   **Function**: IP is responsible for addressing hosts and routing packets (datagrams) from a source host to a destination host across one or more IP networks.
*   **Analogy**: Think of IP as the postal service; it uses addresses (IP addresses) to figure out where to send the mail, but it doesn't guarantee the mail won't get lost or arrive in the wrong order.

## Transmission Control Protocol (TCP)

*   **Role**: Reliable Data Delivery.
*   **Function**: TCP operates on top of IP. It takes the data from an application, breaks it into smaller chunks (segments), numbers them, and sends them over IP. TCP ensures that all segments arrive correctly and in order at the destination.
*   **Key Features**:
    *   **Connection-Oriented**: Establishes a connection (three-way handshake) before sending data.
    *   **Reliability**: Uses acknowledgments (ACKs) and retransmissions to ensure no data is lost.
    *   **Order**: Sequence numbers guarantee that data is reassembled in the correct order.
    *   **Flow Control**: Prevents a fast sender from overwhelming a slow receiver.

## TCP Communication: A Visual Overview

Here is an ASCII diagram demonstrating a simplified TCP communication flow between two laptops, including the famous "Three-Way Handshake" and data transfer.

```text
    Laptop A (Client)                                          Laptop B (Server)
    IP: 192.168.1.10                                           IP: 192.168.1.20
    [  ======  ]                                                [  ======  ]
    [          ]                                                [          ]
    [__________]                                                [__________]
         ||                                                          ||
 
 ========================== 1. TCP Three-Way Handshake ==========================
 
      (SYN) Let's connect!
      Sequence=100
      --------------------------------------------------------------------->
                                                       (SYN-ACK) I hear you, let's connect!
                                                       Ack=101, Sequence=300
      <---------------------------------------------------------------------
      (ACK) Got it, connection established!
      Ack=301, Sequence=101
      --------------------------------------------------------------------->
 
                           [Connection Established]
 
 =============================== 2. Data Transfer ===============================
 
      (DATA) Sending file block 1
      Sequence=101, Length=500
      --------------------------------------------------------------------->
                                                       (ACK) Received block 1
                                                       Ack=601 (101+500)
      <---------------------------------------------------------------------
 
      (DATA) Sending file block 2
      Sequence=601, Length=500
      --------------------------------------------------------------------->
                                                       (ACK) Received block 2
                                                       Ack=1101 (601+500)
      <---------------------------------------------------------------------
 
 ============================== 3. Connection Teardown ==========================
 
      (FIN) I'm done sending.
      Sequence=1101
      --------------------------------------------------------------------->
                                                       (ACK) Acknowledged.
                                                       Ack=1102
      <---------------------------------------------------------------------
                                                       (FIN) I'm done too.
                                                       Sequence=5000
      <---------------------------------------------------------------------
      (ACK) Acknowledged, goodbye.
      Ack=5001
      --------------------------------------------------------------------->
 
                           [Connection Closed]
```
