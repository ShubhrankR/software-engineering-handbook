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

## 2026-07-08

### Topic

Sockets (Part 1)

### Learned

- Applications do not communicate directly with the network.
- Applications communicate with the operating system through sockets.
- A socket acts as the communication endpoint between an application and the networking stack.
- TCP and IP are responsible for networking, while sockets provide the programming interface used by applications.

### Realization

Today was different from previous sessions.

Instead of fully understanding a topic in one sitting, I realized it is acceptable to leave a chapter partially complete and revisit it after gaining more context.

I also understood that learning networking is becoming easier because each new concept connects with the previous one.

### Interview Questions I Can Partially Answer

- What is a Socket?
- Why do sockets exist?
- How does an application communicate with the operating system?

### Questions for Tomorrow

- What uniquely identifies a TCP connection?
- How does the operating system manage multiple sockets?
- What does a socket look like in actual code?
- How does `fetch()` eventually use a socket?

### Confidence (Out of 10)

**6.5/10**

I understand the purpose of sockets, but I don't yet have the complete mental model. I want to strengthen this topic using practical examples before marking the TCP/IP chapter as complete.

## 2026-07-10

No study today.

### Reason

Spent the evening planning my flatmate's birthday celebration and packing for my upcoming weekend trip to Chennai.

### Reflection

Personal commitments and planning for upcoming events took priority today.

Missing one study session is acceptable, but I should return to the handbook as soon as the commitments are over instead of letting the break become longer than necessary.

### Next Action

Continue with the TLS & HTTPS chapter.

# Weekly Reflection

## Wins

- Completed the DNS chapter.
- Completed the TCP/IP chapter.
- Built a consistent repository structure.
- Maintained meaningful Git commits.

## Challenges

- Felt overwhelmed by multiple life goals.
- Lost momentum after travelling.
- Sometimes preferred gaming over studying.

## Improvements for Next Week

- Study immediately after dinner instead of deciding later.
- Keep one session focused on one concept only.
- Continue committing after every study session.

---

## 2026-07-11

No study today.

### Reason

Travelled from Bengaluru to Chennai to attend a friend's engagement ceremony.

### Reflection

This was a planned personal commitment, not procrastination.

Maintaining relationships is also important. Planned breaks should not create guilt.

### Next Action

Resume the handbook after returning to Bengaluru.

---

## 2026-07-12

No study today.

### Reason

Returned to Bengaluru after attending the engagement ceremony and spent the day travelling back.

### Reflection

Travelling is tiring, and it is okay to rest before returning to the learning routine.

The important part is returning, not maintaining a perfect streak.

### Next Action

Resume with the TLS & HTTPS chapter.

---

## 2026-07-13

No study today.

### Reason

Returned to the normal work routine after the weekend trip and felt mentally exhausted.

### Reflection

Returning after a break is much harder than maintaining momentum.

I don't need to catch up on missed days.

I only need to continue from the next chapter.

### Next Action

Resume the TLS & HTTPS chapter.

---

## 2026-07-14

No study today.

### Reason

Did not study today. I don't remember the exact reason, but I was unable to continue after the weekend break.

### Reflection

This reminded me how easy it is to lose momentum after taking a few days off.

The challenge wasn't understanding the material—it was restarting.

Going forward, I want to focus less on maintaining a perfect streak and more on returning quickly after a break.

### Next Action

Resume with the TLS & HTTPS chapter.

---

## 2026-07-15

No study today.

### Reason

Attended an office dinner hosted by VISA. A Senior Director visited our office and took the team out for dinner.

### Reflection

Not every missed study session is a result of procrastination.

Work commitments and team events are part of a professional career. The important thing is to resume the learning journey instead of feeling guilty about a planned or unavoidable event.

### Next Action

Continue the TLS & HTTPS chapter from where I left off.

---

## 2026-07-16

### Topic

Why HTTPS Was Invented

### Learned

- HTTP successfully transfers data but sends it in plain text.
- Plain HTTP does not provide confidentiality.
- Sensitive information such as usernames and passwords can potentially be read while travelling across the network.
- HTTPS was introduced to solve this problem by encrypting communication.
- Confidentiality means that only the sender and the intended receiver should be able to read the transmitted data.

### Realization

Earlier, I thought HTTPS was simply a secure version of HTTP.

Today I understood the real reason HTTPS exists.

HTTP already solved the problem of transferring data between a client and a server, but it did not protect that data while it travelled across the network.

HTTPS was introduced to provide confidentiality by encrypting communication.

### Interview Questions I Can Answer

- Why was HTTPS invented?
- Why is HTTP considered insecure?
- What is Confidentiality?
- What problem does HTTPS solve?

### Confidence (Out of 10)

**7/10**

I understand why HTTPS exists and the security problem it solves. Next, I want to learn how TLS uses encryption, public/private keys and certificates to provide secure communication.

---

## 2026-07-17

No study today.

### Reason

Did not study today.

### Reflection

After returning to the learning routine on 16th July, I couldn't maintain the momentum the very next day.

This reminded me that building a consistent habit is more challenging than completing a single productive session.

The goal is to keep returning instead of expecting perfection.

### Next Action

Resume the TLS & HTTPS chapter.

---

## 2026-07-18

No study today.

### Reason

Did not study today.

### Reflection

I missed another study session today.

Instead of feeling guilty about the missed days, I want to focus on getting back to learning tomorrow.

Consistency is built by repeatedly returning after interruptions, not by maintaining an unbroken streak.

### Next Action

Continue learning the TLS & HTTPS chapter.

---

## 2026-07-19

### Topic

Encryption Fundamentals

### Learned

- Encryption transforms readable information into an unreadable form before transmission.
- Simple transformation techniques (such as reversing a message) help explain the concept but are not secure.
- If attackers observe enough encrypted messages, they may discover patterns.
- Modern cryptography does not rely on keeping the encryption algorithm secret.
- The encryption algorithm can be public, while the encryption key must remain secret.

### Realization

Today I understood one of the most important principles of modern cryptography.

Security does not come from hiding the encryption algorithm.

Instead, it comes from protecting the secret key used by the algorithm.

This changed my understanding of how secure communication works over the Internet.

### Interview Questions I Can Answer

- What is encryption?
- Why is simple encryption insecure?
- Why can modern encryption algorithms be public?
- Why is the encryption key kept secret?

### Confidence (Out of 10)

7/10

I now understand why encryption exists and why modern cryptography relies on secret keys.

I still need to learn how Alice and Bob securely exchange those keys over an insecure network.

### Next Action

Learn how two computers securely exchange encryption keys over the Internet.
