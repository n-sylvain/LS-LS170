##### LS171 Assessment: Networking Foundations

---

# Study Guide

## The Internet

##### Have a broad understanding of what the internet is and how it works

* The internet is made up of an incredibly large number of independently operated networks.
* **The internet is fully distributed: there's no central control that is deciding how packets are routed or where pieces of the network are built, or even who interconnects with whom.** These are all business decisions that are made independently by the operators. They are all motivated to assure that there is end-to-end connectivity of every part of the network because the utility of the net is that any device can communicate with any other device; just like you want to be able to make phone calls to any other telephone in the world.
* Broadly, **the internet is a network of networks.**
* At its most basic, a network is comprised of at least two devices connected in such a way that they can communicate or exchange data.
* **A Local Area Network (LAN) is essentially a network of computers all connected to a network bridging device, such as a hub or, more likely, a switch. The computers are all connected to this device via network cables and this forms the network.**
* **The internet can be imagined as a vast number of these networks connected together. In between all the sub-networks are systems of routers that direct the network traffic.**

###### Protocols for Network Communication can be Organized Into a Layered Model

* **Two of the most popular models are the Open Systems Interconnection (OSI) model and the Internet Protocol Suite (also known as the TCP/IP or DoD model).** There is some rough equivalency, albeit with some overlap, between the layers of the two models.
* The top layer of the Internet Protocol Suite (Application) mostly maps to the top three layers of the OSI Model (Application, Presentation, Session).
* The second layer of the Internet Protocol Suite (Transport) mostly maps to the fourth layer of the OSI model (Transport).
* The third layer of the Internet Protocol Suite (Internet) mostly maps to the fifth layer of the OSI model (Network).
* The fourth layer of the Internet Protocol Suite (Link) mostly maps to the bottom two layers of the OSI model (Data Link and Physical).

**The OSI Model:**

![seven-layers-of-OSI-model](/Users/matthewjohnston/Desktop/To Print/seven-layers-of-OSI-model.png)

**Internet Protocol Suite Model:**

![internet_protocol_suite_model](/Users/matthewjohnston/Desktop/To Print/internet_protocol_suite_model.jpg)

**Both Models Together:**

![osi_tcpip_models](/Users/matthewjohnston/Desktop/To Print/osi_tcpip_models.gif)

**Video Links:**

* [Each layer of the OSI model and TCP/IP explained.](https://www.youtube.com/watch?v=kCuyS7ihr_E)
* [OSI and TCP IP Models - Best Explanation](https://www.youtube.com/watch?v=3b_TAYtzuho&t=2s)

###### Protocol Data Units (PDUs)

* **Each layer encapsulates data within a data unit of the layer below, thus hiding that data from other layers.**
* **Data is encapsulated into a PDU, creating separation between protocols operating at different layers.**
* **A PDU is an amount or block of data transferred over a network. Different protocols or protocol layers refer to PDUs by different names. At the Link/Data Link layer, for example, a PDU is known as a _frame_. At the Internent/Network layer it is known as a _packet_. At the Transport layer, it is known as a _segment_ (TCP) or _datagram_ (UDP).**
* In all cases, the basic concept is effectively the same; **the PDU consists of a header, a data payload, and in some cases a trailer or footer.**
* Header and Trailer:
  * The exact structure of the header and, if included, trailer varies from protocol to protocol, but the purpose of them is the same in each case: to provide protocol-specific metadata about the PDU. For example, an Internet Protocol (IP) packet header would include fields for the Source IP Address and the Destination IP Address, which would be used to correctly route the packet.
  * **The purpose of the header/trailer is to provide protocol-specific metadata about the PDU.**
* Data Payload:
  * **The data payload portion of a PDU is simply the data that we want to transport over the network using a specific protocol at a particular network layer.**
  * **The data payload is the key to the way encapsulation is implemented. The entire PDU from a protocol at one layer is set as the data payload for a protocol at the layer below.** For example, a HTTP Request at the Application layer could be set as the payload for a TCP segment at the transport layer.
  * **The major benefit of this approach is the separation it creates between the protocols at different layers. This means that a protocol at one layer doesn't need to know anything about how a protocol at another layer is implemented in order for those protocols to interact. It creates a system whereby a lower layer effectively provides a 'service' to the layer above it.** In other words, a TCP segment isn't really concerned whether its data payload is an HTTP request, an SMTP command, or some other sort of Application layer data. It just knows it needs to encapsulate _some data_ from the layer above and provide the result of this encapsulation to the layer below.

##### Understand the characteristics of the physical network, such as latency and bandwidth

* At the most basic level, or layer, we have a 'physical' network made of tangible pieces such as networked devices, cables, and wires. Even the radio waves used in wireless networks, though we can't touch or see them, exist in the physical realm and are bound by the physical laws and rules.
* These laws and rules determine how data actually gets transported from one place to another in a physical sense. What happens at this level involves real-world limitations and boundaries, such as how fast an electrical signal or light can travel, or the distance a radio wave can reach. These limitations determine the physical characteristics of a network, and these characteristics have an impact on how protocols function further up at the conceptual level. 
* **A network at the physical level can be thought of as lots of devices connected by cables, transmitting binary data in the form of electrical signals, light, or radio waves.**

###### Bits and Signals

* **At the Physical Layer of the OSI model, we are essentially concerned with the transfer of bits (binary data). In order to be transported, these bits are converted into signals. Depending on the transportation medium used, bits are converted to electrical signals, light signals, or radio waves.**

###### Characteristics of a Physical Network

* **The two main characteristics of the performance of a physical network are Latency and Bandwidth.**
* **In simple terms, latency is a measure of the _time_ it takes for some data to get from one point in a network to another point in a network.**
* **Bandwidth is the _amount_ of data that can be sent at once.**

###### The Elements of Latency

* **Latency is a measure of delay. Data starts at one location at a certain point in time. At a later point in time, it reaches another location. The difference between those two points in time is the delay.** There are actually different types of delay that go together to determine the overall latency of a network connection.
* **Propagation delay:** this is the amount of time it takes for a message to travel from the sender to the receiver, and can be calculated as the ratio between distance and speed.
* **Transmission delay:** the journey of data from point A to point B on a network typically won't be made over one single cable. Instead, the data will travel across many different wires and cables that are all inter-connected by switches, routers, and other network devices. Each of these elements within the network can be thought of as an individual 'link' within the overall system. Transmission delay is the amount of time it takes to push the data onto the link.
* **Processing delay:**  Data travelling across the physical network doesn't directly cross from one link to another, but is processed in various ways.
* **Queuing delay:** Network devices such as routers can only process a certain amount of data at one time. If there is more data than the device can handle, then it queues, or _buffers_, the data. The amount of time the data is waiting in the queue to be processed is the queuing delay.
* **The total latency between two points, such as a client and a server, is the sum of all the delays above. This value is usually given in milliseconds (_ms_).**
* **Last-mile latency**: **a lot of the delays described above can take place within the parts of the network which are closest to the end points.** This is often referred to as 'last-mile latency' and relates to the delays involved in getting the network signal from your ISP's network to your home or office network. **The 'hops' within the core part of the network are longer with less interruptions for transmission, processing, and queuing. At the network edge, there are more frequent and shorter hops as the data is directed down the network hierarchy to the appropriate sub-network. You can think of the network edge as the 'entry point' into a network like a home or corporate LAN.**

###### Bandwidth

* Bandwidth varies across the network, and isn't going to be at a constant level between the start point and the end point of our data's journey. For example, the capacity of the core network is going to be much higher than the part of the network infrastructure that ultimately connects to your home or office building. The bandwidth that a connection receives is the lowest amount at a particular point in the overall connection. A point at which bandwidth changes from relatively high to relatively low is generally referred to as a bandwidth bottleneck.

##### Have a basic understanding of how lower level protocols operate

* Protocols are systems of rules.
* **In terms of computer networks, protocols are sets of rules governing the exchange or transmission of data.**
* **There are two main reasons for the existence of different protocols: 1) different protocols were developed to address different aspects of network communication; and 2) different protocols were developed to address the same aspect of network communication, but in a different way or for a specific use-case.**

###### Different Protocols for Different Aspects of Communication

* Syntactic rules that govern the structure of messages.
* Protocols at one layer provide services to the layer above.
* Flow and order of the messages.
* In human communication we have grammatical rules governing speech and writing, we tend to follow certain conventions when speaking, such as allowing one person to speak at a time.
* **TCP and HTTP would be examples of two protocols that address different aspects of communication; TCP the transfer of messages beetween applications, and HTTP the structure of those messages.**

###### Different Protocols for the Same Aspect of Communication

* Certain specific contexts may require a different protocol.
* In human communication, we have different contexts with different protocols, such as a protocol for a conversation between two friends versus a protocol for a speaker at a conference. These contexts are still concerned with using proper syntax and following the flow and order of message transfer, but follow slightly different rules, or protocols.
* **TCP and UDP would be examples of two protocls that address the same basic aspect of communication, the transfer of messages between applications, but do so in different ways.** 

###### The Link/Data Link Layer

* One of the most important rules for transferring data from one place to another is identifying the device to which we want to send that data. **The protocols operating at this layer are primarily concerned with the identification of devices on the physical network and moving data over the physical network between the devices that comprise it, such as hosts (e.g. computers), switches, and routers.**

* Within the OSI model, the Data Link layer is Layer 2 and comes in between the Physical layer (1) and the Network layer (3). Within the Internet Protocol Suite, the Link layer is layer 1, since this model doesn't define a specific layer for the physical network. **Within both of these models though, we can think of what happens at this layer as an interface between the workings of the physical network and the more logical layers above.**

* **The most commonly used protocol at this layer is the Ethernet protocol.** You may have heard of Ethernet cables. These are network cables used to connect devices on the network such as computers, switches, and routers.

* Two of the most important aspects of Ethernet are **framing** and **addressing**.

* ###### Ethernet Frames:

  * **Ethernet Frames are a PDU, and encapsulate data from the Internet/Network layer above. The Link/Data Link layer is the lowest layer at which encapsulation takes place. At the physical layer, the data is essentially a stream of bits in one form or another without any logical structure. An Ethernet Frame adds logical structure to this binary data. The data in the frame is still in the form of bits, but the structure defines which bits are actually the data payload, and which are metadata to be used in the process of transporting the frame.**
  * **Source and Destination MAC address of the Frame: the source address is the address of the device which created the frame (as we'll see later on in this assignment, this can change at various points along the data's journey). The destination MAC address is the address of the device for which the data is ultimately intended. MAC addresses are a key part of the Ethernet protocol.** 
  * **Data Payload of the Frame:** the data payload field can be between 42 and 1497 bytes in length. **It contains the data for the entire PDU from the layer above, an IP Packet for example.**

* ###### MAC Addresses:

  * **Every network-enabled device, e.g. a Network Interface Card (NIC) that you would find in a PC or laptop, is assigned a unique MAC Address when it is manufactured. Since this address is linked to the specific physical device, and (usually) doesn't change, it is sometimes referred to as the _physical address_ or _burned-in address_.** MAC Addresses are formatted as a sequence of six two-digit hexadecimal numbers, e.g. `00:40:96:9d:68:0a`, with different ranges of addresses being assigned to different network hardware manufacturers.

  * In a hub scenario, each receiving device would check its MAC Address against the Destination MAC Address in the Frame to check if it was the intended recipient. If it wasn't, then it would just ignore the frame.

  * Sending every frame to every device on the network isn't very efficient, especially for large networks. These days it is rare that you'll find a network that uses a hub; most modern networks instead use switches. Like a hub, a switch is a piece of hardware to which you connect devices to create a network. Unlike a hub however, a switch uses the destination address in order to direct a frame *only* to the device for which it is intended.

  * **A switch directs the frames to the correct device by keeping and updating a record of the MAC addresses of the devices connected to it, and associating each address with the Ethernet port to which the device is connected on the switch.** It keeps this data in a MAC Address Table, a simple representation of which might look something like this:

  * | Switch Port | MAC Address       |
    | :---------- | :---------------- |
    | 1           | 00:40:96:9d:68:0a |
    | 2           | 00:A0:C9:14:C8:29 |
    | 3           | D8:D3:85:EB:12:E3 |
    | 4           | 00:1B:44:11:3A:B7 |

    **The MAC Addressing system works well for local networks, where all the devices are connected to a switch that can keep a record of each device's address. In theory, we could conduct inter-network communication just using MAC addresses.** For example, we could design routers that kept records of which MAC Addresses could be accessed via other routers on the wider network. **In practice however, there's an issue that prevents us from doing this: scale. This approach isn't scalable due to certain characteristics of MAC addresses:**

    - **They are physical rather than logical. Each MAC Address is tied (burned in) to a specific physical device**
    - **They are flat rather than hierarchical. The entire address is a single sequence of values and can't be broken down into sub-divisions.**

    Imagine your laptop is connected to a local network in New York. You then take that laptop to Tokyo and plug it into a local network there. In both locations, the physical MAC address would be the same. Keeping track of which MAC Addresses were part of which local networks would be an impossible task. Even if we were able to do this, the fact that the addresses are non-hierarchical means that routing devices would need a record of each single address that existed somewhere in the world; that would mean storing impossibly large tables.

    If we want to solve these problems, we need a different system of rules that doesn't have these limitations and that can scale in such a way that we can build a network of networks which spans the entire globe. The Internet Protocol provides just such a set of rules.
    
  * Helpful Videos:
  
    * [Routers, Switches, Packets and Frames](https://www.youtube.com/watch?v=zhlMLRNY5-4&t=481s)
    * 

###### The Internet/Network Layer

* In the OSI model the Network layer is layer 3 (between the Data Link and Transport layers). In the Internet Protocol Suite, the Internet layer is layer 2 (between the Link layer and the Transport layer). Within both models, **the primary function of protocols at this layer is to facilitate communication between hosts (e.g. computers) on different networks.**

* The Internet Protocol (IP) is the predominant protocol used at this layer for inter-network communication. There are two versions of IP currently in use: IPv4 and IPv6. For a general overview of how IP works, we'll mostly be looking at IPv4. Although there are differences between the versions, **the primary features of both versions are the same:**

  * **Routing capability via IP addressing**
  * **Encapsulation of data into packets**

* ###### Data Packets

  * **The Protocol Data Unit (PDU) within the IP Protocol is referred to as a _packet_. A packet is comprised of a Data Payload and a Header. Just as with Ethernet Frames, the Data Payload of an IP Packet is the PDU from the layer above (the Transport layer). It will generally be a TCP segment or a UDP datagram. The Header is split into logical fields which provide metadata used in transporting the packet. Again, as with Ethernet Frames, the data in the IP Packet is in bits. The logical separation of those bits into header fields and payload is determined by the set size of each field in bits and the order within the packet.**

* ###### IP Addresses (IPv4) (see next section)

* **Whereas the Ethernet protocol provides communication between devices on the same local network, the Internet Protocol enables communication between two networked devices anywhere in the world. We can send a message from one device on the internet and it can reach another device on the internet.**

###### The Transport Layer

* **An important thing to understand about the Internet Protocol, and its system of addressing, is that it is intended to provide communication between *hosts*, or devices. These hosts can potentially be on the same local network, or on different local networks halfway around the world from each other. Either way, we can use IP to get a message from one host to the other, but not any more than that.**

* **As we know though, there are potentially many applications running on a single host. If IP can get us as far as the host, how do we provide communication between an application running on one host and an application running on another host (or potentially between two different applications or processes running on the same host)?**

* ###### Multiplexing and Demultiplexing

  * As we've established, there might be many networked applications or processes running on a device at one time. These applications all want to be able to send and receive data simultaneously. For example, you might want to send an email while listening to Spotify or load a web page in your browser while chatting in Slack. We can perhaps think of these different applications or processes as **distinct *channels*** for communication on a host machine.
  * If you recall in the previous lesson when we discussed IP packets, **the source and destination IP addresses are contained in the packet header and can be used to identify the host machines. This effectively creates a communication channel between hosts.** So, although we have multiple communication channels *on* a host, with IP addresses we only have a single channel *between* hosts. **What we need is a way to transmit these multiple data inputs over this single host-to-host channel and then somehow separate them out at the other end.**
  * **In the context of a communication network, this idea of transmitting multiple signals over a single channel is known as *multiplexing*, with *demultiplexing* being the reverse process.** It is a general concept that can be applied in lots of contexts within communications networks; for example at the physical level we can think of optical fibres carrying multiple light signals at different angles of refraction, or radio waves carrying signals at different frequencies. Our focus in this assignment is the application of this concept at the Transport layer of our network communication model. This takes place through the use of **network ports**.
  * **We can use ports to identify specific services running on host machines, but how does that help us with multiplexing and demultiplexing? The answer is that the source and destination port numbers are included in the Protocol Data Units (PDU) for the transport layer. The name, and exact structure, of these PDUs varies according to the Transport Protocol used, but what they have in common is that they include these two pieces of information.**
  * **Data from the application layer is encapsulated as the data payload in this PDU, and the source and destination port numbers within the PDU can be used to direct that data to specific processes on a host. The entire PDU is then encapsulated as the data payload in an IP packet. The IP addresses in the packet header can be used to direct data from one host to another. The IP address and the port number *together* are what enables end-to-end communication between specific applications on different machines. The combination of IP address and port number information can be thought of as defining a *communication end-point*. This communication end-point is generally referred to as a *socket*. We'll talk more about sockets later, but for now you can just think of them as the combination of IP address and port number, for example `216.3.128.12:8080`.**
  * This concept can be a little bit tricky to grasp at first, so it might help to compare it with a concept most of you should be familiar with: the postal service. Imagine an apartment building. It has numerous apartments, but the building itself has a single street address. The postal worker delivers a bunch of mail to the building. The concierge of the building then sorts the mail and posts the individual letters to the appropriate mailbox in the foyer, each mailbox being identified by a specific apartment number.
  * In this context we can think of the street address of the apartment building address as the IP address and the individual apartment numbers as port numbers. Furthermore, the postal service can be thought of as the Internet Protocol, and the building concierge as a Transport layer protocol (e.g. TCP or UDP).
  * To allow for many processes within a single Host to use TCP communication facilities simultaneously, the TCP provides a set of addresses or ports within each host. Concatenated with the network and host addresses from the internet communication layer, this forms a socket.
  * ***Multiplexing* and *demultiplexing* provide for the transmission of multiple signals over a single channel**
  * **Multiplexing is enabled through the use of *network ports***

* ###### Connectionless vs. Connection-Oriented System

  * In a **connectionless system** we could have one socket object defined by the IP address of the host machine and the port assigned to a particular process running on that machine. That object could call a `listen()` method which would allow it to wait for incoming messages directed to that particular IP/port pair. **Such messages could potentially come from any source, at any time, and in any order, but that isn't a concern in a connectionless system -- it would simply process any incoming messages as they arrived and send any responses as necessary.**
  * A **connection-oriented system** would work differently. You could have a socket object defined by the host IP and process port, just as in the connectionless system, also using a `listen()` method to wait for incoming messages; the difference in implementation would be in what happens when a message arrives. **At this point we could instantiate a *new* socket object; this new socket object wouldn't just be defined by the local IP and port number, but also by the IP and port of the process/host which sent the message. This new socket object would then listen specifically for messages where all four pieces of information matched (source port, source IP, destination port, destination IP). The combination of these four pieces of information are commonly referred to as a four-tuple.**
  * **Any messages not matching this four-tuple would still be picked up by the original socket, which would then instantiate another socket object for the new connection.**
  * Implementing communication in this way effectively creates a dedicated virtual connection for communication between a specific process running on one host and a specific process running on another host. **The advantage of having a dedicated connection like this is that it more easily allows you to put in place rules for managing the communication such as the order of messages, acknowledgements that messages had been received, retransmission of messages that weren't received, and so on. The purpose of these types of additional communication rules is to add more reliability to the communication.**

###### The Application Layer

* Both the TCP/IP model and the OSI model define an Application layer as the topmost layer in their respective layered systems. **Something to be clear about here is that the application layer is not the *application itself*, but rather a set of protocols which provide communication services to applications.**
* One thing both models have in common however is that the protocols which exist at the Application layer are the ones with which the application most directly interacts. That's not to say that networked applications are limited to interacting with only Application layer protocols. You can see many applications interacting with Transport layer protocols by, for example, opening a TCP socket. However, it is much less common to build applications which interact directly with protocols below the Transport layer.
* Earlier in the course we discussed how using a layered model allows you to focus on different aspects of communication occurring at different layers. The protocols we've looked at within other layers, in both the OSI and TCP/IP models, have mainly been concerned with managing the establishment and flow of communications; in other words, the rules around how messages get from one point to another. **Application layer protocols rely on the protocols at the layers below them to ensure that a message gets to where it is supposed to, and focus instead on the structure of that message and the data that it should contain.**
* **We can perhaps think of Application layer protocols as being the rules for how applications talk to each other at a syntactical level. Different types of applications have different requirements with regards to how they communicate at a syntactical level, and so as a result there are many different protocols which exist at the application layer.** For example, the rules for how an email client communicates with an email server will be different from the rules for how a web browser communicates with a web server, because emails and web pages are fundamentally different things serving different purposes.



##### Know what an IP address is and what a port number is

* ###### IP Addresses (IPv4)

  * **Unlike MAC Addresses, IP Addresses are logical in nature. This means that they are not tied to a specific device, but can be assigned as required to devices as they join a network. The IP address that the device is assigned must fall within a range of addresses available to the local network that the device is connected to. This range is defined by a network hierarchy, where an overall network is split into logical subnetworks, with each defined by the range of IP addresses available to it.**
  * IPv4 addresses are 32 bits in length and are divided into four sections of eight bits each. When converted from binary to decimal, each of those sections provides a range of numbers between `0` and `255` (since 2 to the power of 8 equals 256). For example `109.156.106.57`.
  * A basic example of this hierarchy in action would be if all the addresses in the range `109.156.106.0` to `109.156.106.255` were assigned to a **single local network.** Each network defines the address at the start of the range, e.g. `109.156.106.0`, as the **network address**, and the address at the end of the range, e.g. `109.156.106.255`, as the **broadcast address**. Addresses between the network and broadcast address, `109.156.106.1` to `109.156.106.254`, can be allocated to individual devices on the network.
  * **We won't go into what broadcast address is used for, but the network address of the range is used to identify a specific network segment. What this means is that a router that wants to forward an IP packet to any address in the entire range only needs to keep a record of which router on the network controls access to the segment with that network address. This logic is what creates the hierarchical structure, and means that routers don't need to keep records of every single device within an addressable range.**

* ###### Routing and Routing Tables

  * **All routers on the network store a local routing table. When an IP packet is received by a router, the router examines the destination IP address and matches it against a list of network addresses in its routing table.** As explained above, these network addresses define a range of addresses within a particular subnet. **The matching network address will determine where in the network hierarchy the subnet exists. This will then be used to select the best route for the IP packet to travel.**

* ###### Ports

  * **In simple terms a port is an identifier for a specific process running on a host.** This identifier is an integer in the range 0-65535. Sections of this range are reserved for specific purposes:
    * 0-1023 are well-known ports. These are assigned to processes that provide commonly used network services. For example HTTP is port 80, FTP is port 20 and 21, SMTP is port 25, and so on.
    * 1024-49151 are registered ports. They are assigned as requested by private entities. For example, companies such as Microsoft, IBM, and Cisco have ports assigned that they use to provide specific services. On some operating systems, ports in this range are also used for allocation as *ephemeral ports* on the client side.
    * 49152-65535 are dynamic ports (sometimes known as private ports). Ports in this range cannot be registered for a specific use. They can be used for customized services or for allocation as *ephemeral ports*.
  * **Services running on servers will likely have a port in the well-known range assigned to them. If you want to connect via HTTP to a web-server running on a host machine, that web-server process will likely have port 80 assigned to it. This is sometimes described as the web server *listening* on port 80.** We'll look in a bit more detail at what that means later on.
  * **A service running on a client machine, for example in a browser running on your laptop, won't use one of these well-known ports, but instead have an *ephemeral* or temporary port assigned to it by the operating system, for example 59258.**
  * **So we can use ports to identify specific services running on host machines, but how does that help us with multiplexing and demultiplexing? The answer is that the source and destination port numbers are included in the Protocol Data Units (PDU) for the transport layer.** The name, and exact structure, of these PDUs varies according to the Transport Protocol used, but what they have in common is that they include these two pieces of information.
  * **Network sockets can be thought of as a *combination of IP address and port number***

##### Have an understanding of how DNS works

* ###### How the Internet Works

  * The Internet consists of millions of interconnected networks that allow all sorts of computers and devices to communicate with each other. By convention, all devices that participate in a network are provided unique labels. The general term for this type of label is an Internet Protocol Address or **IP Address** and is similar to a computer's phone number on the Internet. **Port numbers** add more detail about how to communicate (think of company phone extensions). IP Addresses are represented as: `192.168.0.1`
  * When a port number is needed, the address is specified as: `192.168.0.1:1234`
  * where the IP Address is `192.168.0.1` and the port number is `1234`. An IP Address acts as the identifier for a device or server, and can contain hundreds or thousands of ports, each used for a different communication purpose to that device or server.
  * When it comes to the wider Internet, effective communication begins when each device has a public IP address provided by an [Internet Service Provider](http://en.wikipedia.org/wiki/Internet_service_provider). But what about an address like [http://www.google.com](http://www.google.com/)? How does your computer know what IP address it's mapped to? When we wish to connect to Google's main page, we do not type in the IP Address, we type in its URL.

* ###### Domain Name System (DNS)

  * **The *Domain Name System* (DNS) is a distributed database which *translates a domain name* such as `google.com` *to an IP Address* such as `216.58.213.14`.**
  * **This mapping from URL to IP address is handled by the Domain Name System or DNS. DNS is a distributed database which translates computer names like [http://www.google.com](http://www.google.com/) to an IP address and maps the request to a remote server.** Stated differently, it keeps track of URLs and their corresponding IP addresses on the Internet. So an address like [http://www.google.com](http://www.google.com/) might be resolved to an IP address `197.251.230.45`. By the way, you can also get to Google's main page by typing the IP address into your browser's address bar.
  * However, most people want to use a user-friendly address like [http://www.google.com](http://www.google.com/), instead of memorizing a number of digits. **DNS databases are stored on computers called DNS servers. It is important to know that there is a very large world-wide network of hierarchically organized DNS servers, and no single DNS server contains the complete database. If a DNS server does not contain a requested domain name, the DNS server routes the request to another DNS server up the hierarchy. Eventually, the address will be found in the DNS database on a particular DNS server, and the corresponding IP address will be used to receive the request.**
  * Your typical interaction with the Internet starts with a web browser when you:
    1. Enter an address like [http://www.google.com](http://www.google.com/) into your web browser.
    2. Your request is sent to your device's network interface.
    3. The request goes over the Internet where a search for [http://www.google.com](http://www.google.com/) begins. Behind the scenes, [http://www.google.com](http://www.google.com/) is simply a human-friendly name that represents an IP Address associated with a remote computer or a server.
    4. The remote server accepts the request and sends a response over the Internet to your network interface which hands it to your browser. 
    5. Finally, the browser displays the response in the form of a web page.

##### Understand the client-server model of web interactions, and the role of HTTP as a protocol within that model

* Within the client-server model, the participants in a data message exchange have **clearly defined roles** within that exchange: **the client makes a request**, and **the server issues a response to that request**. You can have many clients connecting to the server, but the dynamic between client and server remains the same.

* ###### Hyptertext Transfer Protocol (HTTP)

  * the set of rules which provide uniformity to the way resources on the web are transferred between applications.
  * **It is a system of rules, a protocol, that serve as a link between applications and the transfer of [hypertext](http://en.wikipedia.org/wiki/Hypertext) documents. Stated differently, it's an agreement, or message format, of how machines communicate with each other.** HTTP follows a simple model where a client makes a **request** to a server and waits for a **response**. Hence, it's referred to as a **request response protocol**. Think of the request and the response as text messages, or strings, which follow a standard format that the other machine can understand.
  * **The main thing you must understand is that when your browser issues a request, it's simply sending some text to an IP address. Because the client (web browser) and the server (recipient of the request) have an agreement, or protocol, in the form of HTTP, the server can take apart the request, understand its components and send a response back to the web browser. The web browser will then process the response strings into content that you can understand.** Navigating to websites like Facebook, Google and Twitter means you've been using HTTP all along. The details were hidden, but your browser was issuing the requests and processing the responses automatically.

* ###### Clients and Servers

  * The **most common client** is an application you interact with on a daily basis called a **Web Browser**. Examples of web browsers include Internet Explorer, Firefox, Safari and Chrome, including mobile versions. Web browsers are responsible for issuing HTTP requests and processing the HTTP response in a user-friendly manner onto your screen. Web browsers aren't the only clients around, as there are many tools and applications that can also issue HTTP requests.
  * The content you're requesting is located on a remote computer called a server. Servers are nothing more than machines or devices capable of handling inbound requests, and their job is to issue a response back. Often, the response they send back contains relevant data as specified in the request.

---

## TCP & UDP

##### Have a clear understanding of the TCP and UDP protocols, their similarities and differences

* ###### Transmission Control Protocol (TCP)

  * The **Transmission Control Protocol (TCP)** is one of the corner-stones of the Internet. One of the key characteristics of this protocol is the fact that it provides **reliable data transfer**. In fact, reliability is listed as a key element of TCP operation as defined in [RFC793](https://www.ietf.org/rfc/rfc793.txt).

  * **The TCP must recover from data that is damaged, lost, duplicated, or delivered out of order by the internet communication system.**

  * **What TCP essentially provides is the abstraction of reliable network communication on top of an unreliable channel. What this abstraction does is to hide much of the complexity of reliable network communication from the application layer: data integrity, de-duplication, in-order delivery, and retransmission of lost data.**

  * The services that TCP provides makes it the protocol of choice for many networked applications. **The flip-side of the benefits that TCP provides are the performance challenges that come with its complexity.** Just because that complexity is abstracted away from a developer working at the application level doesn't mean it doesn't exist. It's there, and it has a very real impact on performance. TCP does attempt to balance this impact on performance by providing mechanisms for flow control and congestion avoidance, which we'll look at later in this assignment. **Reliability isn't the only thing that TCP provides however, it also provides data encapsulation and multiplexing. It achieves this through the use of TCP Segments.**

  * ###### TCP Segments:

    * **Segments are the Protocol Data Unit (PDU) of TCP. Like the PDUs of protocols we've looked at for other network layers, it uses a combination of headers and payload to provide encapsulation of data from the layer above.**
    * **A TCP Segment header contains a number of different fields.** As we saw earlier in this Lesson, **two of these fields -- Source Port and Destination Port -- provide the multiplexing capability of the protocol.** Most of the other header fields are related to the way that TCP implements **reliable data transfer**. A typical TCP header would look something like this.
    * Some of the **more important fields in the header** in terms of **implementing reliability** are:
      - CHECKSUM: **the Checksum provides the Error Detection aspect of TCP reliability.** It is an error checking value generated by the sender using an algorithm. The receiver generates a value using the same algorithm and if it doesn't match, it drops the Segment. We've encountered Checksums already in this course, in other PDUs at other network layers such as IP Packets. Having a Checksum at the Transport Layer does render Checksums at lower layers redundant to a certain extent. IPv6 headers don't include a Checksum for this reason, based on the assumption that checksums are implemented at either the Transport or Link/ Data Link layers (or both).
      - **SEQUENCE NUMBER and ACKNOWLEDGEMENT NUMBER: these two fields are used together to provide for the other elements of TCP reliability such as In-order Delivery, Handling Data Loss, and Handling Duplication.** The precise way in which TCP uses these fields is beyond the scope of this course, but it is essentially a more complex version of the simplified example of the Reliable Protocol we constructed in the previous assignment.
    * Other fields of interest in a typical header are the WINDOW SIZE field and the various Flag fields. **The WINDOW SIZE field is related to Flow Control**, which we will look at a bit later on. The Flag fields are one-bit boolean fields. A couple of these fields, `URG` and `PSH`, are related to how the data contained in the Segment should be treated in terms of its importance or urgency; we aren't going to go into exactly how these particular flags are used. The `SYN`, `ACK`, `FIN`, and `RST` flags are used to establish and end a TCP connection, as well as manage the state of that connection; we'll look at these in some more detail below.
    * ***TCP* is a *connection-oriented* protocol. It establishes a connection using the *Three-way-handshake.***
    * **TCP provides reliability through *message acknowledgement* and *retransmission*, and *in-order delivery*.**
    * **TCP also provides *Flow Control* and *Congestion Avoidance*.**

  * ###### Disadvantages of TCP

    * Although TCP provides reliable data transfer, and also uses flow control and congestion avoidance techniques to try and do so efficiently, there are also **drawbacks** to using it. We've already seen that there is a **latency overhead in establishing a TCP connection due to the handshake process**. Another **potential issue** with using **TCP is Head-of-Line (HOL) blocking**.
    * **Head-of-line blocking is a general networking concept, and isn't specific to TCP. In general terms it relates to how issues in delivering or processing one message in a sequence of messages can delay or 'block' the delivery or processing of the subsequent messages in the sequence.**
    * **With TCP, HOL blocking can occur as a result of the fact that TCP provides for in-order delivery of segments. Although this in order delivery is one aspect of TCP's reliability, if one of the segments goes missing and needs to be retransmitted, the segments that come after it in the sequence can't be processed, and need to be buffered until the retransmission has occurred. This can lead to increased queuing delay which, as we saw in an [earlier assignment](https://launchschool.com/lessons/4af196b9/assignments/097d7577), is one of the elements of latency.**
    * **The main *downsides of TCP* are the *latency overhead of establishing a connection*, and the potential *Head-of-line blocking* as a result of in-order delivery.**

* ###### User Datagram Protocol (UDP)

  * In the previous assignment, we saw how TCP implements reliable data transfer through sequencing and retransmission of lost data, as well as providing mechanisms for flow control and congestion avoidance. So how does UDP implement all of those things? Well, basically, it doesn't.
  * **The Protocol Data Unit (PDU) of UDP is known as a Datagram. Like all the PDUs we've looked at so far it encapsulates data from the layer above into a payload and then adds header information.** If we examine the header of a UDP Datagram, we can see that it's really quite simple.
  * **The header only has four fields: Source Port, Destination Port, UDP Length (the length, in bits, of the Datagram, including any encapsulated data), and a Checksum field to provide for error detection. That's it.** Even the Checksum field is optional if using IPv4 at the Network layer (if using IPv6, you need to include a Checksum in the Datagram since IPv6 packets don't include one themselves).
  * **Through the use of the Source and Destination Port numbers, UDP provides multiplexing in the same way that TCP does. Unlike TCP however, it doesn't do anything to resolve the inherent unreliability of the layers below it.** In fact, it's probably easier to define UDP by what it *doesn't* do (particularly in comparison with TCP) than by what it *does* do.
    * It provides **no guarantee of message delivery**
    * It provides **no guarantee of message delivery order**
    * It provides **no built-in congestion avoidance or flow-control mechanisms**
    * It provides **no connection state tracking, since it is a connectionless protocol**
  * You might be wondering, if UDP is unreliable then why use it? Why not just use TCP? **The advantage that UDP has over TCP is its simplicity. This simplicity provides two things to a software engineer: speed and flexibility.**
  * **UDP is a connectionless protocol. Applications using UDP at the Transport layer can just start sending data without having to wait for a connection to be established with the application process of the receiver. In addition to this, the lack of acknowledgements and retransmissions means that the actual data delivery itself is faster; once a datagram is sent it doesn't have to be sent again. Latency is less of an issue since without acknowledgements data essentially just flows one way: from sender to receiver. The lack of in-order delivery also removes the issue of Head-of-line blocking (at least at the Transport layer).**
  * It's likely that someone building a UDP-based application will want to implement some of the services that UDP doesn't natively provide. Which services those would be, and the way they're implemented, would be up to whoever was building the application though. For example, you might want your application to have in-order delivery, but at the same time not be worried about the occasional piece of lost data. You could implement sequencing, but choose not to implement data retransmission. The specifics of which services to include are left up to the software engineer and can be implemented at the application level, effectively using UDP as a 'base template' to build on top of.
  * An example of such an application would be a voice or video calling application. The occasional piece of dropped data leading to a slightly glitchy call or a few pixels of video not rendering properly is worth the trade off of the speed provided by the protocol which allows the application to work even over long distances where there is high latency. Another example would be online gaming where the occasional loss of data causing a slight glitch is more acceptable than having significant lag in the gaming experience.
  * While UDP provides a lot of flexibility and freedom, with that freedom comes a certain amount of responsibility. There are various best practices that should be adhered to. For example, it would be expected that your UDP-based application implements some form of congestion avoidance in order to prevent it overwhelming the network.
  * ***UDP* is a very simple protocol compared to TCP. It provides *multiplexing*, but no reliability, no in-order delivery, and no congestion or flow control.**
  * ***UDP* is *connectionless*, and so doesn't need to establish a connection before it starts sending data.**
  * **Although it is unreliable, the *advantage of UDP* is *speed* and *flexibility*.**

##### Have a broad understanding of the three-way handshake and its purpose

* In an earlier assignment we briefly looked at the difference between connectionless and connection-oriented communication. **TCP is a connection-oriented protocol, it doesn't start sending application data until a connection has been established between application processes. In order to establish a connection TCP uses what is known as a Three-way Handshake: this is where the `SYN` and `ACK` flags come into play**; the `FIN` flag is used in different process, the Four-way Handshake, used for terminating connections.
* In the **Three-Way Handshake process**, the following happens:
  * The **sender sends a SYN message** (a TCP Segment with the `SYN` flag set to `1`)
  * Upon receiving this SYN message, **the receiver sends back a SYN ACK message** (a TCP Segment with the `SYN` and `ACK` flags set to `1`)
  * Upon receiving the SYN ACK, **the sender then sends an `ACK`** (a TCP Segment with the `ACK` flag set to `1`)
* **Upon sending the ACK, the sender can immediately start sending application data. The receiver must wait until it has received the ACK before it can send any data back to the sender.** One of the main reasons for this process is to synchronise (`SYN`) the sequence numbers that will be used during the connection.
* One of the main take-aways should be that there's a certain amount of complexity involved in the way that TCP manages connection state. This fact is particularly pertinent to the initial establishment of a connection, where **a key characteristic of the process is that the sender cannot send any application data until after it has sent the `ACK` Segment. What this means in practical terms, is that there is an entire round-trip of latency before any application data can be exchanged. Since this hand-shake process occurs every time a TCP connection is made, this clearly has an impact on any application which uses TCP at the transport layer.**
* **TCP involves a lot of overhead in terms of establishing connections**, and providing reliability through the retransmission of lost data. In order to mitigate against this additional overhead, it is important that the actual functioning of data transfer when using the protocol occurs as efficiently as possible. In order to help facilitate efficient data transfer once a connection is established, TCP provides mechanisms for flow control and congestion avoidance.

##### Have a broad understanding of flow control and congestion avoidance

* ###### Flow Control:

  * **Flow control is a mechanism to prevent the sender from overwhelming the receiver with too much data at once. The receiver will only be able to process a certain amount of data in a particular time-frame. Data awaiting processing is stored in a 'buffer'. The buffer size will depend on the amount of memory allocated according to the configuration of the OS and the physical resources available.**
  * **Each side of a connection can let the other side know the amount of data that it is willing to accept via the WINDOW field of the TCP header. This number is dynamic, and can change during the course of a connection. If the receiver's buffer is getting full it can set a lower amount in the WINDOW field of a Segment it sends to the sender, the sender can then reduce the amount of data it sends accordingly.**
  * **Although flow control prevents the sender from overwhelming the receiver, it doesn't prevent either the sender or receiver from overwhelming the underlying network. For that task we need a different mechanism: Congestion Avoidance.**

* ###### Congestion Avoidance:

  * **Network Congestion is a situation that occurs when there is more data being transmitted on the network than there is network capacity to process and transmit the data.** You can perhaps think of it as similar to a gridlock of vehicles on a road network. Instead of things coming to a standstill however, the 'excess vehicles' are simply lost.
  * **In the [last lesson](https://launchschool.com/lessons/4af196b9/assignments/b222ecfb) we looked at IP packets moving across the networks in a series of 'hops'. At each hop, the packet needs to be processed: the router at that hop runs a checksum on the packet data; it also needs to check the destination address and work out how to route the packet to the next hop on its journey to that destination. All of this processing takes time, and a router can only process so much data at once. Routers use a 'buffer' to store data that is awaiting processing, but if there is more data to be processed than can fit in the buffer, the buffer over-flows and those data packets are dropped.**
  * **As we've already seen, TCP retransmits lost data. If lots of data is lost that means lots of retransmitted data, which is inefficient. Ideally we want to keep retransmission to a minimum. TCP actually uses data loss as a feedback mechanism to detect, and avoid, network congestion; if lots of retransmissions are occurring, TCP takes this as a sign that the network is congested and reduces the size of the transmission window.**
  * There are various different approaches and algorithms for determining the size of the initial transmission window, and how much it should be reduced or increased by depending on network conditions. The exact algorithm or approach used will depend on which variant of TCP is in operation.

---

## URLs

###### Uniform Resource Identifier (URI)

* **a string of characters which identifies a particular resource. It is part of a system by which resources should be uniformly addressed on the Web.** The W3C website describes the purpose as follows: The Web is an information space. Human beings have a lot of mental machinery for manipulating, imagining, and finding their way in spaces. URIs are the points in that space.

###### Uniform Resource Locator (URL)

*  When you want to check Facebook's games page, you start by launching your web browser and navigating to http://www.facebook.com/games. The web browser makes an HTTP request to this address resulting in the resource being returned to your browser. The address you entered, `https://www.facebook.com/games`, is known as a Uniform Resource Locator or **URL**. A URL is like that address or phone number you need in order to visit or communicate with your friend. A URL is the most frequently used part of the general concept of a Uniform Resource Identifier or **URI**, which specifies how resources are located.

* **According to [RFC3986](https://tools.ietf.org/html/rfc3986#section-1.1.3), a URI is a "sequence of characters that identifies an abstract or physical resource", and a URL refers to:**

  > **the subset of URIs that, in addition to identifying a resource, provide a means of locating the resource by describing its primary access mechanism (e.g., its network "location").**

* **We can take from this that a URL is a *subset* of URI that includes the network location of the resource.** Technically, something like `https://launchschool.com/forum` could be referred to as both a URL and a URI. For ease of communication though it's probably best to just stick with URL, since this is a more specific description.

##### Be able to identify the components of a URL, including query strings

* When you see a URL, such as "http://www.example.com:88/home?item=book", it is comprised of several components. We can break this URL into 5 parts:
  - `http`: The **scheme**. It always comes before the colon and two forward slashes and **tells the web client how to access the resource.** In this case it tells the web client to use the Hypertext Transfer Protocol or HTTP to make a request. Other popular URL schemes are `ftp`, `mailto` or `git`. You may sometimes see this part of the URL referred to as the *protocol*, and there is a connection between the two things in that the scheme can indicate which protocol (or system of rules) should be used to access the resource; in the context of of a URL however, the correct term for this component is the *scheme*.
  - `www.example.com`: The **host**. **It tells the client where the resource is hosted or located.**
  - `:88` : The **port** or port number. It is only required if you want to use a port other than the default. **Unless a different port number is specified, port `80` will be used by default in normal HTTP requests.**
  - `/home/`: The **path**. **It shows what local resource is being requested.** This part of the URL is optional. Although server-side and client-side frameworks differ in their implementation, one thing they have in common is that the way the path portion of the URL is used is determined by the application logic, and doesn't necessarily bear any relationship to an underlying file structure on the server. The way that the path is used will vary according to the specific implementation of the application or framework, but often involves URL pattern-matching to match the path to a pre-defined 'route' which then executes some specific logic.
  - `?item=book` : The **query string**, which is made up of **query parameters**. **It is used to send data to the server.** This part of the URL is also optional. **Because query strings are passed in through the URL, they are only used in HTTP _GET_ requests.**

##### Be able to construct a valid URL

* Point

##### Have an understanding of what URL encoding is and when it might be used

* **URLs are designed to accept only certain characters in the standard 128-character [ASCII character set](http://en.wikipedia.org/wiki/ASCII). Reserved or unsafe ASCII characters which are not being used for their intended purpose, as well as characters not in this set, have to be encoded. URL encoding serves the purpose of replacing these non-conforming characters with a `%` symbol followed by two hexadecimal digits that represent the [ASCII code](http://www.asciitable.com/) of the character.**

* Below are some popular encoded characters and example URLs:

  | Character | ASCII code | URL                                                          |
  | :-------- | :--------- | :----------------------------------------------------------- |
  | Space     | 20         | [http://www.thedesignshop.com/shops/tommy%20hilfiger.html](http://www.thedesignshop.com/shops/tommy hilfiger.html) |
  | !         | 21         | [http://www.thedesignshop.com/moredesigns%21.html](http://www.thedesignshop.com/moredesigns!.html) |
  | +         | 2B         | http://www.thedesignshop.com/shops/spencer%2B.html           |
  | #         | 23         | http://www.thedesignshop.com/%23somequotes%23.html           |

* **Characters must be encoded if:**

  1. **They have no corresponding character within the standard [ASCII character set](http://www.asciitable.com/).**
  2. **The use of the character is unsafe because it may be misinterpreted, or even possibly modified by some systems. For example `%` is unsafe because it can be used for encoding other characters. Other unsafe characters include spaces, quotation marks, the `#` character, `<` and `>`, `{` and `}`, `[` and `]`, and `~`, among others.**
  3. **The character is reserved for special use within the URL scheme. Some characters are reserved for a special meaning; their presence in a URL serve a specific purpose. Characters such as `/`, `?`, `:`, `@`, and `&` are all reserved and must be encoded. For example `&` is reserved for use as a query string delimiter. `:` is also reserved to delimit host/port components and user/password.**

* 

---

## HTTP and the Request/Response Cycle

##### Be able to explain what HTTP requests and responses are, and identify the components of each

* **A single HTTP message exchange consists of a *Request* and a *Response*.** The exchange generally **takes place between a *Client* and a *Server*.** The **client sends a Request to the server** and the **server sends back a Response.**
* **HTTP operates at the application layer and is concerned with structuring the messages that are exchanged between applications**; it's actually TCP/IP that's doing all the heavy lifting and ensuring that the request/response cycle gets completed between your browser and the server.
* **HTTP is a *text-based* protocol. HTTP Request and Responses involve sending text between the client and server.**
* In order for the protocol to work, the Request and Response must be structured in such a way that both the client and the server can understand them.

* ###### HTTP Requests:

  * **An *HTTP Request* consists of a *request line*, *headers*, and an optional *body*.**

  * Making an HTTP request is easy. Say you want to visit Reddit in your browser. All you need to do is launch your browser and enter the address [https://www.reddit.com](https://www.reddit.com/).

  * The server that hosts the main Reddit website handles your request and issues a response back to your browser. Your browser is smart enough to process the response that is sent back and display the site you see, with all its colors, images, text and presentation.

  * Because browsers show us the processed version of the response, we don't get to see the raw response the server sent back.

  * But one HTTP request may also initiate other HTTP requests: why are these additional responses sent back, and who initiated the requests? What's happening is that the resource we requested, the initial `www.reddit.com` entry, **returned some HTML**. And in that HTML body are references to other resources like images, css stylesheets, javascript files and more. Your browser, being smart and helpful, understands that in order to produce a visually appealing presentation, it has to go and grab all these referenced resources. Hence, **the browser will make separate requests for each resource referenced in the initial response.**

  * **HTTP Request Method:** you can think of this as **the verb that tells the server what action to perform on a resource.**  The **two most common HTTP request methods you'll see are `GET` and `POST`.** When you think about retrieving information, think `GET`, which is the most used HTTP request method. 

  * The important thing to understand is that every request gets a response, even if the response is an error -- that's still a response. (That's not 100% technically true as some requests can **time out**, but we'll set those rare cases aside for now.)

  * ###### GET Requests:

    * **`GET` requests are initiated by clicking a link or via the address bar of a browser.** When you type an address like `https://www.reddit.com` into the address bar of your browser, you're making a `GET` request. **You're asking the web browser to go retrieve the resource at that address**, which means we've been making `GET` requests throughout this book. The same goes for interacting with links on web applications. **The default behavior of a link is to issue a `GET` request to a URL.**
    * GET requests are used to retrieve a resource, and most links are GETs.
    * **The response from a GET request can be anything, but if it's HTML and that HTML references other resources, your browser will automatically request those referenced resources.** A pure HTTP tool will not.

  * ###### POST Requests:

    * We've seen how to retrieve or ask for information from a server with `GET`, but what if you need to send or submit data to the server? That's where another essential HTTP request method comes in: `POST`.**`POST` is used when you want to initiate some action on the server, or send data to a server.**
    * **Typically from within a browser, you use `POST` when submitting a form. `POST` requests allow us to send much larger and sensitive data to the server, such as images or videos.** For example, say we need to send our username and password to the server for authentication. We could use a `GET` request and send it through query strings. The flaw with this approach is obvious: our credentials become exposed instantly in the URL; that isn't what we want. Using a `POST` request in a form fixes this problem. `POST` requests also help sidestep the query string size limitation that you have with `GET` requests. With `POST` requests, we can send significantly larger forms of information to the server.
    * But the mystery is, how is the data we're sending being submitted to the server since it's not being sent through the URL? The answer to that is the HTTP **body**. **The body contains the data that is being transmitted in an HTTP message and is optional.** In other words, an HTTP message can be sent with an empty body. **When used, the body can contain HTML, images, audio and so on.** You can think of the body as the letter enclosed in an envelope, to be posted.

  * ###### Required Components of an HTTP Request:

    * **The HTTP method and the path are required, and form part of what is known as the start-line or request-line. As of HTTP 1.0, the HTTP version also forms part of the request-line. The `Host` header is a required component since HTTP 1.1. Parameters, all other headers, and message body are optional.**

  * ###### HTTP Headers:

    * HTTP headers allow the client and the server to send additional information during the request/response HTTP cycle. Headers are colon-separated name-value pairs that are sent in plain text.
    * With HTTP/1.1, the end of the headers is indicated by an *empty line*.
    * The `Content-Length` header can be used to indicate the *size of the body*. This can help determine where the HTTP message should end.

  * ###### Request Headers:

    * Request headers give more information about the client and the resource to be fetched. Some useful request headers are:

      | Field Name      | Description                                 | Example                                                      |
      | :-------------- | :------------------------------------------ | :----------------------------------------------------------- |
      | Host            | The domain name of the server.              | Host: [www.reddit.com](http://www.reddit.com/)               |
      | Accept-Language | List of acceptable languages.               | Accept-Language: en-US,en;q=0.8                              |
      | User-Agent      | A string that identifies the client.        | User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/38.0.2125.101 Safari/537.36 |
      | Connection      | Type of connection the client would prefer. | Connection: keep-alive                                       |

    * Don't bother memorizing any of the request headers, but just know that it's part of the request being sent to the server.

    

  * **The most important components to understand about an HTTP request are:**

    - HTTP method (i.e. GET or POST)
    - path (i.e. URL path)
    - headers
    - message body (for `POST` requests)

* ###### HTTP Response:

  * **An *HTTP Response* consists of a *status line*, optional *headers*, and an optional *body*.**

  * So far we've been sending various requests and looking at the raw HTTP data sent back by the server. This raw data returned by the server is called a **response**.

  * ###### Status Codes: (see section below)

  * ###### Response Headers:

    * Response headers offer more information about the resource being sent back. Some common response headers are:

      | Header Name      | Description                             | Example                                |
      | :--------------- | :-------------------------------------- | :------------------------------------- |
      | Content-Encoding | The type of encoding used on the data.  | Content-Encoding: gzip                 |
      | Server           | Name of the server.                     | Server:thin 1.5.0 codename Knife       |
      | Location         | Notify client of new resource location. | Location: https://www.github.com/login |
      | Content-Type     | The type of data the response contains. | Content-Type:text/html; charset=UTF-8  |

    * There are a lot more response headers, but just like request headers, it's not necessary to memorize them. They have subtle effects on the data being returned, and in some cases, they have subtle workflow consequences (eg, your browser automatically following a `Location` response header). Just understand that response headers contain additional meta-information about the response data being returned.

  * ###### Required Components of an HTTP Response:

    * Status code is required. Headers and body are optional.

  * In sum, we've seen that HTTP is nothing more than an agreement in the form of formatted text that dictates how a client and server communicate.

    The most important parts of an HTTP response are:

    - status code
    - headers
    - message body, which contains the raw response data

##### Be able to describe the HTTP request/response cycle

* **GET Request:** the server response to this request will be to send the client the information associated with the web page specified by the URL.
* **`GET` requests should only retrieve content from the server.** They can generally be thought of as "read only" operations, however, there are some subtle exceptions to this rule. For example, consider a webpage that tracks how many times it is viewed. `GET` is still appropriate since the main content of the page doesn't change.
* **POST Request:** the server response will send a response that contains a reference location in the response header, that will then be automatically used by the client to issue another request for the webpage associated with the reference location.
* **`POST` requests involve changing values that are stored on the server.** Most HTML forms that submit their values to the server will use `POST`. Search forms are a noticeable exception to this rule: they often use `GET` since they are not changing any data on the server, only viewing it.

##### Be able to explain what status codes are, and provide examples of different status code types

*  **The `status code` is a three-digit number that the server sends back after receiving a request signifying the status of the request. The `status text` displayed next to `status code` provides the description of the code.**

* The most common response status code you'll encounter is **200** which means the request was handled successfully. Other useful status codes are:

  | Status Code | Status Text           | Meaning                                                      |
  | :---------- | :-------------------- | :----------------------------------------------------------- |
  | 200         | OK                    | The request was handled successfully.                        |
  | 302         | Found                 | The requested resource has changed temporarily. Usually results in a redirect to another URL. |
  | 404         | Not Found             | The requested resource cannot be found.                      |
  | 500         | Internal Server Error | The server has encountered a generic error.                  |

* As a web developer, you should know the above response status codes and their associated meaning very well.

* ###### 302 Found:

  * What happens when a resource is moved? The most common strategy is to re-route the request from the original URL to a new URL. The general term for this kind of re-routing is called a `redirect`. When your browser sees a response status code of *302*, it knows that the resource has been moved, and will automatically follow the new re-routed URL in the `Location` response header.
  * Say you want to access the account profile at [Github](http://www.github.com/), you'll have to go to the address `https://github.com/settings/profile`. However, in order to have access to the profile page, you must first be signed in. If you're not already signed in, the browser will send you to a page to do that. After you enter your credentials, you'll be redirected to the original page you were trying to access. This is a pretty common workflow most web applications employ.
  * **Unlike 4xx and 5xx response codes, 3xx codes don't indicate an error. Instead they are generally used in relation to redirection, and indicate to the client that it must take some additional action in order to complete the request.**

* ###### 404 Not Found:

  * Next, let's look at a `404` response status code in the browser. The server returns this status code when the requested resource cannot be found. Remember, a resource can be anything including audio files, CSS stylesheets, JavaScript files, images etc.
  * **4xx level response codes indicate an error or issue on the client side, i.e. with the request. A `400` error is a general indication that there is a problem with the structure of the request; in other words the server did not understand the request due to its syntax. This is basically the server saying to the client 'I don't understand what you just asked me'.**

* ###### 500 Internal Server Error:

  * A `500` status code says "there's something wrong on the server side". This is a generic error status code and the core problem can range from a mis-configured server setting to a misplaced comma in the application code. But whatever the problem, it's a server side issue. Someone with access to the server will have to debug and fix the problem, which is why sometimes you see a vague error message asking you to contact your System Administrator. In the wild, a 500 error can be shown in a variety of ways, just like a 404 page can.
  * **5xx level response codes indicate an error or issue on the server side. This time the request was valid, and the server was able to understand it, but it replies to the client that it cannot communicate using the version of HTTP that the client wants to use.**

##### Understand what is meant by 'state' in the context of the web, and be able to explain some techniques that are used to simulate state

* ###### Statelessness:

  * A protocol is said to be **stateless** when it's designed in such a way that **each request/response pair is completely independent of the previous one.** It is important to be aware of HTTP as a stateless protocol and the impact it has on server resources and ease of use. In the context of HTTP, it means that the server does not need to hang on to information, or state, between requests. As a result, when a request breaks en route to the server, no part of the system has to do any cleanup. Both these reasons make HTTP a resilient protocol, as well as a difficult protocol for building stateful applications. Since HTTP, the protocol of the internet, is inherently stateless that means web developers have to work hard to simulate a stateful experience in web applications.

  * When you go to Facebook, for example, and log in, you expect to see the internal Facebook page. That was one complete request/response cycle. You then click on the picture -- another request/response cycle -- but you do not expect to be logged out after that action. If HTTP is stateless, how did the application maintain state and remember that you already input your username and password? In fact, if HTTP is stateless, how does Facebook even know this request came from *you*, and how does it differentiate data from you vs. any other user? There are tricks web developers and frameworks employ to make it seem like the application is stateful, but those tricks are beyond the scope of this book. The key concept to remember is that even though you may feel the application is stateful, underneath the hood, the web is built on HTTP, a stateless protocol. It's what makes the web so resilient, distributed, and hard to control. It's also what makes it so difficult to secure and build on top of.

  * **Each request made to a resource is treated as a brand new entity, and different requests are not aware of each other. This *statelessness* is what makes HTTP and the internet so distributed and difficult to control, but it's also the same ephemeral attribute that makes it difficult for web developers to build stateful web applications.**

  * ###### Sessions:

    * It's obvious the stateless HTTP protocol is somehow being augmented to maintain a sense of statefulness. With some help from the client (i.e., the browser), **HTTP can be made to act as if it were maintaining a stateful connection with the server, even though it's not.** One way to accomplish this is by having **the server send some form of a unique token to the client.** Whenever a client makes a request to that server, the client appends this token as part of the request, **allowing the server to identify clients.** In web development, we call this unique token that gets passed back and forth the **session identifier**.
    * **This mechanism of passing a `session id` back and forth between the client and server creates a sense of persistent connection between requests.** Web developers leverage this faux statefulness to build sophisticated applications. **Each request, however, is technically stateless and unaware of the previous or the next one.**
    * **This sort of faux statefulness has several consequences. First, every request must be inspected to see if it contains a session identifier. Second, if this request does, in fact, contain a session id, the server must check to ensure that this session id is still valid. The server needs to maintain some rules with regards to how to handle session expiration and also decide how to store its session data. Third, the server needs to retrieve the session data based on the session id. And finally, the server needs to recreate the application state (e.g., the HTML for a web request) from the session data and send it back to the client as the response.**
    * This means that the server has to work very hard to simulate a stateful experience, and every request still gets its own response, even if most of that response is identical to the previous response. For example, if you're logged into Facebook, the server has to generate the initial page you see, and the response is a pretty complex and expensive HTML that your browser displays. The Facebook server has to add up all the likes and comments for every photo and status, and present it in a timeline for you. It's a very expensive page to generate. Now if you click on the "like" link for a photo, Facebook has to regenerate that entire page. It has to increment the like count for that photo you liked, and then send that HTML back as a response, even though the vast majority of the page stayed the same.
    * Fortunately, Facebook uses Ajax instead of refreshing your browser. But if Facebook didn't use Ajax, each page refresh would take a really long time.
    * There are many advanced techniques that servers employ to optimize sessions and, as you can imagine, there are also many security concerns. Most of the advanced session optimization and security concerns are out of scope of this book, but **we'll talk about one common way to store session information: in a browser cookie.**

  * ###### Cookies:

    * **A cookie is a piece of data that's sent from the server and stored in the client during a request/response cycle.** **Cookies** or **HTTP cookies**, are **small files stored in the browser and contain the session information.** By default, most browsers have cookies enabled. When you access any website for the first time, the server sends session information and sets it in your browser cookie on your local computer. Note that the actual session data is stored on the server. The client side cookie is compared with the server-side session data on each request to identify the current session. This way, when you visit the same website again, your session will be recognized because of the stored cookie with its associated information.

    * Let's see a real example of how cookies are initiated with the help of the browser inspector. We'll make a request to the address `https://www.yahoo.com`. Note that if you're following along, you may have to use a different website if you already have an existing cookie from Yahoo.

    * With the inspector's Network tab open, navigate to that address and inspect the request headers:

    * Note it has no reference to cookies. Next, look at the response headers:

    * You'll notice it has **set-cookie** headers that add cookie data to the response. This cookie data got set on the first visit to the website. Finally, make a request to the same address and then look at the request headers:

    * You'll see the **cookie** header set (note that this is the *request* header, which implies it's being sent by your client to the server). It contains the cookie data sent previously by the **set-cookie** response header. **This piece of data will be sent to the server each time you make a request and uniquely identifies you -- or more precisely, it identifies your client, which is your browser.** The browser on your computer stores these cookies. **Now, if you were to close your browser and shut down your computer, the cookie information would still persist.**

    * **Where is the session data stored?**

      The simple answer is: on the server *somewhere*. Sometimes, it's just stored in memory, while other times, it could be stored in some persistent storage, like a database or key/value store. Where the session data is actually stored is not too important right now. **The most important thing is to understand that the session id is stored on the client, and it is used as a "key" to the session data stored server side.** That's how web applications work around the statelessness of HTTP.

    * It is important to be aware of the fact that the id sent with a session is unique and expires in a relatively short time. In this context, it means you'll be required to login again after the session expires. If we log out, the session id information is gone.

    * This also implies that if we manually remove the session id (in the inspector, you can right click on cookies and delete them), then we have essentially logged out.

    * To recap, we've seen that the session data is generated and stored on the server-side and **the session id is sent to the client in the form of a cookie.** We've also looked at how web applications take advantage of this to mimic a stateful experience on the web.

  * ###### AJAX:

    * Last, we'll briefly mention `AJAX` and what it means in the HTTP request/response cycle. **AJAX is short for Asynchronous JavaScript and XML. Its main feature is that it allows browsers to issue requests and process responses *without a full page refresh*.** For example, if you're logged into Facebook, the server has to generate the initial page you see, and the response is a pretty complex and expensive HTML page that your browser displays. The Facebook server has to add up all the likes and comments for every photo and status, and present it in a timeline for you. As we described earlier, it's a very expensive page to re-generate for every request (remember, every action you take -- clicking a link, submitting a form -- issues a new request).
    * **When AJAX is used, all requests sent from the client are performed *asynchronously*, which just means that the page doesn't refresh.** Let's see an example by performing some search on google:
      * Make a request to `https://www.google.com` and open the browser's inspector network tab. You'll notice the network tab is empty:
      * As soon as you start your search, you'll see the network tab gets flooded with requests.
    * No doubt you've performed searches many times and notice the page doesn't refresh. The Network tab however gives us some new insight into what's happening: every letter you type is issuing a new request, which means that an AJAX request is triggered with every key-press. The responses from these requests are being processed by some callback. You can think of a `callback` as a piece of logic you pass on to some function to be executed after a certain event has happened. In this case, the callback is triggered when the response is returned. You can probably guess that the callback that's processing these asynchronous requests and responses is updating the HTML with new search results.
    * We won't get into what the callback looks like or how to issue an AJAX request, but the main thing to remember is that AJAX requests are just like normal requests: they are sent to the server with all the normal components of an HTTP request, and the server handles them like any other request. The only difference is that instead of the browser refreshing and processing the response, the response is processed by a callback function, which is usually some client-side JavaScript code.

    

---

## Security

##### Have an understanding of various security risks that can affect HTTP, and be able to outline measures that can be used to mitigate against these risks

* One of the major characteristics of HTTP is that it is a text-based protocol. **By working with HTTP Requests and Responses, we've seen that they are transferred across the network in plain text.** It's also essentially a fairly simple protocol, with quite a basic message structure and set of rules.

* **While these characteristics makes it easier to design and build applications that interact with the protocol, the major downside is a lack of security. If an HTTP Request or Response is intercepted, the contents of that message can easily be read. It's also difficult to know if the source of an HTTP response is trustworthy, or if an HTTP message has been tampered with in transit.**

* This lack of security might not matter too much if you are just sending funny cat memes to a friend, but there are many situations where the ability to securely transfer data is vital. HTTP is used in applications that provide services such as online shopping or banking, as well as many other use cases where security is paramount.

* ###### Secure HTTP (HTTPS)

  * **As the client and server send requests and responses to each other, all information in both requests and responses are being sent as strings. If a malicious hacker was attached to the same network, they could employ *packet sniffing* techniques to read the messages being sent back and forth. As we learned previously, requests can contain the session id, which uniquely identifies you to the server, so if someone else copied this session id, they could craft a request to the server and pose as your client, and thereby automatically being logged in without even having access to your username or password.**
  * This is where **Secure HTTP**, or **HTTPS**, helps. A resource that's accessed by HTTPS will start with `https://` instead of `http://`, and usually be displayed with a lock icon in most browsers.
  * **With HTTPS every request/response is encrypted before being transported on the network. This means if a malicious hacker sniffed out the HTTP traffic, the information would be encrypted and useless.**
  * **HTTPS sends messages through a cryptographic protocol called Transport Layer Security ([TLS](http://en.wikipedia.org/wiki/Transport_Layer_Security)) for encryption.** Earlier versions of HTTPS used `SSL`or Secure Sockets Layer until `TLS` was developed. **These cryptographic protocols use certificates to communicate with remote servers and exchange security keys before data encryption happens.** You can inspect these certificates by clicking on the padlock icon that appears before the `https://`.

* ###### Same-origin policy

  * **The same-origin policy is an important concept that permits unrestricted interaction between resources originating from the same origin, but restricts certain interactions between resources originating from different origins.** What we mean by *origin* here is **the combination of a url's scheme, hostname, and port**. So `http://mysite.com/doc1` would be considered to have the same origin as `http://mysite.com/doc2`, but a different origin to `https://mysite.com/doc2` (different scheme), `http://mysite.com:4000/doc2` (different port), and `http://anothersite.com/doc2` (different host).
  * **Same-origin policy doesn't restrict *all* cross-origin requests. Requests such as linking, redirects, or form submissions to different origins are typically allowed. Also typically allowed is the embedding of resources from other origins, such as scripts, css stylesheets, images and other media, fonts, and iframes.** What *is* typically restricted are cross-origin requests where resources are being accessed programmatically using APIs such as `XMLHttpRequest` or `fetch` (the details of which are beyond the scope of this book).
  * While secure, same-origin policy is an issue for web developers who have a legitimate need for making these restricted kinds of cross-origin requests. Cross-origin resource sharing or **CORS** was developed to deal with this issue. CORS is a mechanism that allows interactions that would normally be restricted cross-origin to take place. It works by adding new HTTP headers, which allow servers to serve resources cross-origin to certain specified origins.
  * **The same-origin policy is an important guard against session hijacking (see next section) attacks and serves as a cornerstone of web application security.** Let's look at some HTTP security threats and their counter-measures.

* ###### Session Hijacking

  * We've already seen that the session plays an important role in keeping HTTP stateful. We also know that a session id serves as that unique token used to identify each session. **Usually, the session id is implemented as a random string and comes in the form of a cookie stored on the computer.** With the session id in place on the client side now every time a request is sent to the server, this data is added and used to identify the session. In fact, this is what many web applications with authentication systems do. When a user's username and password match, the session id is stored on their browser so that on the next request they won't have to re-authenticate.

  * Unfortunately, **if an attacker gets a hold of the session id, both the attacker and the user now share the same session and both can access the web application. In session hijacking, the user won't even know an attacker is accessing his or her session without ever even knowing the username or password.**

  * ###### Countermeasures for Session Hijacking:

    * One popular way of solving session hijacking is by **resetting sessions.** **With authentication systems, this means a successful login must render an old session id invalid and create a new one. With this in place, on the next request, the victim will be required to authenticate. At this point, the altered session id will change, and the attacker will not be able to have access.** Most websites implement this technique by making sure users authenticate when entering any potentially sensitive area, such as charging a credit card or deleting the account.
    * Another useful solution is by **setting an expiration time on sessions**. Sessions that do not expire give an attacker an infinite amount of time to pose as the real user. **Expiring sessions after, say 30 minutes, gives the attacker a far narrower window to access the app.**
    * Finally, as we have already covered, **another approach is to use HTTPS across the entire app to minimize the chance that an attacker can get to the session id.**

* ###### Cross-Site Scripting (XSS):

  * The final security concern we'll talk about, and a very important one for all web developers, is called Cross-site scripting, or **XSS**. **This type of attack happens when you allow users to input HTML or JavaScript that ends up being displayed by the site directly.**

  * For example, the form below allows you to add comments, which will then be displayed on the site.

  * Because it's just a normal HTML `<textarea>`, **users are free to input anything into the form. This means users can add raw HTML and JavaScript into the text area and submit it to the server as well.**

  * **If the server side code doesn't do any sanitization of input, the user input will be injected into the page contents, and *the browser will interpret the HTML and JavaScript and execute it*. In this case an alert message will pop up, which is definitely not the desired outcome. Attackers can craft ingeniously malicious HTML and JavaScript and be very destructive to both the server as well as future visitors of this page. For example, an attacker can use JavaScript to grab the session id of every future visitor of this site and then come back and assume their identity. It could happen silently without the victims ever knowing about it. Note that the malicious code would bypass the same-origin policy because the code lives on the site.**

  * ###### Potential solutions for cross-site scripting:

    * **One way to prevent this kind of attack is by making sure to always sanitize user input.** Eliminate problematic input, such as <script> tags, or disallowing HTML and JavaScript input altogether in favor of a safer format, like Markdown.
    * **The second way to guard against XSS is to escape all user input data when displaying it. If you do need to allow users to input HTML and JavaScript, then when you print it out, make sure to escape it so that the browser does not interpret it as code.**
    * **Escaping:** We mention the term "escaping" above. **To escape a character means to replace an HTML character with a combination of [ASCII](http://www.asciitable.com/) characters, which tells the client to display that character as is, and to not process it; this helps prevent malicious code from running on a page.** These combinations of ASCII characters are called [HTML entities](http://entitycode.com/#math-content).

##### Be aware of the different services that TLS can provide, and have a broad understanding of each of those services

* HTTPS sends messages through a cryptographic protocol called Transport Layer Security ([TLS](http://en.wikipedia.org/wiki/Transport_Layer_Security)) for encryption. Earlier versions of HTTPS used `SSL`or Secure Sockets Layer until `TLS` was developed. These cryptographic protocols use certificates to communicate with remote servers and exchange security keys before data encryption happens. You can inspect these certificates by clicking on the padlock icon that appears before the `https://`.

* **There are three important security services that are provided by TLS: Encryption, Authentication, and Integrity.** Each of these services are important in their own right, but when combined they provide for very secure message exchange over what is essentially an unsecure channel. Let's look a bit more closely at the nature of these services.

* **Encryption:** a process of encoding a message so that it can only be read by those with an authorized means of decoding the message.

* **Authentication:** a process to verify the identity of a particular party in the message exchange.

* **Integrity:** a process to detect whether a message has been interfered with or faked

* It isn't mandatory for an application which uses TLS that all three of these services are used simultaneously. For example, you could design your application to accept encrypted messages from a sender without authenticating who they are. In practice however, all three services are generally used together to provide the most secure connection possible.

* ###### TLS Encryption:

  * Encryption is a major component of the security provided by TLS. **The way in which TLS sets up an encrypted connection is via a process known as the TLS Handshake.** 

  * ###### Symmertic Key Encryption:

    * Cryptography has evolved over time with regards to the complexity of encryption algorithms and the sophistication of encryption keys. Despite these advances, the underlying concept seen in the Vigenere cipher, whereby sender and receiver share a common encryption key, is still used in modern cryptographic systems. **A shared key system such as this is known as symmetric key encryption.**
    * Alice and Bob want to exchange messages securely. They both agree on a secret key and keep a copy of it. Alice can then encrypt a message using the key and send it to Bob. Bob can decrypt the message using the same key. The same process can be carried out in the other direction for messages that Bob sends to Alice.
    * In order to work securely, this system relies on the sender and receiver both having access to the key and no one else being able to access it. This raises the question: how do sender and receiver exchange encryption keys in the first place?
    * The most secure way to exchange keys would be in person. If we want to use symmetric key encryption over the internet however, this isn't a feasible option. **We also can't just send the key in a readable format to the other party in our message exchange; if the key was intercepted by a third-party, they could then use it to decrypt any subsequent messages between the sender and receiver.** What we need is a mechanism whereby we can encrypt the encryption key itself, so that even if it is intercepted it can't be used.

  * ###### Asymmetric Key Encryption:

    * Asymmetric key encryption, also known as **public key encryption**, uses **a *pair* of keys: a *public* key, and a *private* key.** Unlike the symmetric system where the same key is used to encrypt and decrypt messages, **in the asymmetric system the keys in the pair are non-identical: the public key is used to encrypt and the private key to decrypt.**
    * The exact mechanism by which these keys are generated is beyond the scope of this course. The important thing to understand is that messages encrypted with the public key can *only* be decrypted with the private key. The public key is made openly available but the private key is kept in the sole possession of the message receiver.
    * Alice wants to receive encrypted messages. She generates a public key and a private key. She makes the public key available but keeps the private key to herself. Bob uses Alice's public key to encrypt a message and send it to Alice. Alice decrypts Bob's message using her private key.
    * An important thing to note here is that this encryption is primarily intended to work in one direction. **Bob can send Alice messages encrypted with the public key which she can then decrypt with the private one.** The same key pair would not be used in the other direction for secure communication, since anyone with access to the public key can decrypt the message.

  * ###### The TLS Handshake:

    * To securely send messages via HTTP we want both the request *and* the response to be encrypted in such a way that they can only be decrypted by the intended recipient. The most efficient way to do this is via symmetric key cryptography. If we want to use symmetric keys however, we also need a way to securely exchange the symmetric key.
    * **The clever thing about TLS is the way that it uses a combination of symmetric and asymmetric cryptography.** The bulk of the message exchange is conducted via symmetric key encryption, but **the initial symmetric key exchange is conducted using asymmetric key encryption.** The process by which the initial secure connection is set up is conducted during what is known as the TLS handshake.
    * **TLS assumes TCP is being used at the Transport layer, and the TLS Handshake takes place after the TCP Handshake**. A step-by-step description of the TLS Handshake process might look something like this:
      1. **The TLS Handshake begins with a `ClientHello` message which is sent immediately after the TCP `ACK`.** Among other things, this message **contains the maximum version of the TLS protocol that the client can support**, and **a list of Cipher Suites that the client is able to use**.
      2. On receiving the `ClientHello` message, the **server responds with a message of its own.** This message includes a `ServerHello`, which **sets the protocol version and Cipher Suite, as well as other related information**. As part of this message **the server also sends its certificate (which contains its public key)**, and a `ServerHelloDone` marker which indicates to the client that it has finished with this step of the handshake.
      3. **Once the client has received the `ServerHelloDone` marker, it will initiate the key exchange process. It's this key exchange process that ultimately enables both the client and server to securely obtain a copy of the symmetric encryption key that will be used for the bulk of the secure message transfer between the two parties.** The exact process for generating the symmetric keys will vary depending on which key exchange algorithm was selected as part of the Cipher Suite (e.g. RSA, Diffie-Hellman, etc). You don't need to worry about the distinctions between these key exchange mechanisms, but as an example RSA works in the following way:
         - The client generates what's known as a **'pre-master secret**', encrypts it using the server's public key, and sends it to the server.
         - The server will receive the encrypted 'pre-master secret' and decrypt it using its private key.
         - Both client and server will use the 'pre-master' secret, along with some other pre-agreed parameters, to generate the same symmetric key.
         - As part of the communication which includes the `ClientKeyExchange` message (e.g. the pre-master secret), the client also sends a `ChangeCipherSpec` flag, which tells the server that encrypted communications should now start using the symmetric keys. Additionally this communication includes a `Finished` flag to indicate that the client is now done with the TLS Handshake.
      4. The server also sends a message with `ChangeCipherSpec` and `Finished` flags. The client and server can now begin secure communication using the symmetric key.
    * As you can see, the TLS Handshake is a fairly complicated process. We certainly don't expect you to memorize every detail of the various steps involved. Instead, try to form a high-level mental model for how it works. Note also that the exact process will vary according to which version of TLS is used. **The key points to remember about the TLS Handshake process is that it is used to:**
      - **Agree which version of TLS to be used in establishing a secure connection.**
      - **Agree on the various algorithms that will be included in the cipher suite.**
      - **Enable the exchange of symmetric keys that will be used for message encryption.**
    * **Something you should be aware of is that one of the implications of this complexity is its impact on performance. The TLS handshake can add up to two round-trips of latency (depending on the TLS version) to the establishment of a connection between client and server prior to the point where any application data can be sent. This is on top of the initial round trip resulting from the TCP Handshake.**
    * Note: there is a protocol called **Datagram Transport Layer Security (DTLS)**, which is based on TLS. This protocol is specifically for use with network connections which use UDP rather than TCP at the Transport layer.

  * ###### Cipher Suites:

    * **A *cipher* is a cryptographic algorithm; in other words they are sets of steps for performing encryption, decryption, and other related tasks. A *cipher suite* is a suite, or set, of ciphers.**
    * TLS uses different ciphers for different aspects of establishing and maintaining a secure connection. There are various different algorithms for performing the key exchange process, as well as for carrying out authentication, symmetric key encryption, and checking message integrity.
    * The algorithms for performing each of these tasks, when combined, form the *cipher suite*. The suite to be used is agreed as part of the TLS Handshake. As part of the `ClientHello` message, the client sends a list of algorithms it supports for each required task, and the server chooses from these according to which algorithms it also supports.

* ###### TLS Authentication:

  * Being able to transfer data in an encrypted form is all well and good, but what if the source of that encrypted data is malicious? For example, you could be communicating with what you think is your bank, but is in fact a third-party impersonating your bank. Having an encrypted communication channel in this situation doesn't keep you secure from that malicious third-party. In fact it could put you more at risk; since the channel is encrypted you might be more willing to share sensitive data such as credit card details. What we need is a means of identifying the other party in our message exchange.

  * **During the TLS Handshake, as part of its response to the `ClientHello` message, the server provides its certificate. As outlined in the Encryption section, part of the function of this certificate is so that the client can use the Public Key contained within it during the key exchange process. Another function of this certificate is to provide a means of identification for the party providing it.**

  * The certificate will contain various pieces of information, including who the owner is. The certificate on its own isn't much proof of anything, however. Since such certificates are publicly available to anyone, a malicious third-party could easily access one and present it as its own. The certificate, and the Public Key it contains, are only one part of an overall system of authentication.

  * The exact way that the Public Key is used during this process varies depending on the Authentication algorithm selected as part of the Cipher Suite. Generally however, this process will be something along the following lines:

    - The server sends its certificate, which includes its *public* key.
    - The server creates a 'signature' in the form of some data encrypted with the server's *private* key.
    - The signature is transmitted in a message along with the original data from which the signature was created.
    - On receipt of the message, the client decrypts the signature using the server's public key and compares the decrypted data to the original version.
    - If the two versions match then the encrypted version could only have been created by a party in possession of the private key.

  * Following a process such as this we can identify that the server which provided the certificate during the initial part of the TLS Handshake as being in possession of the private key, and therefore the actual owner of the certificate.

  * There's still an issue here though. What's to stop a malicious third-party creating their own key pair and certificate identifying them as, say, a well-known bank? Just as it's possible to create a fake ID card in the real world, it's possible to create a fake digital certificate. **How are we to know if a certificate is genuine or not? This is where Certificate Authorities come in.**

  * ###### Certificate Authorities and the Chain of Trust:

    * If you are presented with a piece of identification, you are much more likely to accept it as genuine if it has been issued by a trustworthy source. **When it comes to digital certificates, the trustworthy sources are called Certificate Authorities (CAs).**

    * **When a CA issues a certificate, it does a couple of important things:**

      1. **Verifies that the party requesting the certificate is who they say they are.** The way that this is done is up to the CA and will depend to an extent on the type of certificate being issued. In the case of a domain validated server certificate, for example, it can involve proving that you own the domain by uploading a specific file to a server that is accessible by the domain for which the certificate is being issued.
      2. **Digitally signs the certificate being issued.** This is often done by encrypting some data with the CA's own private key and using this encrypted data as a 'signature'. The unencrypted version of the data is also added to the certificate. In order to verify that the certificate was issued by the CA, the signature can be decrypted using the CA's public key and checked for a match against the unencrypted version.

    * **So who exactly are these Certificate Authorities, and why should we trust them? There are different 'levels' of CA. An 'Intermediate CA' can be any company or body authorised by a 'Root CA' to issue certificates on its behalf.** A widely-used Intermediate CA is Let's Encrypt, who provide free, automated certificates.

    * Google has their own Intermediate CA called Google Internet Authority, who issue certificates for all of Google's own domains. If you view the certificate for [`https://www.google.com`](https://www.google.com/), you'll be able to see this Intermediate CA listed in the Certificate Hierarchy. The way you view the Certificate Hierarchy will vary depending on the browser you use. 

    * ###### The "Chain of Trust":

      * For Chrome, click on the padlock icon in the address bar and in the resulting pop-up menu click on 'Certificate'.
      * In the Certificate Viewer, click on the 'Details' tab. At the top you should be able to see the Certificate Hierarchy.
      * If you select `www.google.com` in the Certificate Hierarchy List and then click on `Issuer` in the Certificate Fields window, the Field Value should show something like `CN = Google Internet Authority G3` (CN here refers to Common Name), which indicates that Google Internet Authority is the issuer of the certificate for `www.google.com`.
      * If you select `Google Internet Authority` in the Certificate Hierarchy List and follow the same process, you should see that the issuer for this certificate is GlobalSign. This is the 'chain of trust' from google.com to Google Internet Authority to GlobalSign.
      * If you do the same thing again to check the issuer of GlobalSign's certificate however, you'll see that this is also GlobalSign. GlobalSign is a **root CA** and its certificate is what's known as a **Root Certificate**. **Root Certificates are 'self-signed', and are essentially the end-point of the chain of trust.**
      * **Client software, such as browsers, store a list of these authorities along with their Root Certificates (which includes their public key). When receiving a certificate for checking, the browser can go up the chain to the Root Certificate stored in its list.**
      * **The purpose of this chain-like structure is the level of security it provides. The private keys of the Root CAs are kept behind many layers of security in order to be kept as inaccessible as possible. As such they don't issue end-user certificates, but leave that up to the Intermediate CAs. Additionally, if the private key of an Intermediate CA somehow became compromised, the root CA can revoke the certificate for the Intermediate CA, therefore invalidating all of the certificates down the chain from it, and simply issue a new one.**
      * **It is necessary that such a 'chain of trust' would need to have an end-point, but if no-one is authenticating the Root CAs other than themselves, how do we know we can trust them? The answer to this is simply their reputation gained through prominence and longevity. Root CAs are essentially a small group of organisations approved by browser and operating system vendors.**
      * Ultimately this system still relies on trust, and as such isn't infallible. In 2015 [Symantec issued some fake Google Certificates](https://www.itpro.co.uk/security/25315/symantec-employees-fired-over-fake-security-certificates). Although the issue was quickly spotted and fixed, it shows that this security infrastructure isn't necessarily 100% reliable.

    * **Certificates are *signed* by a *Certificate Authority*, and work on the basis of a *Chain of Trust* which leads to one of a small group of highly trusted *Root CAs*.**

    * **Certificates are *exchanged* during the *TLS Handshake* process.**

  * Helpful Videos:

    * [Introduction to Cryptographic Keys and Certificates](https://www.youtube.com/watch?v=q9vu6_2r0o4)
    * [Intro to Digital Certificates](https://www.youtube.com/watch?v=qXLD2UHq2vk)

* ###### TLS Integrity:

  * ***TLS Integrity* provides a means of *checking* whether a message has been *altered or interfered with* in transit.**

  * The Encryption and Authentication capabilities of TLS already provide us with a pretty secure system. **To add a further layer of security, TLS provides the functionality to check the integrity of data transported via the protocol.**

  * To get a clearer picture of how this functionality works, we need to take a step back and look at how the TLS protocol encapsulates data.

  * ###### TLS Encapsulation:

    * **The OSI model defines TLS as a Session layer protocol, and so existing in between Application layer (where HTTP resides) and the Transport layer (where TCP resides).** Although, as previously stated, **we're not too interested in the specifics of how the OSI Model defines these intervening layers, when thinking about TLS it can be useful to think of it as operating between HTTP and TCP.**
    * **Just like other protocols we've looked at in this course, TLS sends messages in a certain format. This format can vary depending on the particular function that TLS is performing, but when it is transporting application data TLS encapsulates that data in the same way that we've seen with other Protocol Data Units. In other words, the data to be transported forms a payload, and meta data is attached in the form of header and trailer fields.**
    * **The main field that interests us in terms of providing message integrity is the `MAC` field.**

  * ###### Message Authentication Code (MAC)

    * **The `MAC` field is similar in concept to the checksum fields we've already seen in other PDUs, although there is a difference in implementation as well as overall intention. The checksum field in, say, a TCP Segment is intended for error detection (i.e. to test if some data was corrupted during transport). The intention of the `MAC` field in a TLS record is to add a layer of security by providing a means of checking that the message hasn't been altered or tampered with in transit.**
    * **The way this is implemented is through the use of a hashing algorithm**. It works something like this:
      1. The sender will **create what's called a *digest* of the data payload**. This is effectively **a small amount of data derived from the actual data** that will be sent in the message. The digest is created using a specific hashing algorithm combined with a pre-agreed hash value. This hashing algorithm to be used and hash value will have been agreed as part of the TLS Handshake process when the Cipher Suite is negotiated.
      2. The **sender will then encrypt the data payload using the symmetric key (as described earlier in the Encryption section), encapsulate it into a TLS record, and pass this record down to the Transport layer to be sent to the other party.**
      3. Upon receipt of the message, **the receiver will decrypt the data payload using the symmetric key. The receiver will then also create a digest of the payload using the same algorithm and hash value. If the two digests match, this confirms the integrity of the message.**

