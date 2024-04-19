# [The Evolution of Network Technologies](https://launchschool.com/lessons/be1304f3/home)

## [Introduction](https://launchschool.com/lessons/be1304f3/assignments/78a372ea)

- At this point you should have:
  -  a good general understanding of Networks
  -  A good deeper understanding of HTTP
-  If you're going to develop networked applications, you should have a good idea of what networked communication looks like at a fundamental level.
-  Many of the concepts discussed in this module are unchanging aspects of the internet.
-  On the other hand these concepts are concretely implemented and there are reasons for their design. These details are subject to change.
-  In this final lesson we will look at *why* and *how* they have changed. Also the importance of those changes on the work of devs today.

## [What to focus on](https://launchschool.com/lessons/be1304f3/assignments/7f0ab47d)

- This lesson is background and context. You needn't memorize all the details.
- You should:
  - Be aware of how and why HTTP is evolving.
    - The modern internet is very different from what Tim Berners-Lee imagined.
    - Knowing how HTTP has adapted over time will be useful in understanding the work-arounds possible.
    - This will have an effect on how we build Networked Applications
  - Be aware of the functionality that browser APIs can provide.
    - Browsers have also evolved. Modern browsers provide lots of APIs that extend functionality beyond HTTP. 
    - We need to know what these APIs can bring to the table when developing apps.
  - Be aware that client-server isn't the only network paradigm.
    - Most of this course is about networking between a client and a server. That's what you'll see most of the time, but it's not the only architecture available.
    - This can inform decisions made when designing networked apps.

## [HTTP: Past, Present, and Future](https://launchschool.com/lessons/be1304f3/assignments/a897d764)

- In lesson 4 we looked at different versions of HTTP. Like in the [Speaking the Same Language](https://launchschool.com/lessons/0e67d1ce/assignments/ea90d10b) assignment. HTTP is an evolving protocol.

### HTTP 0.9

- Named this retroactively. (It's only Bad Boys 1 because there's a Bad Boys 2)
- Characterized by its simplicity. A "one line protocol".
- A request only had:
  - A method (GET was the only one available)
  - Path (could only specify the resource on the server since the specific connection was already taken care of by other means).
  - A response would be a single hyper-text document with no headers or meta-data at all.
  - The end of the response was just the server closing the connection.
- Tim BL also created a World Wide Web browser called Nexus, but it only worked on NeXT computers.
- Nicola Pellow, an intern at CERN wrote the line-mode browser. This was more limited than Nexus as it was operated via the command line and outputing in the terminal. On the other hand it was cross-platform. 

### HTTP 1.0

- Between 1991 and 1996 a few things happened that opened up the internet to users:
  - Browser technology improved a lot. The NSCA built on TBL's unportable and basic versions from CERN. They made the Mosaic browser. This allowed the first commercial browser to be developed: The Netscape Navigator 1.0.
  - Telecommunication companies started providing dial-up connections to the inteernet. It only allowed limited bandwidth, so simple text files and images only.
  - 'The World Wide Web consortium' ("W3C") and 'HTTP working group' were founded. These allowed for a framework to be built for documentation and the standardization of web technologies. Plus a structured approach to their continued development.
  - A series of improvements to HTTP. Many of these were somewhat experimental during this period.
- When HTTP 1.0 was documented in RFC1945 it included some important changes:
  - Two more HTTP methods: `HEAD` and `POST`
  - The Request line became more flexible/varied.
  - The Request URI portion of the request could now be a path or an absolute URI.
  - The HTTP version was added to the end of the request line, so that the server receiving the request would know how to interpret it.
  - Responses now included a status line comprised of a status code + status text + HTTP version.
  - HTTP now included headers. This was part of requests and responses becoming more varied and complex and clients and servers becoming more powerful and flexible.
- Many of these developments were in response to changes happening in the internet eco-system. For instance the `content-type` header was created because HTTP needed to deliver content other than HTML.
- This kind of organic evolution of technology is quite common. Often immediate fixes to bugs become permanent features.

### HTTP 1.1

- HTTP 1.0 still had many limitations and problems. Firstly, it wasn't an official standard. Secondly many efficiencies were built-in and couldn't deal with the increasing complexities it had to deal with.
- RFC2068 was released in 1997, then updated in '99. It was the first standard version of HTTP. It tried to resolve some interoperability issues and ambiguities. It also gave a massive performance boost for the new content being produced for the web.
- 1.0 still used a seperate TCP conection for each request-response cycle. If the client had to make a second request, they would have to open a new connection. This may have been sufficient for baby-internet, when pages were just Hypertext documents, but now we were seeing a rise in embedded images, links to CSS stylesheets and JS scripts. (Javascript was added to the browser in 1995) the first CSS was completed in 1996. All of these resources had to be fetched with an individual HTTP request. This was not ideal.
- 1.1 aimed to fix that. One of the big ways was by allowing connection re-use. This reduced latency and allowed for 'pipe-lining' requests. This means a client can send lots of requests before receiving a response. Another way was the implementation of cahce-control mechanisms. (We'll look a these two later)
- HTTP 1.1 also provided more methods:
  - `PUT`
  - `DELETE`
  - `TRACE`
  - `OPTIONS`

### HTTP 2

- Standardized in 2015.
- The new features, improvements and problems solved by 1.1 had now become restrictive for the complexity of modern web applications. Modern web pages rely much more on visual data and embedded files. They also allow interactivity through HTTP in the background, like AJAX.
- This added complexity/interactivity requires many more HTTP requests to be made. It could take dozens of HTTP requests to render a web-page with all its functionality.
- Yes HTTP 1.1 gave us pipelining, but we need more efficiency. Pipelining means the server must respond in the order the requests are received. If one request takes a long time, all must wait. This is called "head-of-line-blocking". HTTP 2 solves this problem by replacing pipelining with multiplexing.
- This version also saves space by compressing headers.

### HTTP 3

- Even though HTTP 2 is a great improvement and hasn't been completely adopted yet, 3 is being built now.
- It aims to solve:
  - The inefficiency of needing to use TCP at the Transport layer.
  - The inefficiency/complexity of relying on TLS to create secure transfers.
- 3 does this with a new protocol called QUIC. QUIC will do the reliability and security that is now covered by TCP/TLS.

### HTTP 3

## [Web Performance and HTTP Optimizations](https://launchschool.com/lessons/be1304f3/assignments/98ecce1c)

- As web devs we need to keep an eye on perfomance and how we can improve it.

### The birth of the modern web

- In the beginning content was delivered by a simple hypertext document and all you could do was read the text. It was simple and simplicity means performance benefits (the entire document only needed a single TCP connection to fetch and load).
- Things became more complex with rich web-pages, but remained non-interactive for the user.
- So the browser receives the multiple documents needed to display a web-page and for each resource sends another request, requiring another TCP connection handshake. This is inefficient.
- Modern web applications use AJAX, Javascript, and more to give us fun interactivity, but this comes at a cost to performance.
- Modern web applications have complicated webs of dependency created with each load.

### Browser Optimisation

- Browsers have their own ways of optimising. There are two types:
  - Document-aware optimisations: The browser can identify and prioritize fetching resources. So the browser can prioritise how it fetches resources, getting the longest ones first (which would be CSS and Javascript).
  - Speculative Optimisations: The browser studies the user's patterns over time and attempts to predict actions. So it might:
    - pre-resolve DNS names
    - pre-render pages to frequently visited sites.
    - Open a TCP connection when you hover over a link.

### Latency as the main limiter

- This course looks a lot at latency because it can be a serious limiter to perfomance.
- Because of the physical distances to be travelled there will always be a base-amount of latency. At the physical layer this is determined by
  - the limitations of the hardware, ie. fibre-optic cables
  - the efficiency of the hardware.
- So if an app is hosted in Malaysia there will be greater latency than if it's hosted in the UK.
- We can't eliminate latency, so we must mitigate it:
  - Get rid of unneccesary round-trips
  - minimize resources to be fetched.
  - add components to our system
  - and more!

### Further optimizations

- This is for what we can do beyond the optimizations automated by the browser, to increase efficency. (I won't do detailed notes here, but...):
  
  1. Consider whether every resource/dependency used by your app is strictly necessary.
  2. Compression techniques: reduce the size of the resources needed to be fetched.
  3. Re-use TCP connections. Use 'keep-alive' connections.
  4. DNS optimizations:
    - Every request to a domain will require a domain lookup. Until it is complete, the browser can't connect to the server and download any resources.
  5. Caching

## [Browser Networking APIs](https://launchschool.com/lessons/be1304f3/assignments/2b0cef9f)

- Modern web-apps are super complex and HTPP can't always deal with it. For this browsers give us networking APIs.
- The HTTP request-response model has limitations with real-time data synchronisation. We'll look at how APIs make up for this.

### HTTP and Real-time data-synchronization

- The request-response model is good at general-purpose user interaction, but it sucks at real-time sync. Real time sync is a 'like' appearing on your post even though you didn't refesh the page. But the RR model requires a request to be sent. So we need an API
  - XHR: 
    - (XML HTTP Request) 
    - (XML is a markup language that defines a set of rules for encoding documents). 
    - XHR is a big part of AJAX, which is used almost everywhere now.
    - We dan do 'polling' which is checking automatically for things. 'long polling' is a more efficient version of this.
    - Popular for "real-time" delivery of data, but it might be out-performed by SSE or WebSocket.
  - SSE
    - (Server Sent Events)
    - Delivers messages over a single long-lived TCP connection.
    - Trade-offs include:
      - Only works with client-server model
      - Doesn't allow for request streaming, like streaming a large upload.
      - Streaming support is designed for UTF-8 data, so binary streaming is inefficient.
  - WebSocket
    - simple and minimal
    - lets us layer and deliver arbitrary application protocols between the client and the server so that either side can send data to each other independently. This is called 'bi-directional communication'.

## [Peer to Peer Networking](https://launchschool.com/lessons/be1304f3/assignments/5a9cbadb)

- This is the client-server model. There can be many clients, but it's always like this:

<img width="622" alt="Screenshot 2023-05-08 at 10 52 30" src="https://user-images.githubusercontent.com/78854926/236793899-d56e49d0-357d-4b44-8523-886b40138934.png">

- Another model is Peer to Peer (P2P)
  - Each computer acts as a node on the network. Each node can do what a client and server can.
  - P2P is about how computers talk to each other, the underlying infrastructure is the same.

### Use cases

Advantages:
  - You don't have to set-up/maintain a server. This decentralization can make the system more resilient. So P2P is good for file-sharing applications.
  - Communication doesn't have to be routed through a central point. This means shorter paths, lower latency. So it's good for video-calling.

### Complexities

- Discovery: finding other nodes on the network. With client-server we can assume that the server should be available. With P2P specific nodes might not always be available, might have different IP addesses, might be offline.
  - A solution to this is 'flooding'. Each node forwards your message and everyone who can respond does respond, until its hops are used up.
  - A Distributed Hash Table (DHT) is a more structured solution.
  - A hybrid model
- Connection negotiation/establishment
- security
- performance
- scaling

### WebRTC

- For video calling.
-  Provides real-time communication functionality within the browser.
-  WebRTC is a collection of protocols, standards and APIs.

## [Optional: Blog Post](https://launchschool.com/lessons/be1304f3/assignments/bebb6461)


|  | Once | Twice | Thrice | 
| :--- | :---: | :---: | :---: | 
|1. [Juliette Sinbardy](https://jsinibardy.com/how-internet-works)| 8.5.23|
|2.[Liz](https://lizfedak.medium.com/how-does-the-internet-work-9238bf40aa87)| 8.5.23|
|3.[Karis' Comic](https://medium.com/launch-school/comic-a-very-basic-explanation-of-how-the-internet-works-db4f67252a14)|8.5.23|
|4.[Vahid pt.1](https://vahid.blog/post/2020-12-15-how-the-internet-works-part-i-infrastructure/)|
|5.[Vahid pt.2](https://vahid.blog/post/2020-12-21-how-the-internet-works-part-ii-layers/)|
|6.[Vahid pt.3](https://vahid.blog/post/2020-12-24-how-the-internet-works-part-iii-reliability-and-security/)|
|7.[Write my own](https://tenor.com/en-GB/view/smiling-javi-gutierrez-pedro-pascal-the-unbearable-weight-of-massive-talent-happy-gif-25135496)|

## [Summary](https://launchschool.com/lessons/be1304f3/assignments/f4934607)

- HTTP is ever growing.
- Most of this growth is driven by the need to improve performance to respond to constantly increasing demands.
- Latency has a big impact on the working of networked applications. You need to be able to optimize this.
- When building apps we can escape the limitations of HTTP functionality with tools and techniques.
- Sometimes P2P architecture might be better than client/server.

## Overview:

|  | Once | Twice (just my notes)| Thrice | Comprehension | Retention
| :--- | :---: | :---: | :---: | :--- | :---
|1. Introduction| 8/5/23|13/9/23|| 100%| -%
|2.	What to Focus On|8/5/23|13/9/23|| -%| -%
|3.	HTTP: Past, Present, and Future|8/5/23|13/9/23|| 100%| -%
|4.	Web Performance and HTTP Optimizations	|8/5/23|13/9/23|| 100%| -%
|5.	Browser Networking APIs	|8/5/23|13/9/23|| 100%| -%
|6.	Peer to Peer Networking	|8/5/23|13/9/23|| 100%| -%
|7.	Optional: Blog Post	|8/5/23|13/9/23|| 100%| -%
|8.	Summary	|8/5/23|13/9/23|| 100%| -%
|9.	Course Feedback|8/5/23|||-| -
