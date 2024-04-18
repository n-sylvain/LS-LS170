1. **What is a network?**

A network is 2 or more points of communication connected in a way that allows them to send and receive information to the other connected machines. This can be as small as two computers connected by an ethernet cable and as vast as the entire internet of laptops, smart watches and robots world-wide,

2. **What is the Internet?**

The internet is a network of networks. At a local level we have devices connected on a LAN, usually wirelessly, to a switch or less commonly a hub. The switch/hub then sends on the transmission to a router which sends the transmission to its destination. This is usually a DNS server, which finds the IP address and sends it back. The originating device then uses this IP address to find the server it requires.

3. **Is the Internet the same thing as a network?** 

- No. The internet is a network, but not all networks are the internet. 

4. **What is WEB (world wide web)**

The World Wide Web is a service accessible on the internet. It is comprised of the websites and online services you use, and the internet is the network of computers that host them.

5. **What is the difference between network, Internet, and WEB?**

The Internet is a network of networks and the World Wide Web is a service provided on the internet. A single network can be two computers linked to each other, but to be connected to the internet those computers need to be connected to a device such as a switch or hub which can traffic their data to a router and on to a server. At the server, by a system of DNS

6. **What are LAN and WLAN?**

Local Area Networks are the networks formed by computers relatively near each other, for example in an office or a home. A WLAN is a Wireless Local Area Network and just means that the transmissions aren't travelling by physical cable, but by wireless signals like bluetooth or radiowaves. This is with a wireless Switch or hub as the central device. This will send on the signal to a router connecting it to the wider internet.

7. **What is a protocol?**

- Protocols are agreed standards for communication which mean that both parties in a network exchange know how to format outgoing signals and read incoming signals. They are comparable to the rules of language which facilitate communication between people. HTTP is a commonly used protocol for sending information between applications on the internet.

8. **What is the role of protocols?** 

- A protocol exists to deal with an aspect of communication between two points on the web. This could be two processes on the same device, or between devices thousands of miles away. Higher protocols deal with how Applications communicate and lower protocols are concerned with the successful transporting of the PDUs.

9. **Why there are many different types of protocols?**

- Different protocols address different aspects of communications on the web. For example for applications communicating at the Application layer, HTTP is commonly used, but at the Link layer HTTP cannot be used and the Ethernet protocol is the most commonly used protocol. Protocols also address the same aspect of communication in different ways. For example HTTP is used at the Application layer to communicate between applications on the web, but for file trsansfer FTP is more suitable and for email, SMTP. 

10. **What does it mean that a protocol is stateless?**

 With a stateless protocol, like HTTP, each PDU has no knowledge of the previous or next PDUs being sent. The stateless nature of HTTP means the following:
  - it is what makes the internet distributed and so difficult to control. 
  - It means that servers do not need to hang on to information between requests. 
  - It means that when a request breaks on the way to a server no clean-up is required
  - It makes HTTP a resilient protocol
  - It means that developers have to work hard to simulate statefulness, for example allowing a user to remain logged in to a website despite the HTTP packets having no connection to previous request/response cycles.
  - A negative is that it makes communications hard to secure and difficult to build on top of.

11. **Explain briefly what are OCI and TCP/IP models? What is the purpose of having models like that?** 

- The Open Systems Interconnection model and the Transmission Control Protocol/Internet Protocol are conceptual models for seperating different layers/aspects of communication between points on the internet. The OCI model has more layers. They are Physical, Data-link (these map to the Link layer in the TCP/IP model), Network (this maps to the Internet in the TCP/IP model), Transport (the same in the TCP/IP model), Session, Presentation and Application layers (these map to the Application layer in the TCP/IP model). The TCP/IP model defines each layer by the scope of its communication within each layer. So between networks, or within a LAN.THe OCI model on the other hand focuses on teh function of each layer, ie physical addressing and logical functioning.

12. **What is PDU? What is its role?**

- A Protocol data unit is a general term for the units of data that are generated by each layer of a transmission on the internet. At the application layer the data payload, which is the actual message to be delivered, is encapsulated in meta-data, most probably using HTTP. This is passed to the transport layer which encapsultates the message in meta-data relating to how to reliably transmit the message from one application to another. This PDU is called a segment. This is then encapsulated by the Internet layer which adds meta data to facilitate communication between hosts on different networks. This PDU uses IP and is called a packet. After this at the ethernet layer the data is encapsulated in a frame and sent on to the physical layer (in the OSI model), which is the information travelling in bits over the physical network.

13. **What is Data Payload?** 

The data payload is the part of a PDU containing the data that needs to arrive and be read by the receiver. It is the actual message, whereas the rest of the transmission contains meta-data to protect and direct the message.

14. **What is the relationship between PDU and Data Payload?** 

The data payload in encapsulated with meta-data by each PDU, making it the centre of a many layered message.

15. **Explain How lower-level protocols work in general?**

Lower level protocols encapsulate the data received from higher levels and then pass the PDU on to the layer below. So for example at the transport layer the data received is coming from the application layer and is most likely a HTTP request/response. This data has a header added to it and possibly a footer. If the transport layer is using TCP it will encapsulate the data in a segment, so the meta-data will relate to how to create a reliable data transfer and multiplex the data. This segment will then be passed to the lower layer, which in the TCP/IP model is the Internet layer.

16. **What is encapsulation in the context of networking?**

- In this context encapsulation relates to 

17. **Why do we need encapsulation?** 
18. **What are the characteristics of a physical network?** 
19. **How can we as developers deal with the limitations of physical network?**
20. **What is Latency?**
21. **What is** **Bandwidth?**
22. **What are** **Network 'Hops'?**
23. **What is the relationship between network 'Hops' and latency?** 
24. **What is a switch and what is it used for?**
25. **What is a hub and what is it used for?**
26. **What is a modem and what it is used for?**

- Modems (modulator-demodulators) are devices that allow digital communication devices, like computers or local networks, to connect to the internet by converting digital signals  into analog signals for transmission over a specific medium, and the same in the other direction.

27. **What is a router and what is it used for?**

- Routers are machines that receive network traffic, process it and forward it to other networks. Within a LAN they act as gateways in and out.

28. **What is the difference between a switch, hub, modem, and router?**

- A switch, modem or hub act as the central device in a LAN. Hubs are inefficient because they forward any transmission to all devices on the network and depend on these devices to discard messages not intended for them. Switches are preferable in modern systems because they use destination addresses to direct data to their intended destination. They do this by using a MAC address table to send data through the coresponding data-port.
- Modems (modulator-demodulators) and routers are devices that allow devices or local networks, to connect to the internet by converting digital signals into analog signals for transmission and the same in the other direction. They are like gateways into and out of LANs.

29. **How does the Internet work?**
30. **What is a MAC address and what is its role in network communication?** 
31. **Give an overview of the Link/Data Layer**
32. **What is included in an Ethernet frame?**
33. **Give an overview of the Internet/Network Layer and it's role.**
34. **What is IP?**
35. **What is IP address?** 
36. **What are the components of IP addresses?** 

- IPv4 addresses (32bits) are composed 4 sections of 8 bits. When converted from binary to decimal these sections represent numbers between 0 and 255. It could look like this: `101.05.244.99`. IPv6 addresses (128 bits) are composed of 8 sets of hexadecimal characters, each set representing different aspects of a location on the network. It could look like this: `2001:0db8:85a3:0000:0000:8a2e:0370:7334` .

37. **What is a packet in computer networking?**
38. **Why do we need both MAC addresses and IP addresses?** 
39. **What is DNS and how does it work?**
40. **How do port numbers and IP addresses work together?**
41. **What is a checksum and what is it used for? How is it used?**

A checksum is a window in a PDU, for example the Frame Check Sequence in an Ethernet frame implements a checksum. The function of a checksum is to check that the data received is the same as the data sent. This is done by using an agreed upon algorithm to generate the checksum based on the data in the PDU. This guards against corrupted or falsified transmissions. If the checksums do not match then the PDU is dropped. TCP segments also use checksums.

42. **Give an overview of the Transport Layer.** 

-	The Transport layer is concerned with facilitating reliable communication between networked applications. It receives data from the layer above it, which is the application layer (or session layer in OCI model) encapsulates that data, usually with TCP into a segment and passes the segment to the Network layer. This also happens in reverse when packets are received from the Network/internet layer. 

43. **What are the fundamental elements of reliable protocol?**

For a protocol to be considered reliable it must take care of:
-	In-order delivery: Data must be received in the order it was sent.
-	Error detection, using a checksum to check for corrupt data.
-	Handling data-loss: Lost data is resent using a system of acknowledgements and time-outs.
-	De-duplication: duplicate data should be eliminated by using an idempotency token system.

44. **What is pipe-lining protocols? What are the benefits of it?**

-	Pipe-lining is sending multiple messages before having received acknowledgements. It is a way of more efficiently using bandwidth. The number of messages that can be sent before an acknowledgement has been received is indicated in the Window field of a TCP segment.

45. **What is a network port?**

A network port is the same as a port number in the question below. It is a number between 0 and 65535 that identifies a specific process on a host. 0 – 1023 is for well-known ports, 1024 – 49151 is for registered ports assigned to private entities and 49152 to 65535 is for ephemeral ports, ie customised services.

46. **What is a port number?**

- A port number is an identifier between 0 and 65535 for a specific process on a host. Each process will expect to send and receive data-packets, but for the sake of efficiency these packets will be multiplexed so that more can be sent at the same time. They are then demultiplexed at the receiving end into individual packets for each port and its application. The Transport layer deals with transporting data from one machine to another, but once it gets there it needs to be delivered to a specific port in order to be funnelled to a particular process. The application layer is where the Request/response payload is generated and the Transport layer deals with multiplexing these into segments (or datagrams)

47. **What is a network socket?**

- In brief they are the combination of IP address and port number, for example 216.3.128.12:8080.  
- It represents an end-point for communication between networked processes.
- At an implementation level it can refer to a few things:
  - A UNIX socket: a way of local processes on the same machine communicating
  - Internet sockets: (like a TCP/IP socket) A way for networked processes on different machines to communicate.
- Weirdly, two processes on the same machine could be using internet sockets to communicate, without actually going out onto the internet.
- Just remember there's a difference between the concept of a socket and it's implementation in code.
- In socket programming this involves instantiating a socket object.
- These socket instances are what are created in a connection-oriented protocol to allow a machine to form specific connections for each channel. Every time a new message arrives with a new source address it will be assigned to a new socket. If the message is coming from a source that has already been assigned to a socket it will be passed to that socket. 
- This adds to the reliability of the communication. and allows one to manage each communication uniquely, for instance acknowledgements and retransmission of lost messages.

48. **Is TCP connectionless? Why?**

TCP is connection-oriented, which is essential because one of its main functions is to provide reliability on an unreliable channel. It does not start sending data until a connection has been established with the “three-way-handshake”. This involves sending a `SYN` segment (synchronising), the receiver responding with a `SYN ACK` segment and the first party responding with an `ACK` segment and beginning transmission of application data.
This handshake process has a cost in latency since it means there is always a round-trip of latency before applications can begin to send data.

49. **How do sockets on the implementation level relate to the idea of protocols being connectionless or connection-oriented?** 

-	See q47

50. **What are sockets on implementation and on a theoretical level?** 

-	See q47

51. **What does it mean that the protocol is connection-oriented?**

-	A connection oriented protocol means that when the host receives a message it checks the source and if it is new source, ie if the Source/destination IP address and Source/destination port number are not yet assigned to a socket, the host will instantiate a new socket to listen for messages matching this four-tuple of information. This means that there will be unique sockets for each channel of communication between processes. A connectionless protocol on the other hand will rely on one socket to listen for all data sent to that particular IP address/destination port number pair.

52. **What is a three-way handshake? What is it used for?**

- see q48

53. **What are the advantages and disadvantages of a Three-way handshake?** 
54. **What are multiplexing and demultiplexing?**
55. **How does TCP facilitate efficient data transfer?**
56. **What is flow control? How does it work and why do we need it?**

Flow control is a mechanism which aims to prevent the sender from overwhelming the receiver. The WINDOW field of a TCP segment indicates how much data it is willing to receive. This number is dynamic and can be reduced if the receiver is at risk of being overwhelmed, ie if the buffer is getting too full. Flow control means that the sender and receiver don't overwhelm each other, but doe not address the problem of overwhelming the network.

57. **How does TCP prevent the receiver's buffer from getting overloadeded with data?**

- Flow control. See previous question

58. **What is congestion avoidance?**  

- A way of vaoiding network congestion.

59. **What is network congestion?**

- To make data transfer as efficient as possible TCP employs flow-control and congestion avoidance. Congension happens when there is more traffic on a network than can be processed. This is different to flow control which tries to prevent the sender from overloading the receiver with too much data. IP packets moving across the network in hops need to be processed at each stage of their journey. If the machine processing them has more data than it can manage the packet is dropped and disappears. Routers have buffers to store queued data, but overflow is dropped. If data is lost then TCP retransmits the data. Losing lots of data is used as a metric to control the flow of data in order to avoid congestion. It does this by reducing the transmission window.

60. **How do transport layer protocols enable communication between processes?**
61. **Compare UDP and TCP. What are similarities, what are differences? What are pros and cons of using each one?** 

- Broadly speaking TCP is more reliable, but UDP is faster and more flexible. TCP deals with transferring data reliably while using an unreliable channel. It deals with data-integrity, de-duplication, in-order delivery and retransmission of lost data. Also multiplexing and data-encapsulation. TCP uses flow control and congestion avoiddance techniques. This comprehensive list of roles comes with a cost in terms of performance and complexity and can cause Head-of -Line blocking on top of a larger latency overhead. UDP (User Datagram Protocol) on the other hand is much faster because it leaves out many of the services described above. The datagrams only have 4 fields: source port, destination port, checksum (optional) and length. It leaves outa guarantee of message delivery or message delivery order and leaves out any congestion avoidance/flow control mechanisms and connection-state tracking (as it is a connectionless protocol). The benefit of this is that UDP can start sending data immediately and needn't wait for a connection to be established.The lack of acknowledgement means all messages are assumed to have gone through and nothing  is retransmitted. So traffic is one way and therfore latency is much lower. The lack of in-order delivery prevents HOL blocking. 

62. **What does it mean that network reliability is engineered?**
63. **Give an overview of the Application Layer.** 
64. **What is HTML?**
65. **What is a URL and what components does it have?**
66. **What is a Query string? What it is used for?**
67. **What URL encoding is and when it might be used for?**
68. **Which characters have to be encoded in the URL? Why?**
69. **What is www in the URL?** 
70. **What is URI?**
71. **What is the difference between scheme and protocol in URL?**
72. **What is HTTP?**
73. **What is the role of HTTP?**
74. **Explain the client-server model of web interactions, and the role of HTTP as a protocol within that model**
75. **What are HTTP requests and responses? What are the components of each?**
76. **Describe the HTTP request/response cycle.**
77. **What is a** s**tate in the context of the 'web'?**
78. **What is** s**tatelessness?**

A protocol is said to be [stateless](https://launchschool.com/books/http/read/background#statelessness) when each request/response cycle is completely independent of each other. HTTP is a stateless protocol which means that stateful web applications must implement statefulness with things like sessions, cookies and AJAX. These can allow a user to remain logged in for example while accessing different parts of a website.

79. **What is a stateful Web Application?**
80. **How can we mimic a stateful application?**
81. **What is the difference between stateful and stateless applications?**
82. **What does it mean that HTTP is a 'stateless protocol?** 
83. **Why HTTP makes it difficult to build a stateful application?**
84. **How the idea that HTTP is a stateless protocol makes the web difficult to secure?** 
85. **What is a `GET` request and how does it work?** 
86. **How is `GET` request initiated?**
87. **What is the HTTP response body and what do we use it for?**
88. **What are the obligatory components of HTTP requests?** 
89. **What are the obligatory components of HTTP response?**
90. **Which HTTP method would you use to send sensitive information to a server? Why?**
91. **Compare `GET` and `POST` methods.**
92. **Describe how would you send a `GET` request to a server and what would happen at each stage.**
93. **Describe how would you send `POST` requests to a server and what is happening at each stage.**
94. **What is a status code? What are some of the status codes types? What is the purpose of status codes?** 
95. **Imagine you are using an HTTP tool and you received a status code `302`. What does this status code mean and what happens if you receive a status code like that?** 
96. **How do modern web applications 'remember' state for each client?**
97. **What role does AJAX play in displaying dynamic content in web applications?**
98. **Describe some of the security threats and what can be done to minimize them?**
99. **What is the Same Origin Policy? How it is used to mitigate certain security threats?**  
100. **What determines whether a request should use `GET` or `POST` as its HTTP method?**
101. **What is the relationship between a scheme and a protocol in the context of a URL?**
102. **In what ways can we pass information to the application server via the URL?**
103. **How insecure HTTP message transfer looks like?**
104. **What services does HTTP provide and what are the particular problems each of them aims to address?**
105. **What is TLS Handshake?**

The Transport Layer Security Handshake is a 3 way exchange that uses symmetric and asymmetric encryption to add a layer of security onto HTTP, an otherwise insecure protocol. The first part of this handshake is the `ClientHello` message which is sent after the final message of the TCP exchange, namely the `ACK` message. The `ClientHello` message contains the maximum version of TLS the client can support and a list of cypher suites the client is able to use. Then the server sends back a message containing a `ServerHello` message, which sets the protocol and the cypher suite to be used. It also sends its certificate which contains its public key and a `ServerHelloDone` which tells the client that this part of the handshake is finished. Once the Client receives this it knows it can begin the exchange process.

106. **What is symmetric key encryption? What is it used for?**
107. **What is asymmetric key encryption? What is it used for?**
108. **Describe SSL/TLS encryption process.**
109. **Describe the pros and cons of TLS Handshake**
110. **Why do we need digital TLS/SSL certificates?** 
111. **What is it CA hierarchy and what is its role in providing secure message transfer?**
112. **What is Cipher Suites and what do we need it for?**
113. **How does TLS add a security layer to HTTP?**
114. **Compare HTTP and HTTPS.**
115. **Does HTTPS use other protocols?** 
116. **How do you know a website uses HTTPS?**
117. **Give examples of some protocols that would be used when a user interacts with a banking website. What would be the role of those protocols?** 
118. **What is server-side infrastructure? What are its basic components?**
119. **What is a server? What is its role?** 
120. **What are optimizations that developers can do in order to improve performance and minimize latency?**

- get ride of unnecessary round-trips, by reducing the number of resources to be fetched. SO for instance if a javascript file is only used on one page, make sure it isn;’t loaded by all pages. This reduces ‘page-bloat’.
- minimise the size of resources to be fetched by using data-compression techiques. Programs like gzip can reduce data size on text-based assets by 60 – 80 %. This could be by reducing white-space and code-comments.
- Re-use TCP connections with keepalive connections.
- DNS optimisations. Reduce the number of host names that need to be looked up. Download external resources and host them locally. Get a faster DNS provider.
- Caching. These are short term memory banks on the server. They store content that has been recently accessed by a user
