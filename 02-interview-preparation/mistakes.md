# Interview Mistakes Log

This document records incorrect mental models discovered during interview preparation.

It is not a knowledge base.

It is a list of mistakes I have personally made so I don't repeat them.

---

# JavaScript

## Execution Context

❌ I thought JavaScript starts executing code during the Memory Creation Phase.

✓ The Memory Creation Phase only allocates memory.

Execution happens afterwards.

---

## let

❌ I thought let creates another execution context.

✓ let does not create another execution context.

It is block scoped and remains uninitialized until execution reaches its declaration.

---

## Hoisting

❌ I thought hoisting moves variables to the top.

✓ Nothing is physically moved.

JavaScript scans declarations during the Memory Creation Phase before execution begins.

---

# Browser

(Leave placeholder)

---

# HTTP

## Host Header

❌ I initially thought the Host header was redundant because the browser already knows the URL.

✓ The Host header is for the Web Server.

It tells the server which website should process the request when multiple websites share the same IP address.

---

## HTTP Request

❌ I thought an HTTP request was simply GET or POST.

✓ Every HTTP request consists of:

- Request Line
- Headers
- Optional Body

---

# Angular

(Leave placeholder)

---

# HTML

(Leave placeholder)

---

# CSS

(Leave placeholder)

---

# System Design

(Leave placeholder)

---

# Behavioral

(Leave placeholder)
