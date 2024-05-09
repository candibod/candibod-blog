---
title: "Technical Terms"
date: 2023-01-23
layout: post
author: jeevan
---

Technical Terms

## Internet Layers

physical
data link
network
transport
session
presentation
application

## Protocol

## API - Application Programming Interface

Set of protocols that systems use to communicate with each other to share data. Usually when a client requests for any resource, servers give the relevant response

![Book logo](/assets/images/api-overview.jpg)

### Different Types of API

- REST(Representational State Transfer) - HTTP
  - Stateless - no client context is stored on the server
  - Cache - clients can cache responses
- SOAP(Simple Object Access Protocol) - supports multiple protocols(TCP, HTTP, SMTP, e.t.c.,)
  - XML Based
  - Secure - Financial services & payment gateway
  - Complex & verbose
- gRPC(Google Remote Procedural Call) - HTTP/2
  - Micro Service Architecture
  - Limited browser support
  - Build by google based on RPC(TCP)
- GraphQL - HTTP
  - query language
- WebSocket - TCP
  - Realtime, low-latency
  - Bi-directional
  - Persistent connections
- WebHook - HTTP
  - Async Request
- WEBRTC(Web Real-Time Communications)
  - capture/stream audio and/or video media

Explicit type conversion in programming is done manually by the programmer, while implicit conversion is handled automatically by the compiler
