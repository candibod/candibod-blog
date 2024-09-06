---
title: "Technical Terms"
date: 2023-01-23
layout: post
author: jeevan
image: "assets/images/banner/tech.jpg"
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

## Architecture

### Horizontal scaling

Horizontal scaling Adds more nodes or instances to an existing infrastructure, distributing the workload across multiple servers.

This can improve performance, availability, and fault tolerance, making it well-suited for distributed architectures and dynamic workloads, like web apps and content delivery networks (CDNs)

### Vertical Scaling

Increasing characteristics of computing resources, such as memory, storage, and network bandwidth

### Hybrid Scaling

Combines elements of both horizontal and vertical scaling, allowing to scale vertically when they need to improve the performance of specific components and horizontally when they require additional capacity

### Thin-client model

In thin-client model, all the application processing and data management is carried by the server. The client is simply responsible for running the presentation software.

### Thick/Fat-client model

In thick-client model, the server is only in charge for data management. The software on the client implements the application logic and the interactions with the system user.

## Tools

### Jmeter

Load testing tool which supports different protocols

## Terms

### Proxy or proxy-server or web-proxy (Forward proxy)

### Reverse Proxy

## To Review (Rewrite)

### Multi-Tier Architecture (n-tier Architecture)

Multi-tier architecture is a client–server architecture in which the functions such as presentation, application processing, and data management are physically separated. By separating an application into tiers, developers obtain the option of changing or adding a specific layer, instead of reworking the entire application. It provides a model by which developers can create flexible and reusable applications.

### Broker Architectural Style

Broker Architectural Style is a middleware architecture used in distributed computing to coordinate and enable the communication between registered servers and clients. Here, object communication takes place through a middleware system called an object request broker (software bus).

### Service-Oriented Architecture (SOA)

A service is a component of business functionality that is well-defined, self-contained, independent, published, and available to be used via a standard programming interface. The connections between services are conducted by common and universal message-oriented protocols such as the SOAP Web service protocol, which can deliver requests and responses between services loosely.

Service-oriented architecture is a client/server design which support business-driven IT approach in which an application consists of software services and software service consumers (also known as clients or service requesters).
