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

## Common Questions and Concepts

### Why can't we send one huge file?
Sending a huge file as a single massive block of data is highly inefficient and error-prone. If even a tiny bit of interference or network issue corrupts a small part of that massive block, the entire file would need to be retransmitted. It would also hog network bandwidth, preventing other users or applications from communicating simultaneously. Breaking data into small pieces (packets/segments) allows for multiplexing (sharing the connection), faster recovery from errors, and efficient routing.

### What are packets?
Packets (or datagrams/segments depending on the layer) are the small chunks of data that a larger file or message is broken down into for transmission over a network. Each packet contains a portion of the actual data (the payload) as well as a header. The header contains essential metadata, such as the source IP address, destination IP address, sequence numbers, and error-checking information, ensuring the packet can independently find its way to the destination and be reassembled correctly.

### What is an ACK?
An ACK, short for **Acknowledgment**, is a specific type of control packet or a flag within a TCP packet. When the receiving device successfully receives a packet or a sequence of packets, it sends an ACK back to the sender. This tells the sender, "I got the data up to this point." It's the core mechanism TCP uses to guarantee reliable delivery.

### What happens if a packet is lost?
TCP handles lost packets gracefully. If a sender transmits a packet but does not receive an ACK from the receiver within a specific timeframe (a timeout), the sender assumes the packet was lost or corrupted in transit. The sender will then automatically retransmit the unacknowledged packet. This ensures that no data is permanently lost, even over unreliable networks.

### The Truck Analogy
A great way to visualize this is using a "Truck" analogy.
Imagine you want to send an entire house (a huge file) across the country. 
*   You can't put the whole house on one truck (why we don't send one huge file).
*   Instead, you dismantle the house into many small boxes (**packets**).
*   Each box is loaded onto its own small delivery truck. Each truck has an address label telling it where to go (the **IP header**).
*   The trucks might take different highways or routes depending on traffic (**IP routing**).
*   When a truck arrives at the destination, the receiver checks off a list and sends a postcard back to you saying "Box #4 arrived safely" (**ACK**).
*   If one truck gets a flat tire and never arrives, you notice you never got a postcard for Box #12. So, you pack a duplicate Box #12 and send it on a new truck (**retransmission of lost packets**).
*   Finally, the receiver uses the sequence numbers on the boxes to rebuild the house exactly as it was.

## Key Takeaways

- DNS finds the server.
- IP delivers packets.
- TCP makes communication reliable.
- Data is divided into packets.
- ACKs confirm successful delivery.
- Lost packets are retransmitted.
- TCP and IP have different responsibilities.

## Connections

This chapter relates to several software engineering concepts:

- Separation of Concerns
- Single Responsibility Principle (SOLID)
- Layered Architecture
- Reliability vs Performance trade-offs

## Questions for Future Me

- Why does TCP use a three-way handshake?
- What are sequence numbers?
- How does TCP detect duplicate packets?
- What is a sliding window?
- How does congestion control work?

## TCP Three-Way Handshake

Before transferring data, TCP establishes a reliable connection between two computers.

The connection is established using three messages:

1. **SYN** – The client asks to establish a connection.
2. **SYN-ACK** – The server acknowledges the request and agrees to establish the connection.
3. **ACK** – The client confirms that it received the server's response.

After these three messages, both computers know that they can send and receive data reliably.

### Why not one message?

With only one message, the sender has no idea whether the receiver actually received it.

### Why not two messages?

After two messages, the client knows the server received its request, but the server still doesn't know whether the client received its reply.

### Why not four messages?

A fourth message doesn't provide any additional information. It only increases latency and network overhead.

### Real-world Analogy

Making a phone call:

Person A: "Hello?"

Person B: "Hello, I can hear you."

Person A: "Great, I can hear you too."

Now both people know the connection works in both directions.

## My Understanding

The biggest takeaway for me was that TCP's three-way handshake is not about sending data.

It is about both computers gaining confidence that communication works in both directions.

Using only one or two messages leaves uncertainty for one side.

Three messages are the minimum required for both computers to confirm that they can send and receive data reliably.

A fourth message would not provide any additional information and would only increase network overhead.