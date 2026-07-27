# TLS & HTTPS

## The Problem

HTTP is an application-layer protocol that allows a client and server to exchange information over the Internet.

It successfully transfers data, but it has one major limitation.

**HTTP sends data in plain text.**

Anyone able to inspect the network traffic may be able to read what is transmitted.

This is not a major concern for public information such as a news article. It becomes serious when usernames, passwords, banking details, session cookies or personal information are involved.

---

## Real-world Analogy

Imagine sending a postcard through the postal service.

The message reaches its destination, but everyone handling it can potentially read it.

HTTP behaves in a similar way.

HTTPS is like placing that message inside a sealed envelope that only the intended recipient can open.

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
    "��y��y�
Wi-Fi Router
     �w^~)�v
Internet Service Provider (ISP)
     �w^~)�v
Internet
    "��y��y�
Bank Server
```

With plain HTTP, anyone capable of inspecting that traffic may be able to read the credentials.

The request arrives, but it is **not confidential**.

---

## Confidentiality

Confidentiality means:

> Only the sender and the intended receiver should be able to read the transmitted data.

HTTP does not provide confidentiality. HTTPS was introduced to protect data while it travels across the network.

That raises the next question: how can readable data be protected in transit?

---

## Why HTTPS Was Invented

The Internet already had HTTP for transferring information between clients and servers.

The problem was not transferring data. The problem was protecting it while it travelled through the network.

Without HTTPS:

- Usernames and passwords can be exposed.
- Banking credentials can be exposed.
- Session cookies can be stolen.
- Personal information can be exposed.

HTTPS was introduced to provide confidentiality. Encryption is the first tool that makes this possible.

---

## Key Takeaways

- HTTP successfully transfers information but does not protect it.
- HTTP sends data in plain text.
- Plain HTTP provides no confidentiality.
- Confidentiality means that only the sender and intended receiver should read the data.
- HTTPS was introduced because HTTP lacked confidentiality.

---

## Interview Questions

### Why was HTTPS invented?

HTTP transfers information but sends it in plain text. HTTPS was introduced to protect sensitive information while it travels across the network.

---

### What is confidentiality?

Confidentiality means that only the sender and the intended receiver should be able to read transmitted data.

---

### Why is HTTP considered insecure?

Because it sends data in plain text, making sensitive information readable to anyone capable of inspecting the network traffic.

---

## My Understanding

Initially, I thought HTTPS was simply a secure version of HTTP.

Now I understand that HTTPS exists because HTTP lacks confidentiality. The next step is understanding how encryption provides that confidentiality.

---

# Encryption

Encryption transforms readable information into an unreadable form before it is sent over the network.

Only an authorized receiver should be able to convert it back to the original message.

---

## Simple Example

Suppose Alice wants to send Bob:

```
HELLO
```

They agree to reverse every message before sending it.

Alice sends:

```
OLLEH
```

Bob reverses it again and recovers:

```
HELLO
```

This demonstrates the basic idea: a message is transformed before transmission.

---

## Why Simple Transformations Are Not Enough

Reversing text is not secure. If an attacker observes enough messages, the pattern becomes obvious.

Modern cryptography therefore does not depend on keeping the algorithm secret.

The algorithm can be public and well documented. Security comes from keeping the **key** secret.

A key is the value that controls how data is encrypted and decrypted. Without the correct key, intercepted data should remain unreadable.

Encryption solves confidentiality. However, both parties must first have the correct key.

---

## Key Takeaways

- Encryption transforms readable information into an unreadable form.
- Simple transformation techniques are easy to discover and therefore insecure.
- Modern cryptography does not rely on hiding the algorithm.
- Modern cryptography relies on keeping the encryption key secret.

---

## Interview Questions

### What is encryption?

Encryption is the process of transforming readable information into an unreadable form so that only authorized parties can recover the original message.

---

### Why are simple encryption techniques insecure?

Attackers can discover patterns after observing many messages. Once the transformation rule is known, future messages can also be understood.

---

### Why can encryption algorithms be public?

Modern cryptography relies on protecting the key rather than hiding the algorithm. Without the correct key, the encrypted data should remain unreadable.

---

## My Understanding

Initially, I believed secure communication depended on hiding the encryption technique itself.

Now I understand that the algorithm can be public. Security comes from protecting the key used by that algorithm.

---

# The Key Exchange Problem

The fast form of encryption used for normal communication is **symmetric encryption**.

It requires Alice and Bob to share the same secret key.

If they already share that key, they can encrypt and decrypt messages efficiently. But how do two strangers get the same secret key in the first place?

Suppose Alice sends Bob:

```
Secret Key = banana123
```

over the Internet.

Anyone intercepting the packet receives the same secret key. From that point onward, the attacker can decrypt every message protected with it.

So sending the secret directly does not work.

> How can two computers establish a shared secret when every packet may be intercepted?

This is the **Key Exchange Problem**.

Symmetric encryption protects messages only after both parties already have a shared secret. Solving the earlier problem requires a different idea: Public-Key Cryptography.

---

## Key Takeaways

- Symmetric encryption requires both parties to share the same secret key.
- Sending that secret over an insecure network exposes it.
- Two strangers cannot simply exchange a secret key in plain text.
- This challenge is called the Key Exchange Problem.

---

## Interview Questions

### What is the Key Exchange Problem?

The Key Exchange Problem is the challenge of securely establishing a shared secret between two parties over an insecure communication channel.

---

### Why can't Alice simply send the secret key to Bob?

Anyone intercepting the network traffic would also receive the key and could decrypt future communication.

---

## My Understanding

Initially, I thought that once Alice and Bob had a secret key, secure communication would be solved.

Now I understand that the real challenge comes earlier: they must establish the same secret without revealing it to anyone else.

---

# Public-Key Cryptography

Public-Key Cryptography solves the Key Exchange Problem by giving every participant two related keys:

- A **Public Key**, which can be shared openly.
- A **Private Key**, which remains secret on its owner's computer.

Suppose Bob shares his Public Key with Alice.

Alice can use Bob's Public Key to protect information intended for Bob. Only Bob's corresponding Private Key can recover it.

An attacker can see Bob's Public Key and the encrypted message, but cannot read the message without Bob's Private Key.

This gives strangers a secure way to establish a shared secret without first sending that secret in plain text.

Public-Key Cryptography solves the trustless-start problem. However, it is not efficient enough to protect all website data.

---

## Key Takeaways

- Public-Key Cryptography uses a public key and a private key.
- The public key can be shared openly; the private key must remain secret.
- It allows strangers to establish a shared secret over an insecure network.
- It solves the Key Exchange Problem.

---

## Interview Questions

### What is the difference between a Public Key and a Private Key?

A Public Key can be shared openly. A Private Key remains secret. Data protected with a public key can be recovered only with its corresponding private key.

---

### Why is Public-Key Cryptography useful for HTTPS?

It allows a browser and server that do not already share a secret to establish one securely.

---

## My Understanding

Public-Key Cryptography solves the problem that symmetric encryption cannot solve alone: how two strangers can establish a shared secret without sending that secret directly.

---

# Why Public-Key Cryptography Is Too Slow

Public-Key Cryptography is computationally expensive.

For a small amount of information during connection setup, that cost is acceptable. Encrypting every web page, image, video stream or download with it would be unnecessarily slow.

Symmetric encryption algorithms such as AES are much faster for large amounts of data.

TLS therefore uses each approach where it is strongest:

```
Public-Key Cryptography +�u���R establish a shared secret
Symmetric Encryption    "��y��y� protect the actual HTTP data
```

The shared secret used for one secure connection has a special name: the Session Key.

---

## Key Takeaways

- Public-Key Cryptography is secure but computationally expensive.
- Symmetric encryption is much faster for large amounts of data.
- TLS uses both approaches for different parts of the connection.

---

## Interview Questions

### Why doesn't HTTPS use Public-Key Cryptography for the entire communication?

It is computationally expensive and inefficient for large amounts of data. HTTPS uses it during setup, then uses fast symmetric encryption for the actual communication.

---

## My Understanding

I initially thought HTTPS used Public-Key Cryptography for every request and response.

Now I understand that it is mainly used during connection setup, while symmetric encryption handles the bulk of the work.

---

# Session Key

A **Session Key** is the temporary shared secret used by the browser and server for one secure connection.

After TLS establishes it, both sides use the Session Key with symmetric encryption to protect HTTP requests and responses.

A fresh Session Key is created for each new connection. This limits the impact if one session is ever compromised.

At this point, the browser can establish a shared secret with whoever sent a Public Key. But it still needs to know that it is talking to the real server.

---

## Key Takeaways

- A Session Key is a temporary shared secret for one secure connection.
- It is used with fast symmetric encryption after connection setup.
- A new connection receives a new Session Key.

---

## Interview Questions

### What is a Session Key?

A Session Key is a temporary symmetric key established for one secure connection and used to encrypt its communication.

---

### Why is symmetric encryption preferred after the TLS handshake?

It is significantly faster and more efficient than Public-Key Cryptography for encrypting large amounts of data.

---

## My Understanding

The Session Key connects the two encryption approaches: Public-Key Cryptography helps establish it, and symmetric encryption uses it to protect the rest of the communication.

---

# Digital Certificate

A browser must verify that the Public Key it receives actually belongs to the intended website.

Without that verification, an attacker could replace a server's Public Key with their own and impersonate the server. This is a **Man-in-the-Middle (MITM) Attack**.

Instead of sending only a Public Key, a web server presents a **Digital Certificate**.

A certificate binds the server's identity to its Public Key. It typically contains:

- The domain name, such as `google.com`
- The server's Public Key
- Its validity period
- The Certificate Authority (CA) that issued it
- Evidence that the CA issued it

A **Certificate Authority** is a trusted organization that verifies domain control before issuing certificates. Browsers include a built-in list of trusted CAs.

The certificate tells the browser which server key it should trust. The browser still needs a way to verify that the certificate was actually issued by that Certificate Authority.

---

## Key Takeaways

- Public-Key Cryptography alone does not verify server identity.
- A Digital Certificate binds a domain name to a server Public Key.
- Certificate Authorities issue certificates after verifying domain control.
- Browsers trust certificates from their built-in list of trusted CAs.

---

## Interview Questions

### Why do we need Digital Certificates?

They allow a browser to verify that a server's Public Key belongs to the intended website, helping prevent server impersonation.

---

### What is a Certificate Authority (CA)?

A Certificate Authority is a trusted organization that verifies domain control and issues Digital Certificates.

---

### What information does a Digital Certificate contain?

It typically contains the domain name, the server's Public Key, its validity period, the issuing CA, and evidence that the CA issued it.

---

## My Understanding

Receiving a Public Key is not enough to establish a secure connection. Before using it, the browser must verify that it genuinely belongs to the intended website.

---

# Digital Signature

A **Digital Signature** lets a receiver verify two properties:

- **Authenticity**"��y��y� the information came from the claimed sender.
- **Integrity**+�u���T the information has not been modified.

It does not hide the document. Encryption provides confidentiality; a Digital Signature proves that a document is genuine and unchanged.

When a CA issues a certificate, it signs the certificate using the CA's Private Key.

The browser has trusted CA Public Keys built in. It uses the relevant CA Public Key to verify the certificate's Digital Signature.

If an attacker changes the certificate, the signature verification fails. Creating a new valid signature would require the CA's Private Key.

Once the browser verifies the certificate, it can trust the server's Public Key and continue with the TLS Handshake.

---

## Key Takeaways

- A Digital Signature provides authenticity and integrity.
- Digital Signatures do not encrypt the document.
- CAs sign certificates using their Private Keys.
- Browsers verify those signatures using trusted CA Public Keys.
- Changing a certificate causes signature verification to fail.

---

## Interview Questions

### What is a Digital Signature?

A Digital Signature is a cryptographic mechanism that verifies the authenticity and integrity of digital information.

---

### What is the difference between Encryption and a Digital Signature?

Encryption protects confidentiality by preventing unauthorized reading. A Digital Signature verifies who created information and that it has not been modified.

---

### Why can't an attacker modify a Digital Certificate?

Changing the certificate invalidates its Digital Signature. Creating a valid replacement requires the CA's Private Key.

---

### How does a browser verify a Digital Certificate?

It uses the trusted CA's Public Key to verify the certificate's Digital Signature, then checks that the certificate is valid for the requested domain and has not expired.

---

## My Understanding

A certificate alone is not enough. The browser must verify its Digital Signature to know that a trusted CA issued it and that it has not been altered.

---

# TLS Handshake

The **TLS Handshake** is the setup conversation that happens before encrypted HTTP data is sent.

At a high level, it does the following:

1. The browser connects and asks to start a secure session.
2. The server sends its Digital Certificate.
3. The browser verifies the certificate, including its Digital Signature, domain and validity period.
4. The browser and server use Public-Key Cryptography to establish a shared Session Key.
5. Both sides confirm that future communication will use that Session Key.

After the handshake, the browser knows it is communicating with the intended server and both sides share the temporary secret needed for fast symmetric encryption.

Now the normal HTTPS request can be sent safely.

---

## Key Takeaways

- The TLS Handshake happens before encrypted HTTP data is exchanged.
- It verifies the server's certificate.
- It establishes a shared Session Key.
- The Session Key is then used for fast symmetric encryption.

---

## Interview Questions

### What happens during the TLS Handshake?

The browser verifies the server's certificate and the browser and server establish a shared Session Key before encrypted HTTP communication begins.

---

## My Understanding

The TLS Handshake is the bridge between trust and communication. It verifies the server first, then creates the temporary secret used to protect the actual request and response.

---

# HTTPS Request Flow

Once the TLS Handshake is complete, HTTPS works like HTTP with an important difference: the HTTP data is encrypted using the Session Key.

```
Browser
  �w^~)�v
 "��y��y� TLS Handshake: verify certificate and establish Session Key
 +�u���|
Secure connection
  �w^~)�v
 "��y��y� Encrypted HTTP request
 "��y��y�
Server
  �w^~)�v
 "��y��y� Encrypted HTTP response
 +�u���|
Browser
```

For example, when a browser sends a login request, the username, password, headers and response are protected while travelling across the network.

HTTPS does not change the purpose of HTTP. It adds the confidentiality and server identity checks needed to use HTTP safely on the Internet.

---

## Key Takeaways

- HTTPS begins with a TLS Handshake.
- After the handshake, HTTP requests and responses are encrypted with the Session Key.
- TLS provides confidentiality and helps the browser verify the server's identity.

---

## Interview Questions

### What is the difference between HTTP and HTTPS?

HTTP transfers application data. HTTPS uses HTTP over TLS, adding encryption and server identity verification.

---

### What protects an HTTPS request after the handshake?

The browser and server use their shared Session Key with symmetric encryption to protect the request and response.

---

## My Understanding

HTTPS is not a separate replacement for HTTP. It is HTTP protected by TLS: the browser verifies the server, establishes a temporary shared key, and then exchanges encrypted requests and responses.
