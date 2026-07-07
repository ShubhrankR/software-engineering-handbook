# Study Log

## 2026-06-29

### Topic
How the Web Works (Part 1)

### Learned
- A browser doesn't immediately send an HTTP request.
- DNS resolution happens before the HTTP request.
- The browser usually receives HTML first, then discovers additional resources like CSS, JavaScript, images, and fonts.
- HTML is only one stage of the browser rendering pipeline.

### Realization
I thought I had forgotten web fundamentals.

After today's discussion, I realized I remember many concepts individually, but I need a better mental model connecting them together.

### Next Topic
DNS Resolution

## 2026-06-30
No study today.

## 2026-07-01
Forgot to fill.

## 2026-07-02
No study today.

### Reason:
Work and personal commitments.

### Reflection:
Missing one day is acceptable.
The goal is consistency over months, not perfection.

### Next Action:
Continue from where I left off on 3rd July.

## 2026-07-03
Forgot to fill.

## 2026-07-04
No study today.

### Reason
Getting overwhelmed with too many goals, decided to play PS5 instead (Ghost of Tusuhima).

### Reflection
Setting too many goals at once leads to burnout. It is better to start with one or two goals and gradually add more as you get comfortable. Also, never miss twice.

## 2026-07-05

### Topic
TCP & IP (Part 2)

### Learned
- TCP and IP are separate protocols with different responsibilities.
- IP is responsible for delivering packets from one computer to another.
- TCP is responsible for reliable communication.
- Data is divided into packets because sending one huge file is inefficient and unreliable.
- TCP uses acknowledgements (ACKs) and retransmissions to ensure reliable delivery.
- Packet ordering is maintained by TCP, not IP.
- TCP can detect duplicate packets and discard them.
- Separation of Concerns is one of the fundamental ideas behind the design of TCP/IP.

### Realization
Today I realized that networking protocols are designed using the same software engineering principles that I already know, such as Separation of Concerns and Single Responsibility.

I'm not learning isolated networking concepts. I'm learning how engineers design reliable systems.

### Interview Questions I Can Answer
- Why can't we send one huge file over the Internet?
- What is the difference between TCP and IP?
- Why are TCP and IP separate protocols?
- What happens when a packet is lost?
- What is an ACK?

### Questions for Tomorrow
- Why does TCP use a three-way handshake?
- What are sequence numbers?
- What is a TCP segment?
- How does TCP reorder packets?

## 2026-07-06

### Topic
TCP Three-Way Handshake

### Learned
- TCP establishes a reliable connection before transferring data.
- A Three-Way Handshake consists of SYN, SYN-ACK and ACK.
- One message is insufficient because the sender does not know whether the receiver got the request.
- Two messages are insufficient because the receiver does not know whether the sender received its response.
- Three messages are the minimum required for both computers to confirm they can send and receive data.
- A fourth message adds unnecessary latency and network overhead.

### Realization
The biggest lesson today was understanding that the Three-Way Handshake is not about transferring data—it is about building confidence that communication works in both directions.

I also realized that good protocol design follows the same engineering principles that we use while writing software: solve the problem with the minimum complexity required.

### Interview Questions I Can Answer
- Why does TCP use a Three-Way Handshake?
- Why isn't one message enough?
- Why isn't two messages enough?
- Why are four messages unnecessary?
- What problem does the Three-Way Handshake solve?

### Questions for Tomorrow
- What is the difference between TCP and UDP?
- What is a Port Number?
- How do multiple applications use the network simultaneously?

### Confidence (Out of 10)

Topic Understanding: **8/10**

I can confidently explain the intuition behind the Three-Way Handshake using a real-world analogy, but I still need to understand sequence numbers and how the handshake is implemented internally.

## 2026-07-07

### Topic

Port Numbers & TCP vs UDP

### Learned

- An IP Address identifies a computer on the network.
- A Port Number identifies the application running on that computer.
- The operating system uses the destination port number to deliver packets to the correct application.
- TCP prioritizes reliability by using acknowledgements, retransmissions and packet ordering.
- UDP prioritizes speed and low latency by avoiding acknowledgements and retransmissions.
- The choice between TCP and UDP depends on the application's requirements.

### Realization

Today I realized that networking protocols are not designed to be universally "better" than one another.

Instead, they represent different engineering trade-offs.

The biggest takeaway for me was understanding that engineers choose protocols based on the properties they want in a system, such as reliability, latency and performance.

### Interview Questions I Can Answer

- What is a Port Number?
- Why do we need Port Numbers?
- What is the difference between TCP and UDP?
- When should TCP be used?
- When should UDP be used?
- Why is UDP preferred for online games and live streaming?

### Questions for Tomorrow

- What is a Socket?
- How does the operating system deliver packets to an application?
- What happens inside `fetch()` before an HTTP request is sent?

### Confidence (Out of 10)

**9/10**

I now have a strong understanding of TCP/IP fundamentals. I can explain the intuition behind packets, acknowledgements, retransmissions, the Three-Way Handshake, Port Numbers and TCP vs UDP using real-world analogies. I still want to understand sockets and how the operating system internally manages network communication.

