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

---

# Encryption

Sending data in plain text over the Internet is insecure because anyone capable of inspecting the network traffic may be able to read the transmitted information.

One way to solve this problem is to transform the original message into another form before sending it across the network.

This process is called **encryption**.

Instead of sending readable information (plain text), the sender converts it into an unreadable form before transmission.

Only the intended receiver should be able to convert it back to its original form.

---

## Simple Example

Suppose Alice wants to send the following message to Bob.

```
HELLO
```

Instead of sending it directly, Alice and Bob agree on a simple rule.

Reverse every message before sending it.

Alice sends:

```
OLLEH
```

Bob knows the agreed rule, so he reverses the message again and recovers:

```
HELLO
```

Someone intercepting the message can still see:

```
OLLEH
```

but without knowing the agreed rule, they cannot immediately understand its meaning.

---

## Why Simple Transformations Are Not Enough

The previous example demonstrates the basic idea of encryption, but it is not secure.

If an attacker observes enough encrypted messages, patterns begin to appear.

Eventually, the attacker may discover that every message is simply written backwards.

Once the rule becomes known, every future message can also be understood.

This shows that simple transformation techniques are not sufficient for secure communication over the Internet.

---

## Modern Cryptography

Modern cryptography follows an important principle.

The encryption algorithm itself does **not** need to be secret.

In fact, modern encryption algorithms are public and well documented.

The security comes from keeping the **key** secret.

Even if everyone knows how the encryption algorithm works, only the people possessing the correct key can encrypt and decrypt the transmitted data.

Without the key, intercepted data should remain unreadable.

---

## Key Takeaways

- Encryption transforms readable information into an unreadable form.
- Simple transformation techniques are easy to discover and therefore insecure.
- Modern cryptography does not rely on hiding the algorithm.
- Modern cryptography relies on keeping the encryption key secret.
- The algorithm may be public, but the key must remain secret.

---

## Interview Questions

### What is encryption?

Encryption is the process of transforming readable information into an unreadable form so that only authorized parties can recover the original message.

---

### Why are simple encryption techniques insecure?

Because attackers can discover patterns after observing many encrypted messages.

Once the transformation rule becomes known, future messages can also be understood.

---

### Why can encryption algorithms be public?

Modern cryptography relies on keeping the encryption key secret rather than hiding the algorithm itself.

The algorithm may be public, but without the correct key the encrypted data should remain unreadable.

---

## My Understanding

Initially, I believed secure communication depended on hiding the encryption technique itself.

Now I understand that modern cryptography follows a different principle.

Everyone can know the encryption algorithm.

The security comes from protecting the secret key used by that algorithm.

---

# The Key Distribution Problem

Encryption allows Alice and Bob to communicate securely by using a secret key.

However, this introduces a new problem.

Both Alice and Bob need to possess the same secret key before they can exchange encrypted messages.

The obvious solution is for Alice to simply send the key to Bob.

```
Alice ---- Secret Key ----> Bob
```

Unfortunately, if an attacker is able to inspect all network traffic, the attacker also receives the same secret key.

```
Alice
   │
Internet
   │
Eve 👀
   │
Bob
```

Once the attacker knows the secret key, every future encrypted message can also be decrypted.

The communication is no longer secure.

---

## Why Is This Difficult?

At first, it seems like Alice and Bob could each keep part of the secret key and exchange the missing pieces.

However, if those pieces are also transmitted over the same insecure network, an attacker can intercept them as well.

This raises an important question.

> How can two computers establish a shared secret key over a network where every packet can be intercepted?

This problem is known as the **Key Distribution Problem**.

For many years, this was considered one of the biggest challenges in secure communication.

The solution to this problem eventually led to one of the greatest breakthroughs in modern cryptography.

---

## Key Takeaways

- Symmetric encryption requires both parties to share the same secret key.
- Sending the secret key over an insecure network exposes it to attackers.
- Protecting the message is not enough; the secret key must also be protected.
- Securely exchanging a secret key is known as the **Key Distribution Problem**.

---

## Interview Questions

### Why can't Alice simply send the secret key to Bob?

Because anyone capable of intercepting the network traffic would also receive the secret key, making future encrypted communication insecure.

---

### What is the Key Distribution Problem?

The Key Distribution Problem is the challenge of securely establishing a shared secret key between two parties over an insecure communication channel.

---

## My Understanding

Initially, I thought that once Alice and Bob had a secret key, secure communication would be solved.

Today I realized that the real challenge is much earlier.

Before encryption can even begin, both parties somehow need to obtain the same secret key without allowing anyone else to learn it.

Understanding this problem helps explain why more advanced cryptographic techniques were eventually developed.
