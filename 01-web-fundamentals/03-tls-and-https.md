# TLS & HTTPS

## The Problem

HTTP is an application layer protocol that allows a client and a server to exchange information over the Internet.

Although HTTP successfully transfers data, it has one major limitation.

**HTTP sends data in plain text.**

Anyone who is able to inspect the network traffic may be able to read the transmitted information.

This is not a major concern for public information such as news articles or blog posts.

However, it becomes a serious security problem when sensitive information such as usernames, passwords, banking details, session cookies or personal information is transmitted.

---

## Real-world Analogy

Imagine sending a postcard through the postal service.

Everyone involved in delivering the postcard can potentially read its contents.

HTTP behaves in a similar way.

The message reaches its destination, but it is not protected from being read while travelling.

HTTPS is like placing the same message inside a sealed envelope that only the intended recipient can open.

---

## Example

Suppose I visit:

```
http://my-bank.com
```

I enter:

```
Username : shubhrank
Password : MyPassword123
```

The request travels through several devices before reaching the bank.

```
My Laptop
     │
Wi-Fi Router
     │
Internet Service Provider (ISP)
     │
Internet
     │
Bank Server
```

Since HTTP does not encrypt the transmitted data, anyone capable of inspecting the traffic may be able to read the transmitted information.

The communication successfully reaches the bank, but it is **not confidential**.

---

## Confidentiality

Confidentiality is one of the fundamental goals of information security.

It means:

> Only the sender and the intended receiver should be able to read the transmitted data.

HTTP does **not** provide confidentiality.

HTTPS was introduced to provide confidentiality while data travels across the network.

---

## Why HTTPS Was Invented

The Internet already had HTTP for transferring information between clients and servers.

The problem was not transferring data.

The problem was protecting the data while it travelled through the network.

Without HTTPS:

- Usernames can be exposed.
- Passwords can be exposed.
- Banking credentials can be exposed.
- Session cookies can be stolen.
- Personal information can be exposed.

HTTPS was introduced to solve this problem.

---

## Key Takeaways

- HTTP successfully transfers information but does not protect it.
- HTTP sends data in plain text.
- Plain HTTP provides no confidentiality.
- Confidentiality means that only the sender and the intended receiver should be able to read the transmitted data.
- HTTPS was introduced because HTTP lacked confidentiality.

---

## Interview Questions

### Why was HTTPS invented?

HTTP successfully transfers information but sends it in plain text.

HTTPS was introduced to protect sensitive information while it travels across the network.

---

### What is Confidentiality?

Confidentiality means that only the sender and the intended receiver should be able to read the transmitted data.

---

### Why is HTTP considered insecure?

Because it sends data in plain text, making sensitive information readable by anyone capable of inspecting the network traffic.

---

## My Understanding

Initially, I thought HTTPS was simply a secure version of HTTP.

Now I understand that HTTPS exists because HTTP lacks confidentiality.

The first step towards understanding TLS is not encryption.

It is understanding the problem that encryption was designed to solve.