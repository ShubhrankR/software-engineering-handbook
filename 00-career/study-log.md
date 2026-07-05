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
