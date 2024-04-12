##### LS171 Assessment: Networking Foundations

---

## Key Ideas and Concepts

### The Internet

---

#### What is the Internet and how does it work?

The Internet may be conceived of a vast network of networks. At the most basic level, this means a large interconnected system of computers, switches, and routers communicating with each other. The physical channels of communication include wires and radio waves. The Internet is designed in such a way that it is fully distributed with no central control deciding how information is routed or where pieces of the network are built, or even who interconnects those various pieces.  

Like any system of communication, the Internet employs rules for how communication should occur over the network. Machines and software need to be able to speak the same language in order for orderly communication to take place. A protocol is the name for a set of rules used for network communication. The Internet employs different protocols for different aspects of network communication or for different purposes within the same aspect of network communication. Some protocols are concerned with the flow and order of messages (e.g. TCP), whereas other protocols are concerned with the structure of those messages (e.g. HTTP).  

Thus, the Internet can be thought of as a vast network of networks through which orderly communication between devices takes place in accordance with a set of protocols.  

##### OSI and Internet Protocol Suite Models

There are two main models that have been constructed in order to help us understand at a much deeper level what is going on "under the hood" of the Internet. Those two models are the Open Systems Interconnection (OSI) model and the Internet Protocol Suite model (also known as the TCP/IP model or DoD model). Both models break network communication down into separate layers (7 in the OSI model and 4 in the TCP/IP model):

OSI Model Layers (from the topmost layer):

* Application
* Presentation
* Session
* Transport
* Network
* Data Link
* Physical

TCP/IP Model Layers (from the topmost layer):

* Application
* Transport
* Internet
* Link

The top three layers of the OSI Model mostly map to the topmost layer of the TCP/IP Model. The Transport layer of both models are roughly equivalent, as are the Network and Internet layers of the respective models. The Datalink and Physical layers of the OSI model mostly map to the Link layer of the TCP/IP model.  

Separating network communication into these separate layers allows us to group the various protocols according to the layer of communication to which they apply. The idea is that at each layer, protocols determine how the data moving across the network must be structured. At each layer, data is encapsulated within a data unit according to the rules defined by a specific protocol, and consequently hiding the data from the layer below it.  

##### Protocol Data Units (PDUs)

These data units are called protocol data units (PDUs), although these PDUs are given more specific names at different layers. For example, at the Transport layer, PDUs are called segments (TCP) or datagrams (UDP); at the Internet/Network layers they are called packets; and at the Link/Data Link layers they are called frames. But no matter what layer we are at, every PDU consists of a header, a data payload, and in some cases a trailer or footer.  

The exact structure of the header and, if included, trailer depends on the specific protocol being used, but the purpose in each case is the same: to provide protocol-specific metadata about the PDU.  

The data payload portion of the PDU is just the data we want to transport over the network using a specific protocol at a particular network layer.  It is the key to the way that encapsulation is implemented: the data payload at one layer is simply the entire PDU from the layer above it. Thus, the PDU at one layer is encapsulated within the data payload of the PDU from the layer below. The layer below is essentially providing a service to the layer above it.  

---

#### What are the characteristics of the physical network, such as latency and bandwidth?

It's easy to think of the Internet as something immaterial. It allows us to send messages without having to actually write something down on a physical piece of paper. But the Internet, at its most basic level, is a 'physical' network comprised of tangible pieces such as networked devices, cables, and wires. Even the radio waves used in wireless networks, though we can't touch or see them, exist in the physical realm and are bound by the physical laws and rules.  

If we think of the Physical Layer of the OSI model, we are essentially concerned with the transfer of bits (binary data). In order to be transported, these bits are converted into signals. Depending on the transportation medium used, bits are converted to electrical signals, light signals, or radio waves. Because the Internet is comprised of physical devices and connections it faces physical constraints.  

Two characteristics that concern the Internet's physical contstraints include latency and bandwidth. Latency refers to the _length of time_ it takes for some data to get from one point of the network to another point in a network, while bandwidth refers to the _amount of data_ that can be sent at once.  

##### Latency

Latency is a measure of delay and there are four different types of delay that comprise the overall latency of any network connection: propagation delay, transmission delay, processing delay, and queuing delay. Propagation delay is the time it takes data to travel the distance between sender and receiver. Transmission delay is the time it takes data to traverse a network link. Processing delay is the time it takes data to be processed when it arrives at a link, or node, in the network. Queuing delay is the time it takes data to queue, or buffer, while it waits to be processed. The total latency between two points, such as a client and a server, is the sum of all of the delays above, usually measured in milliseconds (ms).  

Last-mile latency is a concept that refers to the end part of the data's journey. There are usually more delays that take place near the end points of networks and thus it takes longer for data to traverse individual subnetworks than it does for it to traverse the core network. The 'hops' within the core part of the network are longer with less interruptions for transmission, processing, and queuing. At the network edge, there are more frequent and shorter hops as the data is directed down the network hierarchy to the appropriate sub-network. You can think of the network edge as the 'entry point' into a network like a home or corporate LAN.  

##### Bandwidth

Bandwidth, as mentioned, refers to the amount of data that can be sent at any one time. This amount is not a constant but will vary at different points throughout the network. For example, the capacity, or bandwidth, of the core network is going to be much higher than the part of the network infrastructure that ultimately connects to your home or office building. The bandwidth that a connection receives is the lowest amount at a particular point in the overall connection. A point at which bandwidth changes from relatively high to relatively low is generally referred to as a bandwidth bottleneck.  

---

#### How do lower level protocols, such as Ethernet and IP, operate?

Just above the Physical Layer in the OSI model is the Data Link Layer. The TCP/IP model essentially wraps both of these layers into one Link Layer. The protocols operating at this layer are primarily concerned with the identification of devices on the physical network and moving data over the physical network between the devices that comprise it, such as hosts (e.g. computers), switches, and routers. This layer can be thought of as an interface between the workings of the physical network and the more logical layers above.  

##### The Link/Data Link Layer and the Ethernet Protocol

The most commonly used protocol at this layer is the Ethernet protocol and its two most important aspects are framing and addressing.  

The PDU of the Ethernet protocol is known as a frame. It encapsulates data from the Internet/Network layer above. It is important to note that the Link/Data Link Layer is the lowest layer at which encapsulation takes place. At the physical layer, the data is essentially a stream of bits in one form or another without any logical structure. An Ethernet Frame adds logical structure to this binary data. The frame structures the data by defining which bits are the data payload and which bits are the metadata used in the process of transporting the frame.  

###### MAC Address

That metadata includes a header, which includes the source and destination MAC addresses of the frame. A unique MAC address is assigned to each network-enabled device when it is manufactured (it is sometimes known as the physical address or burned-in address because it is permanent and does not change). The source address included in the header is the address of the device that created the frame (and this can change at various points along the data's journey). The destination MAC address is the address of the device for which the data is intended.  

Local networks nowadays use switches to direct frames to the intended device. A switch does this by keeping and updating a record of the MAC addresses of the devices connected to it, and associating each address with the Ethernet port to which the device is connected on the switch. It keeps this data in a MAC Address Table, a simple representation of which might look something like this:

| Switch Port | MAC Address       |
| :---------- | :---------------- |
| 1           | 00:40:96:9d:68:0a |
| 2           | 00:A0:C9:14:C8:29 |
| 3           | D8:D3:85:EB:12:E3 |
| 4           | 00:1B:44:11:3A:B7 |

The MAC Addressing system works well for local networks, where all the devices are connected to a switch that can keep a record of each device's address. In theory, we could conduct inter-network communication just using MAC addresses. In practice, however, there's an issue that prevents us from doing this: scale. This approach isn't scalable because: 1) MAC addresses are physical rather than logical in that each MAC Address is tied to a specific physical device; and 2) MAC Addresses are flat rather than hierarchical, meaning the entire address is a single sequence of values and can't be broken down into sub-divisions.  

##### The Internet/Network Layer and the Internet Protocol (IP)

The problem of scale is solved at the next layer above, the Network/Internet Layer.  The primary function of protocols at this layer is to facilitate communication between hosts (e.g. computers) on different networks. The Internet Protocol (IP) is the predominant protocol used at this layer for internetwork communication and there are two versions of IP currently in use: IPv4 and IPv6.  

Although there are differences between the two versions, the primary features of both are the same:

* Routing capability via IP addressing.
* Encapsulation of data into packets.

The PDU for IP is referred to as a _packet_, which is comprised of a data payload and a header. Like Ethernet Frames, the data payload of an IP Packet is the PDU from the layer above (the Transport Layer). It will generally be a TCP segment or a UDP datagram. The header is split into logical fields which provide metadata used in transporting the packet.  

Whereas the Ethernet protocol provides communication between devices on the same local network, IP enables communication between two networked devices anywhere in the world. We can send a message from one device on the internet and it can reach another device on the Internet.  

---

#### What is an IP Address? What is a Port Number?

##### IP Addresses

IP addresses identify individual devices, but unlike MAC addresses, they are logical in nature. This means that they are not tied to a specific device, but can be assigned as required to devices as they join a network.  

The IP address to which the device is assigned must fall within a range of addresses available to the local network within which the device is connected. This range is defined by a network hierarchy, where an overall network is split into logical subnetworks, with each defined by the range of IP addresses available to it.  

A basic exampe of this hierarchy would be if all the addresses in the range `109.156.106.0` to `109.156.106.255` were assigned to a single local network. Each network defines the address at the start of the range as the _network address_, and the address at the end of the range as the _broadcast address_. Addresses between the network and broadcast addresses can be allocated to individual devices on the network.  

The network address of the range is used to identify a specific network segment. What this means is that a router that wants to forward an IP packet to any address in the entire range only needs to keep a record of which router on the network controls access to the segment with that network address. This logic is what creates the hierarchical structure, and means that routers don't need to keep records of every single device within an addressable range.  

All routers on the network store a local routing table. When an IP packet is recieved by a router, the router examines the destination IP address and matches it against a list of network addresses in its routing table. The matching network address will determine where in the network hierarchy the subnet exists. This will then be used to select the best route for the IP packet to travel.  

An important thing to understand about the Internet Protocol, and its system of addressing, is that it is intended to provide communication between *hosts*, or devices. These hosts can potentially be on the same local network, or on different local networks halfway around the world from each other. Either way, we can use IP to get a message from one host to the other, but not any more than that.  

As we know though, there are potentially many applications running on a single host. IP can get us as far as the host, but we need a way to provide communication between an application running on one host and an application running on another host (or potentially between two different applications or processes running on the same host). This can be achieved trough the use of port numbers, which brings us to the Transport Layer.  

##### Port Numbers

A port number is an identifier for a specific proccess/application running on a host. This identifier is an integer in the range 0-65535, with sections of the range reserved for specific purposes: 0-1023 are well-known ports; 1024-49151 are registered ports; 49152-65535 are dynamic ports, or private ports, used for customized services or for allocation as _ephemeral ports_.  

Services running on servers will likely have a port in the well-known range assigned to them. A service running on a client machine, for example in a browser running on your laptop, won't use any of these well-known ports, but instead have an ephemeral or temporary port assigned to it by the operating system, for example 59258.  

Source and destination port numbers comprise part of the header of the PDU at the Transport layer, whether that PDU be a TCP segment or a UDP datagram. Like PDUs at other layers, the PDU at the transport layer is encapsulated as the data payload of the layer below, which in this case, is the Internet/Network Layer.  

The header of an IP packet at the Internet/Network Layer contains the source and destination IP addresses. These IP addresses can be used to direct data from one host to another. The IP address effectively creates a communication channel between hosts. But it is only in combination with the port number that we are able to achieve end-to-end communction between specific applications on different machines.  

The combination of IP address and port number can be thought of as defining a _communication end-point_. This communiction end-point is generally referred to as a _socket_. A socket can be thought of as a combination of IP address and port number, for example `216.3.128.12:8080`.  

Socket objects are defined by the local IP and port number as well as the IP and port of the process/host that sent the message. Such a socket object would listen specifically for messages where all four pieces of information matched (source port, source IP, destination port, destination IP). The combination of these four pieces of information are commonly referred to as a four-tuple. New socket objects are instantiated for unique four-tuples, which effectively represent a new connection.  

A good analogy of a socket is to think of an IP address as the street address of an apartment building and port numbers as unit numbers of the individual apartments within the building.  

The advantage of having a dedicated connection like this between a specific process running on one host and a specific process running on another host is that it more easily allows you to put in place rules for managing the communication such as the order of messages, acknowledgements that messages have been received, retransmission of messages that weren't received, and so on. These additional types of communication rules add more reliability to the communication.  

Port numbers enable functions known as _multiplexing_ and _demultiplexing_. Multiplexing and demultiplexing provide for the transmission of multiple signals over a single channel. In the context of a communication network, this idea of transmitting multiple signals over a single channel is known as multiplexing, with demultiplexing being the reverse process.  

An IP address establishes a single communication channel between hosts; port numbers allow us to transmit data from different applications over this single channel and then disaggregate that data to its proper destination. This is what we mean by multiplexing and demultiplexing and these functions are enabled through the use of network ports.  

---

#### How does DNS work?

DNS stands for Domain Name System, which consists of a distributed database that translates a _domain name_, such as `google.com`, to an IP address, such as `216.58.213.14`. In other words, DNS keeps track of URLs and their corresponding IP addresses on the Internet. The domain name is just a human-friendly name that represents a less human-friendly IP address associated with a remote computer or a server.  

DNS databases are stored on computers called DNS servers. It is important to note that there is a very large world-wide network of hierarchichally organized DNS servers, and no single DNS server contains the complete database. If a DNS server does not contain a requested domain name, the DNS server routes the request to another DNS server up the hierarchy. Eventually, the address will be found in the DNS database on a particular DNS server, and the corresponding IP address will be used to receive the request.  

---

#### What is the client-server model of web interactions? And what is the role of HTTP as a protocol within that model?

The client-server model of web interactions allows us to distinguish between the roles of different participants in a data message exchange using the world wide web. The client is the participant that makes a request and the server is the particpant that issues responses to requests. You can have many clients connecting to the server, but the dynamic between client and server remains the same.  

One of the best examples of a client is an application that we use every day--a web browser, like Firefox, Safari, or Chrome. Web browsers issue HTTP requests and then process the HTTP response in a user-friendly manner onto your screen. Web browsers, of course, are not the only types of clients that exist.  

Servers, on the other hand, are remote computers that are capable of handling inbound requests and issuing responses to those requests. Often, the response they send back contains relevant data as specified in the request.  

##### Hypertext Transfer Protocol (HTTP)

HTTP is a system of rules that serve as a link between applications and the transfer of hypertext documents. Stated differently, it's an agreement, or message format, of how machines communicate with each other. Since HTTP follows the client-server model whereby a client makes a request to a server and waits for a response, it is often referred to as a _request-response protocol_.  

The main thing to understand is that when the browser issues a request, it is simply sending some text to an IP address. Because the client (web browser) and the server have an agreement, or protocol, in the form of HTTP, the server can take apart the request, understand its components and send a response back to the web browser. 

---

### TCP & UDP

---

#### What are the TCP and UDP protocols? What are their similarities and differences?

Both TCP and UDP are protocols that operate at the Transport Layer. They implement a different set of rules for the transmission of data, as we shall see below.  

##### Transmission Control Protocol (TCP)

TCP is one of the corner-stones of the Internet. One of its key characteristics is that it provides reliable data transfer. It is designed in a way that it must recover from data that is damaged, lost, duplicated, or delivered out of order by the internet communication system. TCP essentially provides reliable network communication on top of an unreliable channel. But it also provides data enscapsulation and multiplexing, which it achieves through the use of TCP Segments.  

Segments are the PDU of TCP. Like the PDUs of protocols we've looked at for other network layers, it uses a combination of headers and payload to provide encapsulation of data from the layer above. Two of the most important fields in the header are the _source port_ and the _destination port_, as these provide for the multiplexing capability of the protocol. Most of the other header fields are related to the way TCP implements reliable data transfer.  

For instance, the CHECKSUM field contains a Checksum value that supplies the Error Detection aspect of TCP reliability. The sender generates this error-checking value using an algorithm; the receiver then uses the same algorithm to generate a value that should match the value generated by the sender. However, if the two values do not match, the Segment is dropped.  

The SEQUENCE NUMBER and ACKNOWLEDGEMENT NUMBER fields are used together to provide for the other elements of TCP reliability such as In-order Delivery, Handling Data Loss, and Handling Duplication. The WINDOW SIZE field is related to _flow control_.  The Flag fields `URG` and `PSH` are related to how the data contained in the Segment should be treated in terms of importance and urgency. The `SYN`, `ACK`, `FIN`, and `RST` flags are used to establish and end a TCP connection, as well as manage the state of that connection.  

Some key characteristics of TCP are:

* It is a connection-oriented protocol, using the three-way handshake to establish a connection.
* It provides reliability through _message acknowledgement_ and _retransmission_, and _in-order delivery_.
* It also provides _Flow Control_ and _Congestion Avoidance_.

There are, however, some disadvantages to using TCP. Essentially, the flip-side of all the benefits that TCP provides are the performance challenges that come with the complexity associated with those benefits. The main downsides include the _latency overhead_ of _establishing a connection_, and the potential _head-of-line (HOL) blocking_ resulting from in-order delivery.  

A lot of the latency overhead has to do with the round-trip latency associated with the three-way handshake for establishing the initial connection. But head-of-line blocking can also add to that latency overhead.  

Head-of-line blocking is a general networking concept, and isn't specific to TCP. In general terms it relates to how issues in delivering or processing one message in a sequence of messages can delay or 'block' the delivery or processing of the subsequent messages in the sequence.  

HOL blocking can occur as a result of the fact that TCP provides for in-order delivery of Segments. If one of the segments goes missing and needs to be retransmitted, the segments that come after it in the sequence can't be processed, and need to be buffered until the retransmission has occurred. This can lead to increased queuing delay, which is one of the elements of latency.  

##### User Datagram Protocol (UDP)

UDP is a very simple protocol compared to TCP. It does provide multiplexing, but it does not provide reliability, in-order delivery, nor congestion or flow control. UDP is a _connectionless_ protocol, and so does not need to establish a connection before it starts sending data. While unreliable, the advantage of UDP is its simplicity, as well as speed and flexibility.  

The PDU of UDP is known as a Datagram. Like other PDUs it encapsulates data from the layer above into a payload and then adds header information. Unlike TCP Segments, the header of a UDP Datagram has only four fields: source port, destination port, UDP length, and a Checksum field to provide for error detection.  

Through the use of the source and destination port numbers, UDP provides multiplexing in the same way that TCP does. But unlike TCP, it doesn't do anything to resolve the inherent unreliability of the layers below it.  

Applications using UDP at the Transport layer can start sending data without having to wait for a connection to be established. Also, the lack of acknowledgements and retransmissions means that the actual data delivery is faster; once a datagram is sent it doesn't have to be sent again.  

Latency is less of an issue since without acknowledgements data essentially just flows one way: from sender to receiver. The lack of in-order delivery also removes the issue of HOL blocking (at least at the Transport layer).  

It's worth noting that although basic UDP does not implement these reliability features that TCP does, someone building a UDP-based application can still implement some of those features themselves. The specifics of which features to include are left up to the software engineer and can be implemented at the application level, effectively using UDP as a 'base template' to build on top of.  

To sum up the differences between UDP and TCP here is a list of basically all the things that UDP doesn't do that TCP does do:

* Guarantee of message delivery (UDP: no; TCP: yes).
* Guarantee of messsage delivery order (UDP: no; TCP: yes).
* Built-in congestion avoidance or flow-control mechanisms (UDP: no; TCP: yes).
* Connection state tracking (UDP: no; TCP: yes).

---

#### What is the three-way handshake and its purpose?

TCP is a connection-oriented protocol, which means that it doesn't allow for the transmission of application data until a connection has been established between application processes. In order to establish a connection TCP uses what is known as a three-way handshake.  

In the three-way handshake process, the following happens:

* The sender sends a SYN message (a TCP Segment with the `SYN` flag set to `1`).
* Upon receiving this SYN message, the receiver sends back a SYN ACK message (a TCP Segment with the `SYN` and `ACK` flags set to `1`).
* Upon receiving the SYN ACK, the sender then sends an `ACK` (a TCP Segment with the `ACK` flag set to `1`).  

Upon sending the ACK, the sender can immediately start sending application data. The receiver must wait until it has received the ACK before it can send any data back to the sender.  

One of the main reasons for this process is to synchronise the sequence numbers that will be used during the connection.  

---

#### What is Flow Control? What is Congestion Avoidance?

TCP involves a lot of overhead in terms of establishing connections, and providing reliabilty through the retransmission of lost data. In order to mitigate against this additional overhead, it is important that the actual functioning of data transfer when using the protocol occurs as efficiently as possible. In order to help facilitate efficient data transfer once a connection is established, TCP provides mechanisms for flow control and congestion avoidance.  

##### Flow Control

Flow control is a mechanism to prevent the sender from overwhelming the receiver with too much data at once. The receiver will only be able to process a certain amount of data in a particular time-frame. Data awaiting processing is stored in a 'buffer'. The buffer size will depend on the amount of memory allocated according to the configuration of the OS and the physical resources available.  

Each side of a connection can let the other side know the amount of data that it is willing to accept via the WINDOW field of the TCP header. This number is dynamic, and can change during the course of a connection. If the receiver's buffer is getting full it can set a lower amount in the WINDOW field of a Segment it sends to the sender, the sender can then reduce the amount of data it sends accordingly.  

Although flow control prevents the sender from overwhelming the receiver, it doesn't prevent either the sender or receiver from overwhelming the underlying network. For that task we need a different mechanism: congestion avoidance.  

##### Congestion Avoidance

Network congestion is a situation that occurs when there is more data being transmitted on the network than there is network capacity to process and transmit the data. You can perhaps think of it as similar to a gridlock of vehicles on a road network. Instead of things coming to a standstill, however, the 'excess vehicles' are simply lost.  

IP packets move accross networks in a series of 'hops'. At each hop, the packet needs to be processed: the router at the current hop runs a checksum on the packet data; it also needs to check the destination address and work out how to route the packet to the next hop on its journey to that destination.  

All of this processing takes time, and a router can only process so much data at once. Routers use a 'buffer' to store data that is awaiting processing, but if there is more data to be processed that can fit in the buffer, the buffer over-flows and those data packets are dropped.  

As already mentioned, TCP retransmits lost data. If lots of data is lost that means lots of retransmitted data, which is inefficient. In order to keep retransmission to a minimum, TCP will use data loss as a feedback mechanism to detect, and avoid, network congestion. If lots of retransmissions are occurring, TCP takes this as a sign that the network is congested and reduces the size of the transmission window.  

---

### URLs

---

#### What is a URI? What is a URL?

##### Uniform Resource Identifiery (URI)

A URI is a sequence of characters that identifies a particular resource, whether abstract or physical. It is part of a system by which resources should be uniformly addressed on the Web. The Web is an infomration space and URIs are the points in that space.  

##### Uniform Resource Locator (URL)

Addresses, such as `https://www.facebook.com/games`, are known as URLs. A URL is like the address or phone number you need in order to visit or communicate with your friend. A URL is the most frequently used part of the general concept of a URI.

A URL refers to the subset of URIs that, in addition to identifying a resource, provide a means of locating the resource by describing its primary access mechanism (e.g. its network "location").

Technically, something like `https://launchschool.com/forum` could be referred to as both a URL and a URI. For ease of communication though it's probably best to just stick with URL, since this is a more specific description.

---

#### What are the components of a URL, including query strings?

A URL can be broken down into 5 separate parts. Take the following URL as an example: `http://www.example.com:88/home?item=book`:

1. `http:`: This part of the URL is known as the **scheme**, which always comes before the colon and two forward slashes and tells the web client how to access the resource. In this case it tells the web client to use the Hypertext Transfer Protocol or HTTP to make a request. Other popular URL schemes include `ftp`, `mailto`, or `git`. 
2. `www.example.com`: This part is known as the **host**. It tells the client where the resource is hosted or located.
3. `:88`: This part is known as the **port** or **port number**. It is only required if you want to use a port other than the default. Unless a different port is specified, port `80` will be used by default in normal HTTP requests.
4. `/home/`: This part is known as the **path**. It shows what local resource is being requested. This part of the URL is optional.
5. `?item=book`: This part is known as the **query string**, which is made up of query parameters. It is used to send data to the server. This part of the URL is also optional. Because query strings are passed in through the URL, they are only used in HTTP GET requests.

---

#### What is URL encoding? And when might it be used?

URLs are designed to accept only certain characters in the standard 128-character ASCII character set. Reserved or unsafe ASCII characters which are not being used for their intended purpose, as well as characters not in this set, have to be encoded.  

URL encoding serves the purpose of replacing these non-conforming characters with a `%` symbol followed by two hexadecimal digits that represent the ASCII code of the character. Below are some popular encoded characters and example URLs.  

| Character | ASCII code | URL                                                          |
| :-------- | :--------- | :----------------------------------------------------------- |
| Space     | 20         | [http://www.thedesignshop.com/shops/tommy%20hilfiger.html](http://www.thedesignshop.com/shops/tommy hilfiger.html) |
| !         | 21         | [http://www.thedesignshop.com/moredesigns%21.html](http://www.thedesignshop.com/moredesigns!.html) |
| +         | 2B         | http://www.thedesignshop.com/shops/spencer%2B.html           |
| #         | 23         | http://www.thedesignshop.com/%23somequotes%23.html           |

Characters must be encoded if:

1. They have no corresponding character within the standard ASCII character set.
2. The use of the character is unsafe because it may be misinterpreted, or even possibly modified by some systems. For example `%` is unsafe because it can be used for encoding other characters. Other unsafe characters include spaces, quotation marks, the `#` character, `<` and `>`, `{` and `}`, `[` and `]`, and `~`, among others.
3. The character is reserved for special use within the URL scheme. Some characters are reserved for a special meaning; their presence in a URL serve a specific purpose. Characters such as `/`, `?`, `:`, `@`, and `&` are all reserved and must be encoded. For example `&` is reserved for use as a query string delimiter. `:` is also reserved to delimit host/port components and user/password.

---

### HTTP and the Request/Response Cycle

---

#### What are HTTP requests and responses? What are the components of each? 

##### HTTP Requests

Making an HTTP request is a simple as typing a URL address into a web browser's address bar. The server that hosts the website will handle the request and issue a response, which is then processed by the browser and translated into a human-friendly display.  

Sometimes a single HTTP request will initiate additional requests. The reason for that is that the response may contain code, such as HTML, that contains references to other resources. The browser processes those references and then issues new requests in order to retrieve those resources from the server. The browser makes separate requests for each resource referenced in the initial response.  

An HTTP Request consits of a _request line_, _headers_, and an optional _body_. The request line, or start line, consists of the HTTP method and the path. As of HTTP 1.0, the HTTP version also forms part of the request-line. The `Host` header is a required component since HTTP 1.1. Parameters, all other headers, and message body are optional.  

We can think of the HTTP request method as the verb that tells the server what action to perform on a resource. The two most common HTTP request methods are `GET` and `POST`.  

When you think about retrieving information, think `GET`, which is the most used HTTP request method. Such requests are initiated by clicking a link or via the address bar of a browser. The default behaviour of a link is to issue a `GET` request to a URL. `GET` requests are used to retrieve a resource. The response from a `GET` request can be anything, but if it's HTML and that HTML references other resources, your browser will automatically request those referenced resources.  

`POST` is an HTTP request method used when you want to initiate some action on the server, or send data to a server. Typically from within a browser, you use `POST` when submitting a form. `POST` requests allow us to send much larger and sensitive data to the server, such as images or videos. This data is sent via the body of the HTTP request. The body is optional, but it can contain HTML, images, audio, and so on.  

HTTP headers allow the client and server to send additional information during the request/response HTTP cycle. Headers are colon-separated name-value pairs that are sent in plain text. Below are some examples of typical request headers.  

| Field Name      | Description                                 | Example                                                      |
| :-------------- | :------------------------------------------ | :----------------------------------------------------------- |
| Host            | The domain name of the server.              | Host: [www.reddit.com](http://www.reddit.com/)               |
| Accept-Language | List of acceptable languages.               | Accept-Language: en-US,en;q=0.8                              |
| User-Agent      | A string that identifies the client.        | User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/38.0.2125.101 Safari/537.36 |
| Connection      | Type of connection the client would prefer. | Connection: keep-alive                                       |

To sum up, the most important components of an HTTP request are:

* HTTP method (i.e. `GET` or `POST`)
* path (i.e. URL path)
* headers
* message body (for `POST` requests)

##### HTTP Response

The raw data returned by a server after receiving an HTTP request is called an HTTP response. An HTTP response consits of a _status line_, optional _headers_, and an optional _body_.  

The status line consits of a three-digit status code and status text, which provides a description for the code. Response headers provide additional meta-information about the response data/resource being sent back. Below are some examples of reponse headers.  

| Header Name      | Description                             | Example                                |
| :--------------- | :-------------------------------------- | :------------------------------------- |
| Content-Encoding | The type of encoding used on the data.  | Content-Encoding: gzip                 |
| Server           | Name of the server.                     | Server:thin 1.5.0 codename Knife       |
| Location         | Notify client of new resource location. | Location: https://www.github.com/login |
| Content-Type     | The type of data the response contains. | Content-Type:text/html; charset=UTF-8  |

The server response to a `GET` request will be to send the client the information associated with the web page specified by the URL. `GET` requests should only retrieve content from the server and can generally be thought of as "read only" operations.  

The server response to a `POST` request will be to send a response that contains a reference location in the response header, which will then be automatically used by the client to issue another request for the webpage associated with the reference location. `POST` requests involve changing values that are stored on the server.  

Most HTML forms that submit their values to the server will use `POST`. Search forms are a noticeable exception to this rule: they often use `GET` since they are not changing any data on the server, only viewing it.  

To sum up, the most important components of an HTTP response are:

* Status line, including the status code (required)
* Headers (optional)
* Message body, which contains the raw response data (optional)

---

#### What is the HTTP request/response cycle?

HTTP is a _text-based_ protocol that operates at the Application Layer. HTTP _requests_ and _responses_ involve sending text between a _client_ and a _server_. A single HTTP message exchange consists of a request and a response that takes place between the client and the server.  

HTTP is concerned with the structuring of these messages that are being exchanged between applications. It's actually TCP/IP that is doing all the heavy lifting to ensure that the request/response cycle gets completed between your browser and the server.   

---

#### What are status codes? Provide examples of different status code types.

The _status code_ is a three-digit number that the server sends back after receiving a request signifying the status of the request. The _status text_ displayed next to the status code provides the description of the code.  

The most common response status code you'll encounter is **200**, which means the request was handled successfully. Other useful status codes are listed below.

| Status Code | Status Text           | Meaning                                                      |
| :---------- | :-------------------- | :----------------------------------------------------------- |
| 200         | OK                    | The request was handled successfully.                        |
| 302         | Found                 | The requested resource has changed temporarily. Usually results in a redirect to another URL. |
| 404         | Not Found             | The requested resource cannot be found.                      |
| 500         | Internal Server Error | The server has encountered a generic error.                  |

###### 302 Found

When a resource is moved the most common strategy is to re-route requests from the original URL to a new URL. The general term for this kind of re-routing is called a `redirect`. When your browser sees a response status code of 302, it knows that the resource has been moved, and will automatically follow the new-rerouted URL in the `Location` response header.  

Such redirects commonly happen when you are trying to access a resource that requires users to be logged in. If you're not already signed in, the browser will send you to a page to do that. After you enter your credentials, you'll be redirected to the original page you were trying to access.  

Unlike 4xx and 5xx response codes, 3xx codes don't indicate an error. Instead they are generally used in relation to redirection, and indicate to the client that it must take some additional action in order to complete the request.  

###### 404 Not Found

The server returns a `404` response status code when the requested resource cannot be found. Remember, a resource can be anything including audio files, CSS stylesheets, JavaScript files, images, etc.   

4xx level response codes indicate an error or issue on the client side, i.e. with the request. A `400` error is a general indication that there is a problem with the structure of the request; in other words the server did not understand the request due to its syntax. This is basically the server saying to the client 'I don't understand what you just asked me'.  

###### 500 Internal Server Error

A `500` status code says "there's something wrong on the server side". This is a generic error status code and the core problem can range from a mis-configured server setting to a misplaced comma in the application code. But whatever the problem, it's a server side issue. Someone with access to the server will have to debug and fix the problem.  

5xx level response codes indicate an error or issue on the server side. This time the request was valid, and the server was able to understand it, but it replies to the client that it cannot communicate using the version of HTTP that the client wants to use.  

---

#### What is meant by 'state' in the context of the web? What are some techniques that are used to simulate state?

In the context of the web, _state_ can be thought of as a concept describing the degree of data/informational continuity or persistence provided by a protocol once a connection has been established between a client and a server. With HTTP, each request–response cycle can be thought of as a particular moment punctuating the duration of any particular session. Because each request-response pair is completely independent of the previous one there is virtually no continuity. Thus, HTTP is said to be a _stateless_ protocol.  

Each request made to a resource is treated as a brand new entity, and different requests are not aware of each other. This statelessness is what makes HTTP and the internet so distributed and difficult to control, but it's also the same ephemeral attribute that makes it difficult for web developers to build stateful web applications.    

This means that the server does not need to hang on to information, or state, between requests. As a result, when a request breaks en route to the server, no part of the system has to do any cleanup. Both these reasons make HTTP a resilient protocol, as well as a difficult protocol for building stateful applications. Since HTTP, the protocol of the Internet, is inherently stateless, web developers have to work hard to simulate a stateful experience in web applications.  

An example of the problem posed by a stateless protocol like HTTP is imagine you navigate to Facebook's site, the first thing you expect to see is the login page. That was one complete request/response cycle. You then login--another request/response cycle. You then click on a picture--another request/response cycle--but you don't expect to be logged out after that action. If HTTP is stateless, how did the application maintain state and remember that you already input your username and password? How does Facebook even konw this request came from you, and how does it differentiate data from you vs. any other user? There are tricks web developers employ to make it seem like the application is stateful.  

##### Some Techniques for Simulating State

HTTP can be made to act as if it were maintaining a stateful connection with the server, even though it's not. One way to accomplish this is by having the server send some form of a unique token to the client. Whenever a client makes a request to that server, the client appends this token as part of the request, allowing the server to identify clients. In web development, we call this unique token that gets passed back and forth the session identifier. This mechanism of passing a session id back and forth between the client and server creates a sense of persistent connection between requests.  

This sort of faux statefulness has several consequences. First, every request must be inspected to see if it contains a session identifier. Second, if this request does, in fact, contain a session id, the server must check to ensure that this session id is still valid. The server needs to maintain some rules with regards to how to handle session expiration and also decide how to store its session data. Third, the server needs to retrieve the session data based on the session id. And finally, the server needs to recreate the application state (e.g., the HTML for a web request) from the session data and send it back to the client as the response.  

###### Cookies

One common way to store session information is by way of a browser cookie.  A cookie is a piece of data that's sent from the server and stored in the client during a request/response cycle. Cookies or HTTP cookies, are small files stored in the browser and contain the session information.  

When you access any website for the first time, the server sends session information and sets it in your browser cookie on your local computer. Note that the actual session data is stored on the server. The client side cookie is compared with the server-side session data on each request to identify the current session. This way, when you visit the same website again, your session will be recognized because of the stored cookie with its associated information.  

On the first visit to a new site, the response will likely contain a header called `set-cookie`. This header will add cookie data to the response. If we then make another request to this site we should see a `cookie` header, which contains the cookie data sent previously by the `set-cookie` response header. This piece of data will be sent to the server each time you make a request and uniquely identifies you--or more precisely, it identifies your client, which is your browser. The brow ser on your computer stores these cookies and if you were to close your browser and shut down your computer, the cookie information would still persist.  

The most important thing to understand is that the session id is stored on the client, and it is used as a "key" to the session data stored server side. That's how web applications work around the statelessness of HTTP.  

Some other important points:

* The session id is unique and expires in a relatively short amount of time, meaning you'll be required to login again after the session expires.
* If you manually remove the session id (they can be manually deleted), then you have essentially logged out.
* The session id is sent to the client in the _form_ of a cookie.

###### AJAX

AJAX is short for Asynchronous JavaScript and XML. Its main feature is that it allows browsers to issue requests and process responses without a full page refresh. For example, if you're logged into Facebook, the server has to generate the initial page you see, and the response is a pretty complex and expensive HTML page that your browser displays. The Facebook server has to add up all the likes and comments for every photo and status, and present it in a timeline for you. It's a very expensive page to re-generate for every request.  

When AJAX is used, all requests sent from the client are performed _asynchronously_, which just means that the page doesn't refresh. The main thing to remember is that AJAX requests are just like normal requests: they are sent to the server with all the normal components of an HTTP request, and the server handles them like any other request. The only difference is that instead of the browser refreshing and processing the response, the response is processed by a callback function, which is usually some client-side JavaScript code.

---

### Security

---

#### What are some security risks that can affect HTTP? What are some measures that can be used to mitigate against these risks?  

One of the major characteristics of HTTP is that it is a text-based protocol. By working with HTTP Requests and Responses, we've seen that they are transferred across the network in plain text. It's also essentially a fairly simple protocol, with quite a basic message structure and set of rules.  

While these characteristics makes it easier to design and build applications that interact with the protocol, the major downside is a lack of security. If an HTTP request or response is intercepted, the contents of that message can easily be read. It's also difficult to know if the source of an HTTP response is trustworthy, or if an HTTP message has been tampered with in transit.  

##### Security Risks

###### Session Hijacking

If a malicious hacker was attached to the same network as the client and server, the hacker could employ _packet sniffing_ techniques to read the messages being sent back and forth. As we learned previously, requests can contain the session id, which uniquely identifies you to the server, so if someone else compied this session id, they could craft a request to the server and pose as your client, therby automatically being logged in without even having access to your username or password.  

###### Cross-Site Scripting (XSS)  

XSS is a type of attack that happens when you allow users to input HTML or JavaScript that ends up being displayed by the site directly.  

If the server side code doesn't do any sanitization of input, the user input will be injected into the page contents, and _the browser will interpret the HTML and JavaScript and execute it_.  

Attackers can craft ingeniously malicious HTML and JavaScript and be very destructive to both the server as well as future visitors of this page. For example, an attacker can use JavaScript to grab the session ide of every future visitor of this site and then come back and assume their identity. It could happen silently without the victims ever knowing about it.  

Note that the malicious code would bypass the same-origin policy because the code lives on the site.   

##### Security Risk Mitigation  

###### Countermeasures for Session Hijacking

One popular way of solving session hijacking is by resetting sessions. With authentication systems, this means a successful login must render an old session id invalid and create a new one. With this in place, on the next request, the victim will be required to authenticate. At this point, the altered session id will change, and the attacker will not be able to have access.  

Another useful solution is by setting an expiration time on sessions. Sessions that do not expire give an attacker an infinte amount of time to pose as the real user. Expiring sessions, say 30 minutes, gives the attacker a far narrower window to access the app.  

Another approach is to use HTTPS across the entire app to minimize the chance that an attacker can get to the session id.  

###### Secure HTTP (HTTPS)  

With HTTPS, every request/response is encrypted before being transported on the network. This means if a malicious hacker sniffed out the HTTP traffic, the information would be encrypted and useless.  

HTTPS sends messages through a cryptographic protocol called Transport Layer Security (TLS) for encryption. Earlier versions of HTTPS used `SSL` or Secure Sockets Layer until `TLS` was developed. These cryptographic protocols use certificates to communicate with remote servers and exchange security keys before data encryption happens.  

###### Same-origin policy  

The same-origin policy is an important guard against session hijacking attacks and serves as a cornerstone of web application security.

The same-origin policy is an important concept that permits urestricted interaction between resources originating from the same origin, but restricts certain interactions between resources originating from different origins. What we mean by _origin_ here is the combination of a url's scheme, hostname, and port. So `http://mysite.com/doc1` would be considerd to have the same origin as `http://mysite.com/doc2`, but a different origin to `https://mysite.com/doc2` (different scheme), `http://mysite.com:4000/doc2` (different port), and `http://anothersite.com/doc2` (different host).  

Same-origin policy doesn't restrict _all_ cross-origin requests. Requests such as linking, redirects, or form submissions to different origins are typically allowed. Also typically allowed is the embedding of resources from other origins, such as scripts, css stylesheets, images and other media, fonts, and iframes. What _is_ typically restricted are cross-origin requests where resources are being accessed programatically using APIs such as `XMLHttpRequest` or `fetch` (the details of which are beyond the scope of this book).  

while secure, same-origin policy is an issue for web developers who have a legitimate need for making these restricted kinds of cross-origin requests. Cross-origin resource sharing or CORS was developed to deal with this issue. CORS is a mechanism that allows interactions that would normally be restricted cross-origin to take place. It works by adding new HTTP headers, which allow servers to serve resources cross-origin to certain specified origins.  

###### Potential Solutions for Cross-Site Scripting

One way to prevent XSS is by making sure to always sanitize user input. Eliminate problematic input, such as `<script>` tags, or disallowing HTML and JavaScript input altogether in favour of a safer format, like Markdown.  

The second way to guard against XSS is to escape all user input data when displaying it.  If you do need to allow users to input HTML and JavaScript, then when you print it out, make sure to escape it so that the browser does not interpret it as code.  

To escape a character means to replace an HTML character with a combination of ASCII characters, which tells the client to display that character as is, and to not process it; this helps prevent malicious code from running on a page. These combinations of ASCII characters are called HTML entities.  

---

#### What are the different services that TLS can provide? 

There are three important security services that are provided by the Transport Layer Security (TLS) protocol:

* **Encryption:** a process of encoding a message so that it can only be read by those with an authorized means of decoding the message.
* **Authentication:** a process to verify the identity of a particular party in the message exchange.
* **Integrity:** a process to detect whether a message has been interfered with or faked.

Each of these services are important in their own right, but when combined they provide for very secure message exchange over what is essentially an unsecure channel.  

##### TLS Encryption

The way in which TLS sets up an encrypted connection is via a process known as the TLS Handshake.  

To securely send messages via HTTP we want both the request _and_ the response to be encrypted in such a way that they can only be decrypted by the intended recipient. The most efficient way to do this is via symmetric key cryptography. But if we want to use symmetric keys, we also need a way to securely exchange the symmetric key.  

The clever thing about TLS is the way that it uses a combination of symmetric and assymetric cryptography. The bulk of the message exchange is conducted via symmetric key encryption, but the initial symmertic key exchange is conducted using assymetric key encryption (also known as public key encryption). In the assymetric system the keys in the pair are non-identical: the public key is used to encrypt and the private key to decrypt.  

TLS assumes TCP is being used at the Transport layer, and the TLS Handshake takes place after the TCP Handshake. A step-by-step description of the TLS Handshake process might look something like this:  

1. The TLS Handshake begins with a `ClientHello` message which is sent immediately after the TCP `ACK`. Among other things, this message contains the maximum version of the TLS protocol that the client can support, and a list of Cipher Suites that the client is able to use. (Note: a cipher is a cryptographic algorithm, sets of steps for performing encryption, decryption, or other related tasks; a cipher suite is a suite, or set, of ciphers).
2. On receiving the `ClientHello` message, the server responds with a message of its own. This message includes a `ServerHello`, which sets the protocol version and Cipher Suite, as well as other related information. As part of this message the server also sends its certificate (which contains its public key), and a `ServerHelloDone` marker which indicates to the client that it has finished with this step of the handshake.  
3. Once the client has received the `ServerHelloDone` marker, it will initiate the key exchange process. It's this key exchange process that ultimately enables both the client and server to securely obtain a copy of the symmetric encryption key that will be used for the bulk of the secure message transfer between the two parties. An example of how this key-exchange process might work, using the RSA algorithm, is:
   * The client generates what's known as a 'pre-master secret', encrypts it using the server's public key, and sends it to the server.  
   * The server will receive the encrypted 'pre-master secret' and decrypt it using its private key.
   * Both client and server will use the 'pre-master' secret, along with some other pre-agreed parameters, to generate the same symmetric key.  
   * As part of the communication which includes the `ClientKeyExchange` message (e.g. the pre-master secret), the client also sends a `ChangeCipherSpec` flag, which tells the server that encrypted communications should now start using the symmetric keys. Additionally, this communication includes a `Finished` flag to indicate that the client is now done with the TLS Handshake.  
4. The server also sends a message with `ChangeCipherSpec` and `Finished` flags. The client and server can now begin secure communication using the symmetric key.  

The key points to remember about the TLS Handshake process is that it is used to:

* Agree which version of TLS to be used in establishing a secure connection.  
* Agree on the various algorithms that will be included in the cipher suite.
* Enable the exchange of symmetric keys that will be used for message encryption.

One should also be aware that the TLS handshake can add up to two round-trips of latency (depending on the TLS version) to the establishment of a connection between client and server prior to the point where any application data can be sent. This is on top of the initial round trip of latency resulting from the TCP Handshake.  

Note: there is a protocol called Datagram Transport Layer Security (DTLS) for use with network connections that use UDP rather than TCP at the Transport Layer.  

##### TLS Authentication  

Being able to transfer data in an encrypted form is all well and good, but we also need a way of identifying the other party in our message exchange.  

During the TLS Handshake, as part of its response to the `ClientHello` message, the server provides its certificate. As outlined in the Encryption section, part of the function of this certificate is so that the client can use the Public Key contained within it during the key exchange process. Another function of this certificate is to provide a means of identification for the party providing it.  

The certificate will contain various pieces of information, including who the owner is. The certificate on its own isn't much proof of anything, however. Since such certificates are publicly available to anyone, a malicious third-party could easily access one and present it as its own. The certificate, and the Public Key it contains, are only one part of an overall system of authentication.  

The exact way that the Public Key is used during this process varies depending on the Authentication algorithm selected as part of the Cipher Suite. Generally, however, this process will be something along the following lines:  

* The server sends its certificate, which includes its public key.
* The server creates a 'signature' in the form of some data encrypted with the server's private key.
* The signature is transmitted in a message along with the original data from which the signature was created.
* On receipt of the message, the client decrypts the signature using the server's public key and compares the decrypted data to the original version.
* If the two versions match then the encrypted version could only have been created by a party in possession of the private key.  

Following a process such as this we can identify that the server which provided the certificate during the initial part of the TLS Handshake as being in possession of the private key, and therefore the actual owner of the certificate.  

However, just as it's possible to create a fake ID card in the real world, it's possible to create a fake digital certificate. How are we to know if a certificate is genuine or not?  This is where Certificate Authorities come in.  

###### Certificate Authorities

If you are presented with a piece of identification, you are much more likely to accept it as genuine if it has been issued by a trustworthy source. When it comes to digital certificates, the trustworthy sources are called Certificate Authorities (CAs).  

When a CA issues a certificate, it does a couple of important things:  

1. **Verifies that the party requesting the certificate is who they say they are.**  The way that this is done is up to the CA and will depend to an extent on the type of certificate being issued. In the case of a domain validated server certificate, for example, it can involve proving that you own the domain by uploading a specific file to a server that is accessible by the domain for which the certificate is being issued.  
2. **Digitially signs the certificate being issued.** This is often done by encrypting some data with the CA's own private key and using this encrypted data as a 'signature'. The unencrypted version of the data is also added to the certificate. In order to verify that the certificate was issued by the CA, the signature can be decrypted using the CA's public key and checked for a match against the unencrypted version.  

So who exactly are these Certificate Authorities, and why should we trust them? There are different 'levels' of CA. An 'Intermediate CA' can be any company or body authorised by a 'Root CA' to issue certificates on its behalf.  

###### The Chain of Trust  

Root CAs issue Root Certificates, which are 'self-signed' and are essentially the end-point of the chain of trust.  

Client software, such as browsers, store a list of these authorities along with their Root Certificates (which includes their public key). When receiving a certificate for checking, the browser can go up the chain to the Root Certificate stored in its list.  

The purpose of this chain-like structure is the level of security it provides. The private keys of the Root CAs are kept behind many layers of security in order to be kept as inaccessible as possible. As such they don't issue end-user certificates, but leave that up to the Intermediate CAs. Additionally, if the private key of an Intermediate CA somehow became compromised, the root CA can revoke the certificate for the Intermediate CA, therefore invalidating all of the certificates down the chain from it, and simply issue a new one.  

It is necessary that such a 'chain of trust' would need to have an end-point, but if no-one is authenticating the Root CAs other than themselves, how do we know we can trust them? The answer to this is simply their reputation gained through prominence and longevity. Root CAs are essentially a small group of organisations approved by browser and operating system vendors.  

Points to remember:

* Certificates are signed by a Certificate Authority, and work on the basis of a Chain of Trust, whic leads to one of a small group of highly trusted Root CAs.  
* Certificates are exchanged during the TLS Handshake process.  

##### TLS Integrity  

TLS Integrity provides a means of checking whether a message has been altered or interfered with in transit.  It adds an additional layer of security by providing functionatlity to check the integrity of data transported via the protocol.  

To get a clearer picture of how this functionality works, we need to take a step back and look at how the TLS protocol encapsulates data.  

###### TLS Encapsulation  

The OSI model defines TLS as a Session layer protocol, and so existing in between Application layer (where HTTP resides) and the Transport Layer (where TCP resides). Although, as previously stated, we're not too interested in the specifics of how the OSI Model defines these intervening layers, when thinking about TLS it can be useful to think of it as operating between HTTP and TCP.  

Just like other protocols we've looked at in this course, TLS sends messages in a certain format. This format can vary depending on the particular function that TLS is performing, but when it is transporting application data TLS encapsulates that data in the same way that we've seen with other PDUs. In other words, the data to be transported forms a payload, and meta data is attached in the form of header and trailer fields.  

The main fields that interests us in terms of providing message integrity is the `MAC` field.  

###### Message Authentication Code (MAC)  

The `MAC` field is similar in concept to the checksum fields we've already seen in other PDUs, although there is a difference in implementation as well as overall intention. The checksum field in, say, a TCP Segment is intended for error detection (i.e. to test if some data was corrupted during transport). The intention of the `MAC` field in a TLS record is to add a layer of security by providing a means of checking that the message hasn't been altered or tampered with in transit.  

The way this is implemented is through the use of a hasing algorithm. It works something like this:  

1. The sender will create what's called a _digest_ of the data payload. This is effectively a small amount of data derived from the actual data that will be sent in the message. The digest is created using a specific hashing algorithm combined with a pre-agreed hash value. This hashing algorithm to be used and hash value will have been agreed as part of the TLS Handshake process when the Cipher Suite is negotiated.  
2. The sender will then encrypt the data payload using the symmetric key (as described earlier in the Encryption section), encapsulate it into a TLS record, and pass this record down to the Transport Layer to be sent to the other party.  
3. Upon receipt of the message, the receiver will decrypt the data payload using the symmetric key. The receiver will then also create a digest of the payload using the same algorithm and hash value. If the two digests match, this confirms the integrity of the message.  



