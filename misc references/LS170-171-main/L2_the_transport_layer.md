# [The Transport Layer](https://launchschool.com/lessons/2a6c7439/home)

- This layer deals with how networked applications communicate with each other:
  - how transport layer protocols enable communication between processes.
  - Network reliability is engineered. Peel back the abstraction of the internet to reveal tangible processes that result in the internet we take for granted.
  - Understand the trade-offs (particularly between TCP and UDP).

## [Communication between processes](https://launchschool.com/lessons/2a6c7439/assignments/41113e98)

- The Internet Protocol provides the inter-network communication services necessary for "minimum viable internet".
- But to create networked applications we need more than IP.
  - A direct connection between applications.
  - Reliable network communication.
- The IP's system of addressing is designed to provide communication between *hosts*. These hosts can be on the same network or on the other side of the world. IP is great for getting a message from Host A to Host B, but not more than that. 
- Within each host there are multiple applications running.

### Multiplexing and Demultiplexing

- Different apps need to send and receive data simultaneously. We can think of these different processes as channels.

- An IP packet contains one destination MAC address, so everything bundled into that packet is going to the same host. We need a way to transmit these channels/processes/signals all together and then unpack them on the receiving end.

- Multiplexing: Sending multiple signals over one channel.

- Demultiplexing: reversing the multiplexing on the receiving end.

- These processes take place through the use of **network ports**.

<p align="center">
<img width="918" alt="Screenshot 2023-04-08 at 16 43 09" src="https://user-images.githubusercontent.com/78854926/230730288-d8e42e71-38af-450e-8de7-dfa6652cf45d.png">

### Ports

- A port is an identifier (represented by a number between 0 and 65535) for a specific process on a host.

- Sections of this range are reserved for specific things:

| port| purpose| Explanation| Example
| :--- | :---: | :---: | :---: 
| 0 - 1023 | Well-known ports| Assigned to processes that provide commonly used network service| HTTP is port 80, FTP is 20, SMTP is 25
|1024 - 49151|Registered ports|Assigned as requested by private entities| Microsoft, IBM and Cisco all have ports assigned that they use to provide specific services (On some operating systems ports in this range are also used for allocation as *ephemeral* ports)
|49152 - 65535|dynamic (or private) ports|Ports in this range cannot be registered for a specific use. They can be used for customised services or for alloction as *ephemeral ports*|
  
- Services running on a server will most likely be assigned to a port in the well-known range. So if you want to connect via HTTP to a web-server running on a host machine, the web-server process will most likely have port 80 assigned to it.

- This is known as the web server *listening* on port 80.

## Sockets

- In brief they are the combination of IP address and port number, for example 216.3.128.12:8080.  
- It represents an end-point for communication between networked processes.
- At an implementation level it can refer to a few things:
  - A UNIX socket: a way of local processes on the same machine communicating
  - Internet sockets: (like a TCP/IP socket) A way for networked processes on different machines to communicate.
- Weirdly, two processes on the same machine could be using internet sockets to communicate, without actually going out onto the internet.
- Just rememebr there's a difference between the concept of a socket and it's implementation in code.
- In socket programming this involves instantiating a socket object.
- These socket instances are what are created in a connection-oriented protocol to allow a machine to form specific connections for each channel. Every time a new message arrives with a new source address it will be assigned to a new socket. If the message is coming from a source that has already been assigned to a socket it will be passed to that socket. 
- This adds to the reliability of the communication and allows one to manage each communication uniquely, for instance acknowledgements and retransmission of lost messages.
  
## [Network reliability](https://launchschool.com/lessons/2a6c7439/assignments/89636ed4)

- This chapter is all about how the sender and receiver of data in a network can reliably know whether the other end has successfully received the data.
- [The two genreals problem video by Tom Scott](https://www.youtube.com/watch?v=IP-rGJKSZ3s&vl=en)

- Protocols such as the ethernet and internet protocols contain checksum data to prove to the receiver that the data after transmission is the same as when it was sent. But if the data is corrupt they just drop the packet. We need a system that guarantees that a packet of information will be replaced if it becomes lost or corrupt. 
- The possibility of losing data means that the network up to and including the Internet Protocol is effectively an unreliable communication channel.
- As developers we need a reliable communication channel.
- At lower levels our communication channel is unreliable, so how to we ensure reliability?

### Building a reliable protocol

Solution 1:
- Use acknowledgement messages to ensure that the sender knows the transfer was successful.
  - Sender sends one message at a time
  - If message received, receiver sends acknowledgement back.
  - When acknowledgement received, sender sends next message.
 
 <p align="center">
  <img width="855" alt="Screenshot 2023-04-10 at 16 24 26" src="https://user-images.githubusercontent.com/78854926/230932176-575db796-872d-4546-ba3e-bfbb3b05821b.png">
</p>
  
  - Problem 1: If the receiver never gets the message the system fails.
  - Problem 2: If the acknowledgement message is corrupted/lost the system fails.

Solution 2:

- Resend the message if the acknowledgement is not received within a certain time-frame.
  - Sender sends one message at a time and sets a time-out
  - If message is received receiver sends acknowledgement.
  - When acknowledgement is received, sender sends next message.
  - If time-out expires before acknowledgement recieved sender assumes message has been lost and re-sends it. 

<p align="center">
<img width="805" alt="Screenshot 2023-04-10 at 16 30 10" src="https://user-images.githubusercontent.com/78854926/230933136-ec313447-f587-4524-8b7b-23ac93a941db.png">
</p>

- Problem: The receiver receives the message but the acknowledgement becomes corrupt/lost/ delayed to the extent that the sender resends the same message. The receiver is now getting duplicate messages.

Solution 3:

- Add a sequence of numbers (idempotency token) to the message.
  - Sender sends one message at a time with a timer and an idempotency token.
  - If received the receiver sends back an acknowledgement containing the idempotency token, to indicate which message was received.
  - When acknowledgement is received the sender sends the next part of the sequence.
  - If acknowledgement is not received in time the sender re-sends the message with the same idempotency token.
  - If the receiver receives a duplicated token, it resends an acknowledgement with that token and discards the duplicated message.

<p align="center">
<img width="757" alt="Screenshot 2023-04-10 at 16 38 26" src="https://user-images.githubusercontent.com/78854926/230935633-606a6126-29f4-4e0e-901b-5f43c6b4add4.png">
</p>

- This solution covers the fundamental principles of reliable data-transfer
  - In-order delivery: Data is received in the order it was sent.
  - Error detection: Corrupt data is detected with a checksum.
  - Handling data-loss: Lost data is re-sent using a system of acknowledgements and time-outs.
  - Handling duplication: duplicate data is eliminated with an idempotency token system.
- The solution is effective, but inefficient. We can mitigate this inefficiency with:

### Pipelining:
  - Sending multiple messages before receiving acknowledgements.
  - How does that impact reliability? It doesn't, the acknowledgment system is unchanged.
 
 <p align="center">
<img width="865" alt="Screenshot 2023-04-10 at 16 45 31" src="https://user-images.githubusercontent.com/78854926/230938239-75b7ff33-f9e1-40b7-9cb2-742112dfff7d.png">
</p>

- Different ways to pipeline:
  - Go back N
  - Selective repeat
- but the difference isn't important right now.
- With both systems the sender implements a 'window' representing the maximum number of messages that can be 'in the pipeline' at any one time.
- Once it has received an acknowledgement it sends the next message:
 
 <p align="center">
  <img width="802" alt="Screenshot 2023-04-10 at 16 57 28" src="https://user-images.githubusercontent.com/78854926/230940667-5b668c63-aedf-41a3-9115-9a27d1e6cae5.png">
 </p>
 
 [interactive pipelining simulation](http://www.ccs-labs.org/teaching/rn/animations/gbn_sr/)
 
 - Pipelining is a more efficient use of bandwidth. Less time is spent waiting. More time is spent transmitting.
 - Finding a balance between reliability and performance is a key part of the Transmission Control Protocol(TCP)

## [Transmission Control Protocol(TCP)](https://launchschool.com/lessons/2a6c7439/assignments/d09ddd52)

- The transmission control protocol is one of the corner-stones of the internet and one of its key features is providing reliable data transfer.
- TCP provides the abstraction of reliable data-transfer on top of an unreliable channel.
- What this abstraction does is to hide the complexity of reliable network communication from the application layer:
  - Data integrity.
  - de-duplication.
  - in-order delivery.
  - re-transmission of lost data.
- TCP is the protocol of choice for many networked applications because it provides great services.
- The disadvantages of these services are the performance challenges that come with this complexity. (Just because the complexity is hidden from the dev working at the application layer doesn't mean its not there- it's real and does affect performance).
- TCP also provides:
  - Multiplexing
  - Data-encapsulation

### TCP segments
 
 - OK, so TCP segments are just like the PDUs discussed so far. They have a header and a data-payload. They encapsulate the entire PDU of the Application layer above it and are encapsulated by the layer beneath, which is the Internet layer.
 
 <p align="center">
<img width="869" alt="Screenshot 2023-04-10 at 17 15 36" src="https://user-images.githubusercontent.com/78854926/230943883-f9503ff1-9f42-417a-aa54-cc1e1e2830db.png">
 </p>

-  A TCP segment header contains a number of fields:
  -  A Source port and destination port to allow multiplexing capabilities.
  -  Most of the other fields relate to the way TCP provides reliable data transfer.
- A typical TCP segment header might look like this (although bear in mind there are variants, but most will at a minimum contain these fields):
 
 <p align="center">
  <img width="874" alt="Screenshot 2023-04-10 at 21 36 24" src="https://user-images.githubusercontent.com/78854926/230993460-53ce99b1-eb2f-4fdc-a6b6-511ddd018fcb.png">
 </p>
 
 - Some of the more important fields in terms of implementing reliability are:
   - CHECKSUM: this provides the error detection aspect of TCP reliability. It is a value generated by the sender using an algorithm. The receiver generates a value using the same algorithm and if it doesn't match it drops the segment.
   - Other PDUs also use checksum values.
   - Having a checksum at the transport layer pretty much renders checksums at lower layers redundant. This is why ipv6 headers don't include one, assuming that checksums are implemented at either/both the Transport or Link/Data layer.
   - SEQUENCE NUMBER and ACKNOWLEDGEMENT NUMBER: These two fields are used together to provide for the other elements of TCP reliability, such as:
    - In-order delivery
    - Handling Data loss
    - Handling Duplication
  -  Precisely how this happens is beyond the scope of this course (but it looks a lot like the reliable-protocol covered in lesson 1).
  -  WINDOW SIZE: relates to flow control.
  -  FLAGS: are one bit boolean fields.
    -  URG and PSH relate to how the data contained in this segment should be treated in terms of its importance/urgency.
    -  The SYN, ACK, FIN and RST flags are used to establish and end a TCP connection plus manage that connection.

### TCP Connections

- We covered connectionless v connection-based communication. TCP is connection-oriented. (where? - needs link).
- This means it doesn't start sending application data until a connection has been established between application processes.
- In order to establish a connection TCP uses a "three-way-handshake". This involves the SYN and ACK flags.
- FIN is used in a "four-way-handshake" that terminates connections.
- The three way handshake looks like this:
<p align="center">
<img width="893" alt="Screenshot 2023-04-10 at 22 00 23" src="https://user-images.githubusercontent.com/78854926/230997932-0ae70d6a-5d6b-435e-a946-b026ccc957c9.png">
</p>

- So when the sender gets the ACK, it immediately starts sending application data. The receiver has to wait until it has received the ACK to send back any data. This is so that the SYN numbers can be  synchronised.
- One of the main reasons for flags is to manage the *connection state*.
- A connection progresses through a series of states in its lifetime:
  - LISTEN
  - SYN-SENT
  - SYN-RECEIVED
  - ESTABLISHED
  - FIN-WAIT-1
  - FIN-WAIT-2
  - CLOSE-WAIT
  - CLOSING
  - LAST-ACK
  - TIME-WAIT
  - CLOSED (which is a fictional state because it is implied by the connection not existing).
- We are most interested in ESTABLISHED and LISTEN.
- Here is the RFC document for establishing and closing connections which I am not meant to understand, but looks lovely.
```
                             +---------+ ---------\      active OPEN
                             |  CLOSED |            \    -----------
                             +---------+<---------\   \   create TCB
                               |     ^              \   \  snd SYN
                  passive OPEN |     |   CLOSE        \   \
                  ------------ |     | ----------       \   \
                   create TCB  |     | delete TCB         \   \
                               V     |                      \   \
                             +---------+            CLOSE    |    \
                             |  LISTEN |          ---------- |     |
                             +---------+          delete TCB |     |
                  rcv SYN      |     |     SEND              |     |
                 -----------   |     |    -------            |     V
+---------+      snd SYN,ACK  /       \   snd SYN          +---------+
|         |<-----------------           ------------------>|         |
|   SYN   |                    rcv SYN                     |   SYN   |
|   RCVD  |<-----------------------------------------------|   SENT  |
|         |                    snd ACK                     |         |
|         |------------------           -------------------|         |
+---------+   rcv ACK of SYN  \       /  rcv SYN,ACK       +---------+
  |           --------------   |     |   -----------
  |                  x         |     |     snd ACK
  |                            V     V
  |  CLOSE                   +---------+
  | -------                  |  ESTAB  |
  | snd FIN                  +---------+
  |                   CLOSE    |     |    rcv FIN
  V                  -------   |     |    -------
+---------+          snd FIN  /       \   snd ACK          +---------+
|  FIN    |<-----------------           ------------------>|  CLOSE  |
| WAIT-1  |------------------                              |   WAIT  |
+---------+          rcv FIN  \                            +---------+
  | rcv ACK of FIN   -------   |                            CLOSE  |
  | --------------   snd ACK   |                           ------- |
  V        x                   V                           snd FIN V
+---------+                  +---------+                   +---------+
|FINWAIT-2|                  | CLOSING |                   | LAST-ACK|
+---------+                  +---------+                   +---------+
  |                rcv ACK of FIN |                 rcv ACK of FIN |
  |  rcv FIN       -------------- |    Timeout=2MSL -------------- |
  |  -------              x       V    ------------        x       V
  \ snd ACK                 +---------+delete TCB         +---------+
   ------------------------>|TIME WAIT|------------------>| CLOSED  |
                            +---------+                   +---------+

                  TCP Connection State Diagram
                            Figure 6.
```
The three way handshake can look like this:

|Client Start|Client Action|Client End State|Server Start State|Server Action|Server End State
| :--- | :---: | :---: | :---: | :--- | :---
|CLOSED|Sends a SYN segment|SYN_SENT|LISTEN|waits for a connection request|-
|SYN-SENT|waits to receive an ACK to the SYN it sent, as well as the server's SYN|SYN-SENT|LISTEN|Sends a SYN-ACK segment which serves as both its SYN and and ACK for the client's SYN.|SYN-RECEIVED
|SYN-SENT|Receives the SYN-ACK segment sent by the server and sends an ACK in response. The client is now finished with the connection establishment process|ESTABLISHED|SYN-RECEIVED|waits for an ACK for the SYN it just received|-
|ESTABLISHED|Ready for data transfer. Can start sending application data|ESTABLISHED|SYN-RECEIVED|Receives the ACK sent in response to its SYN. The server is not finished with the connection establishment process.|ESTABLISHED|

- You don't need to memorise this but remember:
  - There is fair amount of complexity in how TCP handles connection state.
  - This is particularly true at the establishment of a connection, where the key thing to remember is that the sender cannot send any data until it has sent the ACK segment.
  - What this means is that there is an entire round trip of latency before any application data can be exchanged.
  - Since this hand-shake process happens every time a TCP connection is made this has a big impact on any application which uses TCP at the transport layer.

<p align="center">
<img width="906" alt="Screenshot 2023-04-10 at 22 28 55" src="https://user-images.githubusercontent.com/78854926/231002601-a0354a55-22de-487d-ad8c-3ebb948b0081.png">
</p>

- So TCP involves a lot of costs in terms of establishing a connection and providing reliability through the retransmission of lost data.
- To deal with this we have to be as efficient as possible with the functioning of data-transfer. To speed things up once a connection is established TCP implements mechanisms for flow-control and congestion-avoidance.

### Flow Control

- The aim of this is to prevent the sender from overloading the receiver.
- The receiver can only process a limited amount of data in a time-frame.
- Data awaiting processing is stored in a "buffer"
- buffer size depends on the amount of memory allocated. That depends on the configuration of the OS and physical resources available.
- Each side of a connection can tell the other side how much data it is willing to receive with the WINDOW field. This number is dynamic so it can change during the course of a connection.
- If the buffer is getting full then it can send a lower window size.
- Flow control means the sender and receiver don't overwhelm each other, but they can still overwhelm the underlying network. For that we need congestion avoidance.

### Congestion Avoidance

- Network Congestion happens when there is more data being transmitted on the network than the network has capacity to process. It's like gridlock on the roads. But instead of things jamming up the excess vehicles disappear.
- IP packets move accross a network in a series of hops and at each hop the packet needs to be processed.
  - The router runs a checksum on the data to make sure it's OK.
  - It also checks the destination to work out how best to send it.
- Routers use a buffer to store data, but overflow is dropped.
- TCP retransmits lost data. If lots is lost, lots is re-transmitted, which is inefficient.
- TCP uses data-loss as a metric by which to detect and avoid network congestion.
- If lots of re-transmissions are occuring TCP reduces the size of the transmission window because congestion has been detected.
- There are different algorithms for detecting and establishing the transmission window.

### pros and cons of TCP

Pros:
  - Reliable data transfer
  - Uses flow control and congestion avoidance techniques.

Cons:
  - Latency overhead in establishing a connection with the handshake process.
  - Head-of-Line (HOL) blocking.

- HOL blocking isn't specific to TCP. Basically it is about how processing one message in a sequence can block the processing of subsequent messages in the sequence.
- TCP's provision of in-order delivery (or segments) can cause HOL blocking. If one segment goes missing, it jams transmission for the subsequent segments and needs to be buffered. This can lead to increased queueing delay, which adds to latency.

## [User datagram protocol (UDP)](https://launchschool.com/lessons/2a6c7439/assignments/9bb82c9b)

- If TCP implements reliable data transfer through sequencing and re-transmission of lost data, how does UDP do this? It doesn't.
- The PDU of UDP is a datagram.
- Datagram headers look like this:
<p align="center">
<img width="873" alt="Screenshot 2023-04-11 at 12 17 01" src="https://user-images.githubusercontent.com/78854926/231144645-799e39a8-4cef-41de-9ae8-ddb5d55de526.png">
</p>

- So only 4 fields:
  - Source port
  - Destination port
  - Checksum (optional if using ipv4 at Network level)
  - Length
- With the source and destination ports UDP can multiplex in the same way TCP does. But unlike TCP it doesn't do anything to resolve the unreliability of lower layers.
- What UDP *doesn't* do:
  - provide a guarantee of message delivery.
  - provide a guarantee of message delivery order.
  - provide a built in congestion avoidance or flow control mechanism.
  - provide connection-state tracking (since it is a connectionless protocol).

### The case for UDP

- UDP provides simplicity, which means:
  - speed
  - flexibility
- As a connectionless protocol applications using UDP can just start sending data straight away, without having to wait for a connection to be established.
- The lack of acknowledgements and retransmission means the actual data delivery is faster. Once a datagram is sent, it doesn't need to be sent again.
- Latency is less of an issue since without retransmission data essentially travels only one way.
- The lack of in-order delivery also prevents HOL blocking.
- It's probable that someone using UDP will implement for themselves some of the features UDP lacks. Which services those would be and how they are implemented would be up to the person writing the application code.
- For example you might want to implement in-order delivery, but not worry too much about losing the odd bit of data. In this case you would implement sequencing, but not re-transmission or lost data. These services can be implemented at the application layer. This is like using UDP as a base template on which to build.
- An example of this would be a voice/video calling app. The occasional lost piece of data means glitching, but its worth it for the speed of the connection over long distances (which would normally mean higher latency). Online gaming is another good example.
- So UDP provides all this freedom, but comes with responsibility. Various practices should be adhered to, for example: implementing your own congestion avoidance in order to prevent it overwhelming the network.

## [Summary](https://launchschool.com/lessons/2a6c7439/assignments/4ab0993c)

- Multiplexing/demultiplexing allow multiple signals to be sent over a single channel
- Multiplexing is enabled through the use of network ports.
- Network sockets are a combination of network port and IP address.
- At the implementation level network sockets can also be socket objects.
- The underlying network is inherently unreliable, so if we want reliable data transfer we should implement a system of rules (at the application layer?)
- TCP
  - is a connection-oriented protocol. It establishes a connection using a three-way handshake.
  - provides reliability through message acknowledgement/retransmission and in-order delivery.
  - provides Flow-control and congestion avoidance.
  - has the disadvantages of 
    - high latency overhead in establishing a connection.
    - potential HOL blocking as a result of in-order delivery
- UDP is
  - Very simple compared to TCP
  - Provides multiplexing, but 
    - no reliability.
    - no in-order delivery.
    - no congestion/flow-control
  - Is connectionless, so doesn't need to establish a connection before it starts sending data.
  - Despite its unreliability it is
    -  fast
    -  flexible

Overview:

|  | Once | Twice | Thrice | Comprehension | Retention
| :--- | :---: | :---: | :---: | :--- | :---
|2. What to Focus on| 6th April | 8th April | 9th September |
|3.  Communication between processes| 6th April | 9th April|  9th September |
|4.  Network Reliability| 6th April |10th April|  9th September |
|5. Transmission Control Protocol| 6th April |10th April|  9th September |
|6.  User Datagram Protocol| 6th April |11th April|  9th September |
|7.  Summary|6th April |11th April|  9th September |
|8. Quiz | 11th April (100%) (open-book)| 9th September (14%) (closed-book)|
| + Read through Discussions |


## [Quiz](https://launchschool.com/quizzes/e539d784) (9th September 2023)

| Question | My answer | Correct? | Correction |
| :--- | :---: | :---: | :---: 
|1.| A,B | no, just B| Multiplexing and demultiplexing DO NOT provide communication between hosts, or devices, on a network.|
|2.| B,D,E,F| no, just B, D, E | A port number is NOT part of an IP address.|
|3.|B,C,D| no, A as well | A socket is the combination of IP address and port number.|
|4.|A,D,E,F|no, also C and G| TCP provides multiplexing and demultiplexing AND TCP provides error detection |
|5.|B,D| no, B, C, G| UDP provides multiplexing and demultiplexing AND UDP DOES NOT provide in-order delivery AND UDP provides error detection|
|6.|E| yes |
|7.|A| no, B | Congestion avoidance is a process by which TCP uses data loss (based on the volume of retransmissions required) as a feedback mechanism to determine how congested the network is, and adjusts the amount of data being sent accordingly.|
|8.|B| no, A | Flow Control is a mechanism to prevent the sender overwhelming the receiver with more data than it can process. Each participant in a connection lets the other participant know how much data it is willing to accept using a field in the TCP header.|
|total| 14%|

