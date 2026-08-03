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


---

# Why is the Host Header Required?

Suppose multiple websites share the same server and IP address.

For example:

- `google.com`
- `youtube.com`
- `gmail.com`

All three websites can be hosted on the same machine.

After DNS Resolution and the TCP/TLS connection are complete, the server only knows that a client has connected to its IP address.

Without additional information, a request such as:

```
GET /
```

is ambiguous because every website has its own root page.

The browser therefore includes the website name in the request:

```
GET /
Host: www.google.com
```

In HTTP/2 and HTTP/3, the equivalent information is sent using the `:authority` pseudo header.

```
Client
  |
  | GET /
  | Host: google.com
  v
Web Server
  |
  | Routes request to Google website
  v
Google website
```

Modern web servers use **Virtual Hosting** to host multiple websites on the same IP address.

The `Host` header, or `:authority` in HTTP/2 and HTTP/3, lets the server distinguish between those websites and route the request to the correct one.

---

# Key Takeaway

The IP address identifies the server.

The Host header identifies the website hosted on that server.

---

# Interview Question

### Why is the Host header required if the browser already knows the website URL?

Because multiple websites can share the same IP address. The Host header tells the web server which website should process the request.

---

# My Understanding

Initially I thought the Host header was redundant because the browser already knew the URL.

Now I understand that the Host header is intended for the web server, allowing it to determine which website should handle the request when multiple websites share the same server.


---

# What is a Web Server?

A **server** is simply a computer that provides services to other computers.

A **Web Server** is software that understands HTTP and HTTPS requests.

Common Web Servers include:

- Nginx
- Apache HTTP Server
- Caddy
- IIS

A Web Server is responsible for:

- Listening for HTTP requests.
- Reading the Request Line and Headers.
- Determining which website should handle the request by using the `Host` header or `:authority`.
- Serving static files such as HTML, CSS, JavaScript, and images.
- Forwarding dynamic requests to backend applications when required.

A restaurant analogy helps explain the role.

```
Customer
   |
   v
Waiter (Web Server)
   |
   v
Chef (Backend Application)
   |
   v
Waiter
   |
   v
Customer
```

The waiter does not cook the food.

The waiter receives the order, understands it, and forwards it to the kitchen when necessary.

A Web Server works in the same way. It receives the HTTP request, understands where it should go, and either serves a file itself or forwards the request to a backend application.

---

## Frontend Example

Suppose an Angular application has been built into:

```
dist/
    index.html
    main.js
    styles.css
```

Nginx can directly serve these files to the browser.

Node.js is not required just to serve this built frontend. The Web Server can read the requested static file from the `dist/` folder and return it as an HTTP response.

A backend application is needed only when the request requires dynamic work, such as fetching user data, processing a payment, or writing to a database.

---

## Why the Host Header Exists

One physical server can host multiple websites:

- `google.com`
- `youtube.com`
- `gmail.com`

The Web Server reads the `Host` header, or `:authority` in HTTP/2 and HTTP/3, to determine which website should process the request.

This is how one server and one IP address can serve several different websites.

---

## Key Takeaway

The IP address identifies the server.

The Host header identifies the website hosted on that server.

---

# HTTP Message Structure

An HTTP request is not just a line such as `GET /`.

The browser and server need an agreed structure so the server can understand what the browser wants.

---

## Why does an HTTP request need a structure?

Imagine placing an order at a restaurant.

If a customer only says, "I want food," the waiter cannot reliably prepare the correct order.

A useful order needs a shared format:

- What is being ordered?
- Which item is requested?
- Are there any instructions?
- Is there extra information for the kitchen?

Communication between a browser and server works the same way.

It becomes reliable when both sides agree on a common format. HTTP defines that format.

---

## Parts of an HTTP Request

An HTTP request has three main parts:

```
HTTP Request
|
|-- Request Line
|-- Headers
\-- Body (Optional)
```

- The **Request Line** tells the server what the client wants to do and which resource it wants.
- **Headers** provide metadata and instructions about the request.
- The **Body** contains application data when the request needs to send it.

The server reads these parts together to understand the request.

---

## Request Line

The Request Line tells the server:

- What action should be performed.
- Which resource is requested.
- Which HTTP version is being used.

For example:

```
GET /products HTTP/1.1
```

It can be broken into three pieces:

```
Method        Path        HTTP Version
GET           /products   HTTP/1.1
```

### Method

The **Method** describes the action the client wants to perform.

In this example, `GET` means the client wants to retrieve a resource.

### Path

The **Path** identifies the resource being requested from the server.

In this example:

```
/products
```

means the client is asking for the products resource.

### HTTP Version

The **HTTP Version** tells the server which version of the HTTP protocol the client is using.

In HTTP/2 and HTTP/3, Chrome DevTools displays pseudo headers instead of the traditional Request Line:

```
:method
:path
:authority
:scheme
```

These are conceptually equivalent to the traditional Request Line plus the `Host` header. The structure looks different in DevTools, but the browser is still communicating the same core information.

After the server understands the basic request, it may need more instructions. That information is sent in headers.

---

## Headers

Headers contain **metadata** about the request.

The Request Line is the order.

Headers are the instructions attached to the order.

For example, headers can tell the server:

- `Host` �w^~)�t which website on the server should handle the request.
- `Accept`+�u���T which response formats the client can understand.
- `Accept-Encoding`+�u���T which compression formats the client supports.
- `Accept-Language`+�u���T which languages the client prefers.
- `User-Agent`"��y��y� information about the browser or client making the request.
- `Cookie`+�u���T stored information that the browser sends back to the server.

Cookies are part of the request headers, but their details will be covered later.

Some requests also need to send the application's actual data. That is the job of the request body.

---

## Request Body

The request body contains the actual application data sent by the client.

For example, a login request may look like:

```
POST /login

{
    "email": "abc@gmail.com",
    "password": "********"
}
```

Here, the body contains the email and password submitted by the user.

GET requests usually do not contain a body because they are commonly used to retrieve an existing resource.

POST requests commonly contain a body because they are often used to send data to the server, such as login details, form data, or JSON payloads.

The distinction is important: headers describe the request, while the body carries the application's data.

---

## Headers vs Body

| Headers | Body |
| --- | --- |
| Metadata | Actual application data |
| Describes the request | Contains data sent by the application |
| Cookies | Form data |
| `Content-Type` | JSON payload |
| `Accept` | Uploaded files |
| `Authorization` | Login credentials |

Login credentials belong in the body because they are the application's data.

An authentication token usually belongs in the `Authorization` header because it describes the identity under which the request is being made.

This difference helps the server understand both what data was sent and who is allowed to make the request.

---

## Chrome DevTools Mapping

Today's learning was verified using Chrome DevTools.

In an HTTP/2 or HTTP/3 request, DevTools shows:

```
:method
:path
:authority
:scheme
```

Together, these represent the information that the traditional HTTP/1.1 Request Line and `Host` header communicate.

Everything below them, such as:

```
Accept
Cookie
User-Agent
Accept-Encoding
```

is a request header.

The inspected Google request had no request body because it was a GET request asking for the homepage.

Now that the structure of a request is clear, later sections can explore HTTP methods, headers, status codes, and responses in more detail.

---

# Key Takeaways

- An HTTP request uses an agreed structure so the client and server can communicate reliably.
- The three parts of an HTTP request are the Request Line, Headers, and an optional Body.
- The Request Line contains the method, path, and HTTP version.
- Headers contain metadata and instructions about the request.
- The Body contains actual application data.
- GET requests usually do not have a body, while POST requests commonly do.
- In HTTP/2 and HTTP/3, pseudo headers represent the core request-line information.

---

# Interview Questions

### What are the three parts of an HTTP request?

The three parts are the Request Line, Headers, and an optional Body.

---

### What is the Request Line?

The Request Line tells the server what action to perform, which resource is requested, and which HTTP version is being used.

---

### What is the difference between headers and the body?

Headers contain metadata that describes the request. The body contains the actual application data being sent to the server.

---

### Why do GET requests usually not have a body?

GET requests are commonly used to retrieve existing resources, so they usually do not need to send application data to the server.

---

### Why are login credentials placed in the body?

Login credentials are application data submitted by the user, so they belong in the request body.

---

### Why is the Authorization token usually sent in a header?

The token describes the identity and permissions under which the request is made, so it is usually sent in the `Authorization` header.

---

# My Understanding

Initially I viewed an HTTP request as just a GET or POST request.

Today I understood that every HTTP request follows a well-defined structure consisting of a Request Line, Headers, and an optional Body.

I also understood the distinction between metadata in headers and application data in the body, and why authentication tokens and login credentials belong in different parts of the request.
