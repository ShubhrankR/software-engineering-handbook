# What is HTTP?

**HTTP** stands for **HyperText Transfer Protocol**.

It is an **Application Layer** protocol that defines how clients and servers communicate.

When a browser wants a web page, HTTP defines the language it uses to ask for that page and the format the server uses to answer.

HTTP does **not** transport data across the network by itself. It relies on lower layers to do that work.

```
Application Layer
        HTTP
          ↓
Transport Layer
         TCP
          ↓
Internet Layer
          IP
```

Each layer has a different responsibility:

- **HTTP** defines the request and response conversation between the browser and server.
- **TCP** provides reliable delivery, making sure data arrives correctly and in order.
- **IP** moves packets between networks toward the correct destination.

This separation is useful because each layer can focus on one job.

When HTTP is used over TLS, it is called **HTTPS**. HTTPS is simply HTTP secured using TLS.

HTTP defines the conversation, but why does the web need a separate conversation protocol at all?

---

# Why do we need HTTP?

The earlier layers solve important problems, but they do not tell a browser how to ask for a web page.

- **DNS** finds the server's IP address.
- **TCP** provides a reliable communication channel.
- **TLS** encrypts the communication.
- **HTTP** defines what the browser and server say to each other.

A restaurant analogy helps.

DNS is like finding the restaurant's address.

TCP is like having a reliable phone line to the restaurant.

TLS is like ensuring nobody can listen to the phone call.

But none of these tells you how to place an order. HTTP is the shared language that lets you say what you want and lets the restaurant respond.

Once the browser and server share this language, they can follow a simple client-server conversation.

---

# Client–Server Model

The web commonly follows a **client-server model**.

The browser is the **client**. It asks for resources such as HTML documents, images, or data.

The server provides those resources.

The client initiates communication. The server waits for a request and sends a response.

```
Browser
    │
    │ Request
    ▼
Server
    │
    │ Response
    ▼
Browser
```

This leads to the basic pattern used by every HTTP interaction.

---

# Request–Response Model

HTTP follows a **Request–Response model**.

The client sends a request. The server processes it and sends back a response.

```
Client
   │
   │ Request
   ▼
Server
   │
   │ Response
   ▼
Client
```

At a conceptual level, the conversation looks like this:

```
Browser:
"Give me /index.html"

Server:
"Here it is."
```

HTTP defines the structure of these messages. Later sections will explore their methods, headers, and status codes.

For now, there is one more important property of this conversation: the server treats each request independently.

---

# Stateless Protocol

HTTP is **stateless**.

Each request is independent. The server does not automatically remember previous requests from the same browser.

Imagine entering a secure building. If the guard does not remember you, you need to show your ID card every time you enter.

HTTP works similarly. By itself, each request arrives without built-in memory of the earlier ones.

Login state is maintained using mechanisms built on top of HTTP, such as cookies, sessions, or authentication tokens.

This is useful to know before looking at a real browser request: the browser sends a request, and the server responds based on the information included in that request.

---

# Real Browser Example

Suppose you visit:

```
https://www.google.com/
```

Before HTTP begins, the browser has already completed the earlier steps:

- DNS finds the server.
- TCP establishes a reliable connection.
- TLS secures the connection.

The browser can then send its first HTTP request for the root HTML document:

```
GET /
```

The server responds with HTML.

The browser receives HTML first. Only after parsing that HTML can it discover references to CSS, JavaScript, images, and fonts.

It then sends additional GET requests for those resources.

```
User types URL
        │
        ▼
DNS
        ▼
TCP
        ▼
TLS
        ▼
GET /
        ▼
Receive HTML
        ▼
HTML Parser
        ▼
Discover CSS
Discover JS
Discover Images
        ▼
Additional HTTP Requests
```

Modern browsers often use HTTP/2 or HTTP/3 internally. In DevTools, you may see pseudo headers such as:

```
:method
:path
:authority
:scheme
```

These are conceptually equivalent to the HTTP/1.1 request line and the `Host` header. For now, the important idea is that the browser uses HTTP to request the HTML document first, then requests the resources it discovers.

---

# Key Takeaways

- HTTP stands for HyperText Transfer Protocol.
- HTTP is an Application Layer protocol that defines communication between clients and servers.
- HTTP relies on TCP for reliable delivery and IP for network routing.
- HTTPS is HTTP secured using TLS.
- DNS finds the server, TCP provides a reliable channel, and TLS encrypts it; HTTP defines the request and response language.
- HTTP follows a client-server, request-response model.
- HTTP is stateless; login state is built on top of it using mechanisms such as cookies, sessions, or authentication tokens.
- The browser requests HTML first, then discovers and requests other resources.

---

# Interview Questions

### What is HTTP?

HTTP is an Application Layer protocol that defines how clients and servers exchange requests and responses.

---

### Why do we need HTTP?

DNS finds the server, TCP transports data reliably, and TLS secures communication. HTTP defines the language a browser and server use to request and provide web resources.

---

### Why isn't TCP enough?

TCP provides a reliable communication channel, but it does not define what a browser should ask for or how a server should structure its response. HTTP provides that application-level meaning.

---

### What does stateless mean?

Stateless means each HTTP request is independent. A server does not automatically remember earlier requests unless state is maintained using mechanisms built on top of HTTP.

---

### What is the Request–Response model?

The client sends a request to the server, and the server sends a response back to the client.

---

### What is the first HTTP request a browser sends?

After DNS, TCP, and TLS are complete, the browser requests the root HTML document. Conceptually, this begins with:

```
GET /
```

---

# My Understanding

HTTP defines the language between a browser and a server.

TCP transports the data reliably, and TLS secures the data, but HTTP defines the request and response conversation itself.

HTTP is stateless, so each request is independent unless state is maintained on top of it.

When I visit a website, the browser first requests the HTML document. After parsing it, the browser discovers CSS, JavaScript, images, and other assets, then sends additional HTTP requests for them.
