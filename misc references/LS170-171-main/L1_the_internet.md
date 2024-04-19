# [The Internet](https://launchschool.com/lessons/4af196b9)

## [Introduction](https://launchschool.com/lessons/4af196b9/assignments/89b5fc88)
-  Outlines what the course is
## [What to focus on](https://launchschool.com/lessons/4af196b9/assignments/a6f8ef54)
- Build a general picture of the network infrastructure.
- Be aware of the limitations of the physical network.
- Understand that protocols are systems of rules.
- Learn that IP enables communication between devices.
## [AWS Cloud9](https://launchschool.com/lessons/4af196b9/assignments/fe5b1fbe)
- The argument for AWS at this part of the course & how to install it. (nothing to learn)
## [What is the internet?](https://launchschool.com/lessons/4af196b9/assignments/268243e5)
- A network of networks.
- A network: 2 or more devices connected in such a way that they can communicate or exchange data.
  - At its most basic this is 2 computers connected by a LAN cable.
  - At its most complex it is the whole internet. 
### LAN
- Local Area Network (LAN): A bunch of computers physically near to each other connected by network cables. An office for instance.

<p align="center">
<img width="627" alt="Screenshot 2023-04-07 at 14 11 06" src="https://user-images.githubusercontent.com/78854926/230614563-05bb1e8a-a747-4313-b757-92dce966ad13.png">
</p>

### WLAN
- Your home network is the same, probably with a wireless hub or switch. This is a WLAN.
- The hub or switch is the "local" in LAN.

### Inter-network communication:

- Routers are network devices that can route network traffic to other networks. For a LAN they are the gatekeepers in and out.

<p align="center">
<img width="902" alt="Screenshot 2023-04-07 at 14 25 54" src="https://user-images.githubusercontent.com/78854926/230616710-83b4a14a-7008-484f-b6f8-87db32950e4c.png">
</p>

### A network of networks:

- The intenet is many sub-networks (like your home) connected by routers:

<p align="center">
<img width="898" alt="Screenshot 2023-04-07 at 14 28 33" src="https://user-images.githubusercontent.com/78854926/230617057-6585308d-8a00-473d-9bfb-ce659f456f5d.png">
</p>

## [Protocols](https://launchschool.com/lessons/4af196b9/assignments/a53e65ce)

- The internet is made by many different devices and different softwares. So in order for them to communicate there are rules that govern the way they send and receive messages. These are protocols.
- "A set of rules that govern the exchange or transmission of information."
- There are many protocols. 
- Why?
  - To address different aspects of network communication. (Structure)
  - To address the same aspect of network communication, but for a different use case. (message transfer rules).
- Different aspects of communication could be:
  -  The structure of the message
  -  The order in which messages are sent and received
- Different protocols for the same aspect:
  - speaking to the teacher in a class
  - speaking to a friend in a social setting.
  - To address the same aspect of network communication, but for a different use case.
- TCP and UDP are examples of 2 protocols that control the same aspect of communication differently.

## [A layered system](https://launchschool.com/lessons/4af196b9/assignments/21ef33af)

- Protocols are best grouped together by the aspect of communication they deal with.
- Rather than trying to understand all aspects of communication simultaneously (language, physics, biology, etiquette) there are models for message transfer that aim to deal with everything in a manageable way. The two main ways are :
  - The Internet Protocol Suite
  - The OSI model.
<p align="center">
<img width="738" alt="Screenshot 2023-04-07 at 15 18 37" src="https://user-images.githubusercontent.com/78854926/230624307-5728f0a0-946b-43dd-bac2-2ae6c425f17f.png">
</p>

- The Internet protocol suite divides layers by **scope of communication**
  - Within a Local network
  - between networks
  - etc. 
- The OSI model divides layers by **the function that each layer supplies**
  - Physical addressing
  - logical addressing and routing
  - encryption
  - compression 
 - Both models have their advantages, but no model will perfectly fit real-world implementation.
### Data encapsulation
- A concept used by most network communication models.
- Hiding data from one layer by hiding it within a data-unit of the level below.

### Protocol Data Units
- A block of data transferred over a network.
- Different protocols and different layers within a protocol refer to PDUs by different names. 

| Layer | Name for PDU
| :---: | :---: |
|link/data layer|'frame'
|Internet/Network 'layer|packet'
|Transport layer|'datagram' or 'segment'

- Despite the different names PDUs always consist of a header, a data payload and in some cases a trailer/footer.
- **The header** provides protocol specific meta-data about the PDU.
  - For example an IP packet header would include fields for the Source IP address and the Destination IP address, which would be used to correctly route the packet.
- **The Data Payload** Is the data we want to transfer.
- The entire PDU from a protocol at one layer is set as the data payload for a protocol at the layer below
    - 'below' might be an unhelpful word here. Think more like Russian nesting-dolls. The next layer is the outer-layer in a game of pass the parcel.
  - For example a HTTP request at the Application Layer could be set as the payload for a TCP segment at the Transport layer.
<p align="center">
  <img width="874" alt="Screenshot 2023-04-07 at 15 56 18" src="https://user-images.githubusercontent.com/78854926/230629907-fe2f5ee4-4692-49bc-9274-a049b7999f8b.png">
</p>

- The major benefit of this approach is the seperation it creates between the different layers of the protocol. So each layer needn't know anything about how a protocol at another layer is implemented in order to interact. It does its little job, without worrying about what is happening at the other levels.
- Lower levels do a task for the level above them.
- Sandy's image: A multi-storey sandwich factory. A slice of ham on floor 5 gets thrown down to floor 4, they catch it between slices of bread, throw it down to level 3, they wrap it in cling-film, throw it down to floor 2, they put it in a box, throw it down to floor 1, they put it in a car and drive away.
- The seperation of layers provides a level of abstraction which allows us to use different protocols at one layer without worrying about the other layers.
  - A good example of this is at the Application layer where many different protocols are used depending on the application and use case.
## [The physical network](https://launchschool.com/lessons/4af196b9/assignments/097d7577)
- Everything described above is conceptual abstractions, but when you drill down there is a physical reality to the internet, which is the subject of this chapter.
- These are devices, cables, wires, radio-waves, light-waves, etc. bound by the laws of physics.
- These elements are bound by such questions as 'how fast can an electrical signal travel? How far can a radio-wave reach?
### Bits and Signals
- The OSI model defines its base layer as 'physical', but the IP suite doesn't directly relate to it (although there are some physical interactions in the link layer)
- Either way these interactions are concerned with 'bits' ie binary data.
- For transportation these bits are converted into signals.
### Characteristics of a physical network.
- Latency: The time it takes for data to get from one point to another in a network.
  - If a car drives at 50mph down a 10 mile road, then the road has a latency of 12 minutes.  
- Bandwidth: The amount of data that can be sent in a unit of time (probably a second).
  - Adding more lanes to the road increases bandwidth because the road can deliver more cars, but it does not affect latency because the cars are still constricted by their maximum speed.
  - Increasing Bandwidth doesn't necessarily improve a network's performance.
- Latency is actually a collection of different types of delay. Here are the elements of latency:
  - Propagation delay: The amount of time it takes for a message to get from sender to receiver. 
    - Speed = distance/time
  - Transmission delay: The route taken by the data will involve many different wires, cables, switches, routers etc. The time it takes to get onto the next part of the route adds up and makes the transmission delay. In the analogy of the road, this can be thought of as time spent at roundabouts and interchanges.
  - Processing delay: Data travelling across the physical network doesn't skip unimpeded from one stage to the next. It is processed in various ways. These processes take time and add up to the processing delay. In the road analogy this might be checkpoints along the route, or toll-booths.
  - Queueing delay: Networks can only handle so much data transfer. If the amount of traffic exceeds this then the network queues or buffers the data. This can be visualised as time spent in traffic waiting for the toll-booth/checkpoint.
  - Total latency is the combined milliseconds (ms) of the above.
- Other Latency-related terms:
  -  Last-mile latency: Most of the delays often occur right at the end of the transfer. So entering the LAN. For this reason they are referred to thusly.
  -  Round-trip-time(RTT): Length of time for a signal to be sent + for an acknowledgement/response to be received.
### Network Hops
- `traceroute google.com` traceroute is a utility for displaying the route and latency of a path across a network. Running this command returns a list of the hops taken for the test data to get from your device to the google server. The values printed here are the RTT for each hop
### Bandwidth
- Varies across the network. So, not a constant from start to end.
- The capacity of the core network is much greater than the part that connects to your LAN.
- Where the bandwidth goes from relatively high to relatively low a bottleneck can occur.
- Low-bandwidth can be an issue when dealing with large volumes of data.
- However in many situations latency can be a greater impingement on the performance of a networked application.
### Limitations of physical networks
- As developers we cannot really change the physical reality of the network, but understanding how it works will be useful in designing programs that can make best use of the physicial network.
## [The data/link layer](https://launchschool.com/lessons/4af196b9/assignments/81df3782)
- Yes, the devices are physically connected by cables etc, but they don't know how to talk or where to send their talking. 
- How do we identify the device we want to send our data to? 
- That's the concern of this layer. Finding the device on the physical network and moving the data there.
- For OSI, this is layer 2 between the physical layer and the network layer. For IPS  the link-layer is level 1.
- For both models though we can think of this layer as the bridge between the physical layer and the more logical layer above.
- The most commonly used protocol at this layer is the ethernet protocol.
- (Ethernet cables are used to connect devices such as switches, computers and routers on a network.)
- Two of the most important aspects of ethernet are
  -  framing  
  -  addressing.

### Ethernet frames
- Ethernet frames are a PDU and encapsulate data from the Internet/Network layer above. 
- This layer (the data/link layer) is the lowest layer at which encapsulation takes place. (Because at the physical layer the data is just a stream of bits without structure.
- An ethernet frame adds logical structure to this mass of bits. The data in the ethernet frame is still in bits, but it is structured so the actual data-payload occupies one particular place and the other places are discernable as meta-data for directing the frame.

<p align="center">
<img width="881" alt="Screenshot 2023-04-07 at 17 57 55" src="https://user-images.githubusercontent.com/78854926/230647639-3a0db69b-b177-4fd1-99ed-a27c490d8bdf.png">
</p>

- Ethernet frames are composed of:

#### checksums

| Name | length (bytes) | length (bits) |explanation|
| :--- | :---: | :---: |:--- |
|A preamble| 7 |56|Not really considered part of the frame, but sent just before the frame as a synchronisation measure, which notifies the receiving device to expect frame data and identify the start point of that data. Both preamble and SFD use a repeated pattern that can be identified by the receiving device.
|SFD| 1 |8 |Still not part of the frame, can be considered with the preamble.
|Source MAC address| 6 |48| The address of the device that created the frame. (This can change at various points along the data journey).
|Destination MAC address| 6 |48| The address of the device where the data is ulimately intended to go.
|Length|2 |16| indicates the size of the payload.
|DSAP|1| 8| Identifies the network protocol used for the data payload.
|SSAP|1|8| As above.
|Control|1|8| Provides information for the specific communication mode for the frame (which helps facilitate flow control)
| Data payload | 42 - 1497|| Contains the entire data from the layer above (an IP packet for example)
|Frame Check sequence (FCS)|4|32| A checksum generated by the machine that created the frame. Calculated from the frame data with an algorithm, such as a cyclic redundancy check. The receiving device creates an FSC in the same way and compares the two FCSs. If the two don't match then the frame is dropped. Ethernet doesn't implement any retransmission functionality, that is dealt with by higher level protocols.

### Interframe Gap

- On top of the Preamble and SFD, ethernet also stipulates an interframe gap of about 0.96 microseconds (about a millionth of a second). This gap allows the receiver to prepare to receive the next frame. The length of gap varies according the the ethernet connection's capability.
- The interframe gap becomes part of the transmission delay and thus part of latency.

### Differences between ethernet standards:

- Explanations so far have been of a frame under the  IEEE 802.3 ethernet standard. This is the most popular version, but not universal. Other standards have slightly different framing structures. 
- Some of the fields described above don't exist in earlier ethernet standards.
- That's not important to memorise. What is important is the Data payload field being used as an encapsulation of the layer above and the MAC address fields being used  to direct the frame between network devices. These fields exist across all ethernet standards.

### MAC addresses

- When a network is made of many devices the problem of how to identify where a message came from or is going to becomes real.
- Situation A: Many devices connected by a hub.
#### Hubs
- A hub recevies a message and forwards it to all of the devices on the network. If the message wasn't intended for all devices then this isn't ideal.
  - This is where addressing comes in.
  - Every network enabled device has a MAC address. These are intended to be unique.
  - MAC addresses are formatted as a sequence of 6 two-digit hexidecimal numbers. eg. `00:40:96:9d:68:0a` with different ranges being assigned to different network hardware-manufacturers. 
  - In situation A each device would simply check whether the destination MAC address is theirs, and if it isn't, ignore the message.
 
 <p align="center">
 <img width="880" alt="Screenshot 2023-04-07 at 19 02 25" src="https://user-images.githubusercontent.com/78854926/230655981-355bd43c-d6c6-49c8-94e1-b8eca776a197.png">
</p>

#### Switches

- So obviously hubs are not great. Inefficient. Modern systems rarely use them. They use instead: Switches.
- Switches are devices which connect devices to form a network, BUT they use destination addresses to direct data only to the destination they were intended for.
- It can do this because switches contain a MAC address table. 

 <p align="center">
<img width="883" alt="Screenshot 2023-04-07 at 19 07 39" src="https://user-images.githubusercontent.com/78854926/230656671-d0de6d23-1e4b-49d3-b20d-3e82cb6ff8a7.png">
</p>

- They send the data on through the corresponding data-port and it shoots along to the intended device.
- A MAC address table might look like this:
 
 <p align="center">
<img width="272" alt="Screenshot 2023-04-07 at 19 10 01" src="https://user-images.githubusercontent.com/78854926/230656920-f563c83d-c85a-4441-aa74-e70d1cc3b651.png">
</p>

### A Problem of scale

- The MAC address system is fine for local networks, but not scalable because:
  - MAC addresses are physical, rather than logical. Each address is burned into a device.
  - MAC addresses are flat rather than hierarchical. The entire address is needed and can't be broken down into sections.
- So keeping track of where each device is would be impossible and the lists necessary to know where to send data would be impossibly long.
- If we want to overcome these problems we need a different set of rules. Which is the Internet Protocol. 

## [The internet/network layer](https://launchschool.com/lessons/4af196b9/assignments/b222ecfb)

- In the OSI the network layer is layer 3 between the data-link and transport layers.
- In the IP it is layer 2 (between link-layer and transport-layer).
- The primary function of protocols at this layer is to facilitate communication between hosts (eg. computers) on different networks.
- The IP is the predominant protocol used at this layer for inter-network communication.
- There are two versions of IP at the moment IPv4 and IPv6. This chapter mainly looks at IPv4. Their two main features are:
  - routing capability via IP addressing.
  - Encapsulation of data into packets.

### Data Packets 

-  The PDU within the IP protocol is referred to as a packet.
-  The data payload of a packet will be the datagram/segment from the Transport layer above.
-  The logical separation of meta-data in the header is determined by the set size of each field and their order in the packet.

 <p align="center">
<img width="883" alt="Screenshot 2023-04-08 at 14 50 17" src="https://user-images.githubusercontent.com/78854926/230724752-cd8ad922-5b7c-4dd4-84bf-3ac644be6c61.png">
</p>

Some of the more important header fields are:

- **Version** : The version of IP being used.
- **ID,flags, fragment offset** : These fields are related to fragmentation. Fragmentation occurs when the Transport-layer PDU is too large to be sent as a single packet. It can be sent as multiple packets and then reassembled by the recipient.
- **TTL** : Every packet has a 'Time To Live' value. This is so that if a packet fails to reach its destination it doesn't get stuck bouncing around the network causing problems. The TTL indicates the maximum number of hops a packet can take before being dropped. At each hop the router will decrement the TTL value by one.
- **Protocol** : The protocol used for the Data Payload.
- **Checksum** : An error checking value generated with an algorithm.
- **Source address** : The 32 bit IP address of the sender of the packet.
- **Destination address** : The 32 bit IP address of the intended recipient of the packet.

### IP Addresses:

- Unlike MAC addresses, IP addresses are logical in nature. So they aren't tied to a specific device. Rather they are assigned when they join a network. This address must fall within the range of addresses available to the LAN the device is connected to. This range is determined by a network hierarchy, where a network is split into subnetworks, with each assigned a range of IP addresses.
- IPv4 addresses = 32 bits. These are in 4 sections of 8 bits. When converted from binary to decimal each section allows for a range of numbers between 0 and 255 (because 2 to the power 8 = 256). For example: `109.156.106.57.`
- An example:
  - A LAN has addresses from `109.156.106.0` to `109.156.106.255`. All the addresses between can be assigned to individual devices.
  - The first address (`109.156.106.0`) is assigned to the network address.
    - The network address is used to identify a specific segment of the network.
    - This means that a router which needs to forward an IP packet to an address in the network's range, need only keep a record of which router on the network has access to the segment with that address.
    - This is the logic that creates the hierarchical structure of the IP address.
  - The last address (`109.156.106.255`) is assigned to the broadcast address. (This term is not covered in this course).
 
 <p align="center">
  <img width="906" alt="Screenshot 2023-04-08 at 15 21 47" src="https://user-images.githubusercontent.com/78854926/230726283-ec6bf8fe-3177-4b6e-aa41-46c8bab02cd1.png">
 </p>

- IPv6 uses 128 bit addresses. (8 16-bit blocks)
- The splitting of networks like this is called sub-netting. Sub-nets can be split into even smaller sub-nets to create more tiers in the hierarchy.

### Routing and routing tables

- All routers on the network store a local routing table. When a router receives an address it consults this table and determines where the PDU should go. 

### IPv6

- The structure of IPv4 address means there is a limit to how many variations can occur. (about 4.3 billion). IPv6 is designed to allow for 340 undecillion addressed. The Internet Engineering Task Force (IETF) are creating it. IPv6 uses 128 bit addresses. There are other differences.

### Networked Applications

- The ethernet protocol allows for communication between two devices on a network. The internet protocol allows for communicationbetween two devices any where in the world.
- But device to device communication isn't sufficient. We need multiple applications on one device to simultaneously communicate with multiple applications on the other device. That's what the next lesson is about.

## [Summary](https://launchschool.com/lessons/4af196b9/assignments/6b7df8fb)
## [Quiz](https://launchschool.com/lessons/4af196b9/assignments/d810a100)

 
Overview:

|  | Once | Twice | Thrice |Revise| Comprehension | Retention
| :--- | :---: | :---: | :---: | :--- |:--- | :---
|1. Introduction|4th April| 7th April||7th September '23||
|2. What to Focus on|4th April|7th April||7th September '23||
|3.  AWS Cloud 9|4th April|7th April||7th September '23||
|4.  What is the internet?|4th April|7th April|15th May|7th September '23| 90%|70%
|5. Protocols|4th April|7th April|15th May|7th September '23|80%|40%
|6.  A layered system|4th April|7th April |15th May|7th September '23|85%|50%
|7. The Physical network|4th April|7th April |15th May|7th September '23|85%|55%
|8.  The data/link layer|4th April|7th April |15th May|7th September '23|80%|60%
|9.  The internet/network layer |4th April| 8th April|15th May|7th September '23|70%|50%
|10.  Summary|4th April|8th April|15th May|7th September '23|90%|70%
|11. Quiz |4th April (44%)|7th April (89%) |15th May (100%)|7th September(67%)|
| + Read through Discussions |

# Quiz Mistakes:
- Question 9:
  - An IP is a unique address that we can use to identify a device or host on the internet.
  - IP addresses are represented by 4 sets of numbers, each containing 8 bits of information. The first two sets of numbers usually references the network and sub-network, respectively. The third is the host, and the fourth part references a machine connected to that host. This choice represents the most widely used type of IP address used at the moment, IPv4.
  - There is also a new standard for IP addresses which is in the process of being adopted, IPv6. This representation of an IP address is broken into 8 sets of hexadecimal characters, each containing 16 bits of information. The first 4 sets are used to locate a specific network on the internet. The last 4 sets are typically used to identify a particular interface or device within that network.

# Quiz 7.9.23:

| Question | My answer | correct? | Correction |
| :--- | :---: | :---: | :---: |
|1.| A,B,C,D| yes|
|2.|A,C,E|A,B,E| Different protocols are concerned with different aspects of network communication. + A single network communication typically uses multiple different protocols. The different protocols each provide different services or functionality, and can operate at different network 'layers'.|
|3.|A,B|yes|
|4.|B|yes|
|5.|C| A|Bandwidth is a measure of capacity, in other words the amount of data that can be transmitted over a network connection in a set period of time.|
|6.|A,D|A,C,D|Addressing is a key aspect of Ethernet.|
|7.|A,C| yes|
|8.|A,D| yes|
|9.|A,B,D|yes|
|total| 67%|
