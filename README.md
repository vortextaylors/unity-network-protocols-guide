# Unity Network Protocols Guide

## Introduction
This repository provides guidance and simple code reference for connecting Unity client to backend server, such as Python, using different network protocol. Unity has its own limitation in supporting specific task, so offloading these task to a backend service is recommended. Choosing the right protocol for communication ensures efficient and reliable interaction between Unity and the backend.

## Network Protocol
| Protocol | Type | Strength | Limitation |
| ------------- | -------------------- | --------------------------------------------------------------- | --------------------------------------------------------- |
| **TCP** | Connection-oriented | Reliable delivery, ordered data | Slower than UDP, introduce lag for real-time update |
| **UDP** | Connectionless | Low-latency update | No delivery guarantee or order, possible some packet loss |
| **WebSocket** | Full-duplex over TCP | Real-time chat, dashboard, collaborative feature | Require a server, built on TCP, not suitable for ultra-low-latency task |
| **WebRTC** | Peer-to-peer communication framework built on UDP, TCP for the initial connection setup | Real-time audio, video, etc | More complicated to setup, require signaling server to exchange connection information before peer can communicate directly |
| **gRPC** | RPC over HTTP/2 | Structured, type-safe API call, backend service, non-real-time AI inference | Not optimized for ultra-low-latency real-time update |
| **HTTP/REST** | Request-response | Non-real-time backend task, configuration, database queries | Slower, not suitable for continuous streaming |

## Video Streaming
### FPS (Frame Per Second) Comparision
Check out the demonstration: [Watch FPS Comparison Video](https://youtube.com/shorts/Mi0yYKSMJUY?si=PKAk2fcQmaBr9Y5a)

In this video, observe how different frame rates (5 FPS vs 30 FPS vs 60 FPS) affect the visual smoothness of streaming. As the FPS increases, motion becomes noticeably smoother, while lower FPS results in choppier motion. 

### Asynchronous (async/await) vs Synchronous (sync)
In Unity streaming, asynchronous operation (async/await) are strongly recommended compared to synchronous (blocking) operation.

Synchronous (sync)
- Block the main Unity thread until the operation complete.
- Network read/write or frame encoding can freeze the game if delayed.
- Simple to implement, but not suitable for high FPS or real-time streaming.

Asynchronous (async/await)
- Allow the Unity main thread to continue running while waiting for task like network I/O or GPU readback.
- Prevent frame drop, stutter, and unresponsive UI.
- Essential for smooth, high-FPS camera streaming, VR/AR, or multi-client networking.
- Scale easily for multiple connections or tasks without blocking rendering.