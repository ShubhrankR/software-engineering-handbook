# DNS Resolution

## What problem does DNS solve?

DNS solves the problem that humans remember names, but computers communicate using numbers.

For example, humans can easily remember a name like `google.com`, but remembering the IP address of Google is difficult. Computers, on the other hand, need an IP address to identify where the request should go.

DNS acts like a phonebook for the internet. It converts a domain name into the IP address that computers can use.

## What is DNS?

DNS stands for Domain Name System.

It is a distributed and hierarchical system that maps domain names to IP addresses. Instead of depending on one server for the whole world, DNS uses many servers that work together to resolve domain names.

## What is DNS Resolution?

DNS Resolution is the process of converting a domain name into an IP address.

When a user enters a domain like `google.com` in the browser, DNS resolution happens in the background. The user does not need to know the IP address manually; DNS finds it and allows the browser to continue the request.

## Why do we need DNS?

We need DNS because domain names are easier for humans to remember, while IP addresses are required by computers to communicate over the network.

Without DNS, users would need to remember IP addresses for every website. This would be difficult, especially because websites can change their IP addresses over time.

DNS makes internet usage practical by allowing users to access websites through readable names instead of numeric addresses.

## What happens if DNS doesn't exist?

If DNS does not exist, users would have to remember the IP address of every website they want to visit.

This would create two major problems:

- Remembering IP addresses would be difficult for humans.
- If a website changes its IP address, users would need to update the saved address manually.

DNS avoids this problem by providing a system where domain names can stay the same even if the underlying IP address changes.

## DNS Caching

DNS caching means storing a DNS response for some time so the same domain does not need to be resolved again and again.

For example, if the browser already knows the IP address for `google.com`, it can reuse that cached result instead of immediately asking a DNS resolver again.

### Why is DNS caching important?

DNS caching improves performance and reduces repeated work.

If every request required a fresh DNS lookup, it would waste computing power and add extra delay. Caching allows commonly visited domains to resolve faster because the answer may already be available nearby.

### Multi-level DNS Cache

DNS responses may be cached at multiple levels:

- Browser
- Operating System
- Router
- ISP Resolver

This is why the browser does not always need to contact a DNS server directly every time a user enters a known domain name.

## Real-world Analogy

DNS is like a phonebook.

If you know a person's name but not their phone number, you look up the name in a phonebook and get the number. Similarly, when you know a domain name like `google.com`, DNS helps find the IP address needed to connect to that website.

## Connections

DNS demonstrates several important software engineering concepts:

- Distributed Systems: DNS is not handled by a single server for the entire world.
- Hierarchical Design: DNS uses a tree-like structure to organize domain names.
- Caching: DNS responses can be stored and reused at multiple levels.
- Performance Optimization: Caching reduces repeated lookups and makes requests faster.

## Key Takeaways

- DNS converts human-readable domain names into IP addresses.
- DNS Resolution is the process of finding the IP address for a domain name.
- DNS is distributed, so it does not depend on one global server.
- DNS is hierarchical, which helps organize domain names at scale.
- DNS caching improves performance by avoiding repeated lookups.
- DNS can be cached at the browser, OS, router, and ISP resolver levels.

## My Understanding

Multi-level caching supports DNS resolution. It is not like every time a user enters `google.com`, Chrome must send a fresh request to a DNS server and resolve it again. Doing that repeatedly would waste computing power and add unnecessary delay.

That is why DNS uses caching at multiple levels, such as the browser, operating system, router, ISP resolver, and other places.

A DNS server is also not a single server for the whole world. DNS is distributed because one server cannot handle resolution for everyone globally. Multiple DNS servers work together to support the entire system.

## Interview Questions

### What problem does DNS solve?

DNS solves the problem of mapping human-readable domain names to IP addresses that computers can use.

### What is DNS Resolution?

DNS Resolution is the process of converting a domain name, such as `google.com`, into its corresponding IP address.

### Why is DNS caching important?

DNS caching is important because it avoids repeated DNS lookups, reduces latency, and saves computing resources.

### What happens if DNS fails?

If DNS fails, the browser may not be able to find the IP address for a domain name, so the website may not load even if the server is running.
