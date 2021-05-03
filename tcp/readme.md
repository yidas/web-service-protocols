TCP
===

The Transmission Control Protocol (TCP) is one of the main protocols of the Internet protocol suite. It originated in the initial network implementation in which it complemented the Internet Protocol (IP). Therefore, the entire suite is commonly referred to as TCP/IP. 

### Basic Concept

TCP protocol operations may be divided into three phases. Connection establishment is a multi-step handshake process that establishes a connection before entering the data transfer phase. After data transfer is completed, the connection termination closes the connection and releases all allocated resources.

#### Sequence Diagram

![Basic Flow](https://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/yidas/web-service-principles/main/tcp/basic-flow.plantuml)

---

### Detailed Process

A TCP connection is managed by an operating system through a resource that represents the local end-point for communications, the Internet socket. During the lifetime of a TCP connection, the local end-point undergoes a series of state changes.

#### Sequence Diagram

![Detailed Flow](https://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/yidas/web-service-principles/main/tcp/detailed-flow.plantuml)

References
----------

[Wikipedia - Transmission Control Protocol](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)

[Wikipedia - Transmission Control Protocol - Protocol operation](https://en.wikipedia.org/wiki/Transmission_Control_Protocol#Protocol_operation)
