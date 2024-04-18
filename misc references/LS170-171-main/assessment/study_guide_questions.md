(These are derived from [the study guide](https://launchschool.com/lessons/f48bf303/assignments/adbc20a4))

1. [What is the internet](https://launchschool.com/lessons/4af196b9/assignments/268243e5) is and how does it work?

 - The internet is a network of networks. Devices are connected to each other in various ways that enable them to transfer data. The first network your device connects to is the Local Area Network, which could be a home or office. At this point the data travels from your device to a network bridging device, such as a hub or switch. To connect your LAN to the wider internet your switch/hub sends the data on to a router. Routers are devices that exist to send data on to other machines on the internet. All of this data transferred is formatted according to protocols so that all devices know the agreed ways to read the messages. There are many protocols, but the first and most famous is Hyper Text Transfer Protocol (HTTP). Each message (or ‘packet’) between devices is a combination of different messages doing different jobs and these are organised in layers like Russian-nesting-dolls. Each layer will have a header (containing information about the packet) and a pay-load (which is the actual message). The packet is sent on a physical network as light signals or electrical signals or radio-waves. There’s much more to talk about such as DNS servers,  the client-server model, URLs and encryption, but I’ll stop there.


2. How does the internet differ from the world wide web?

- The internet is the physical infrastructure of devices linked with switches, hubs, routers, servers etc. The World Wide Web is a service provided on that infrastructure. So a web-page is part of the web, but a laptop is part of the internet. Allegories would be a book and the text or a road network and the shops/houses.

3. What are the characteristics of the physical network such as latency and bandwidth?	

-	As data travels between points on the internet the efficiency with which it can do so is measured in these two ways. Latency is the amount of time it takes. Bandwidth is how much data can be sent in a given time-frame. It’s comparable to a train having a maximum speed, but how big the train is also affects total passengers transported.

4. Explain how lower level protocols operate.

-	The layers of PDUs as they travel across the internet are conceptual aids for people and not strictly how the information is organised. Higher level protocols would be the Application and Transport layers and lower level protocols would be Network, Data-link and Physical layers.
-	Each layer of the PDU encapsulates the data for the layer below and the same in reverse.
-	Each layer operates independently of other layers. It completes its specific task and then passes the result to the next layer. During encapsulation this means taking the data from the layer above and passing it to the layer below. For instance, according to the TCP/IP model (Transmission Control Protocol / Internet Protocol) this would be the Internet layer taking the data from the Transport layer and passing the result of its encapsulation to the Link Layer.


5. What is a port address and an IP address	?

- [Relevant LS page here](https://launchschool.com/lessons/2a6c7439/assignments/41113e98)
- An IP address is a series of numbers between 0 and 255 representing a device’s address on the internet. It is what is used to direct traffic to the required destination. It only takes the information as far as the host. Once it has arrived the data needs to know which application it should go to. This is what ports are for. The PDU is directed to a specific port on a host so that multiple channels of communications can be maintained at once.  This allows multiple channels of communication between applications to be maintained on a single channel between hosts, which is called multiplexing.

6. How does DNS work?

- [DNS](https://github.com/SandyRodger/launch_school_books/blob/main/http_book.md#dns)
- DNS (Domain Name System) is a distributed database that takes a website name and finds its corresponding IP address. DNS databases are stored on DNS servers.
-	If a DNS server doesn’t contain the address it passes it up the hierarchy chain to the next DNS server and searches that.
-	It then sends back the IP address to be used in your PDUs. IP addresses are often saved in a browser cache, so if your browser already has the IP address it won’t search the DNS database.

7. What is the client-server model of web interactions and the role of HTTP protocol as a protocol within that model?

- Most data transfer on the internet happens between two hosts where one host is requesting something and the other is responding to that request. This is called the client-server model. HTTP is a set of rules for how messages between points on the internet should be formatted so that each side knows how to parse the information is receives.

9. Explain the TCP and UDP protocols, their similarities and differences	

- TCP and UDP are protocols for data transfer at the transport layer. Their purpose is to make data transfer reliable even with HTTP, which is inherently unreliable.
- It abstracts reliable network communication away from the Application layer. So it takes care of de-duplication, data-integrity, in-order delivery and re-transmission of lost data.
- As well as taking care of reliability, TCP also deals with encapsulation and multiplexing, through th use of TCP segments.
- TCP is a connection oriented protocol. It uses a 'three-way handshake' system to establish a connection before it starts sending data.
- TCP does its job well, but this comes at a cost to performance. 
- UDP on the other hand does not guarantee message delivery, guarantee message delivery-order, have a built in congestion avoidance/ flow-control mechanism or provide connection state tracking.
- UDP's advantages are speed and flexibility. It allows, but to some degree also requires, a developer to implement their own forms of the features it lacks.

11. Explain the three-way handshake and its purpose.

-  This is a process of establishing a connection between application processes. It is implemented with TCP. To do this the sender sends a SYN segment (to synchronise), the receiver sends back a SYN ACK segment (acknowledging receipt of the SYN segment) and the sender sends back an ACK segment and starts transmitting data.

12. What are flow control and congestion avoidance?

-  Flow control is a mechanism to prevent the sender from overwhelming the receiver with too much information sent too quickly.
-  Congestion avoidance is everything done to avoid network congestion, such as monitoring retransmission, which indicates data-loss from routers, to detect congestion. In response it decreases the transmission window which is the amount of data it is transmitting in a given time. 

13. What are the components of a [URL](https://launchschool.com/lessons/cc97deb5/assignments/a28ccb6f), including query strings([also here](https://launchschool.com/books/http/read/what_is_a_url))

- URL stand for Uniform Resource Locator and is a type of URI (Uniform Resource identifier) which acts as an address for a resource on the internet. They are composed of:
 - the scheme
 - the host
 - the port
 - the path
 - the query string (made of query parameters)

14. Construct a valid URL.

 - `http://www.website-name.com:400/home?member=one&admin=first`
 - `http` :  this is the scheme
 - `://`  :  the scheme is always followed by a colon and two forward slashes
 - `www.website-name.com` : this is the host name. It tells the client where the resource is located.
 - `:400` : this is the port name. It is optional and the default port is 80.
 - `/home` : this is the path, indicating what local resource is indicated. It is optional.
 - `?member=one` and `admin=first` : These are the query parameters, used to send data to the server. It is optional. `?` marks the start of the query string. `member=one` and `admin=first` are parameter name/value pairs. `&` is a reserved character used when adding more parameters to the query string.

15. What is [URL encoding](https://launchschool.com/books/http/read/what_is_a_url#urlencoding) and when it might be used?

- URLs can only be written with the 128 ASCII characters so if a URL requires a character other than these there is a code to include them. The code is a `%` symbol followed by two hexadecimal numbers that represent the desired character as UTF-8 code. For example `%20` is space. 
- Characters must be encoded if they don't exist in the ASCII set, but also if the character has a special function or could be misinterpreted some systems.

16. What are HTTP requests and responses? Identify the components of each.

 - A HTTP request is what is sent when you look up a resource on the internet and the response is what you get back. The response is then parsed by the host and displayed as a webpage.
- A HTTP request must include a HTTP method, such as GET, and a path, for example `www.launchschool.com`. These form the 'start-line' of the request and also include the HTTP version. The host header is also a required component, since HTTP 1.1.  Parameters, all other headers and the message body can then be included, but are optional.
- The HTTP response must include a status line with a status code (for example `200 OK`). Headers and body can be included after that, but are optional. 
- A header could be `Content-type: text/html`. A Body would be written in HTML, so `<html><body>...>

17. Describe the [HTTP request/response cycle](https://launchschool.com/lessons/cc97deb5/assignments/83ae67aa)

- When a browser wants to look up a web-page it sends a HTTP request to a server. The sender is the client in this relationship.
- This is the first step in a HTTP request/response cycle and is usually initialized by a user interaction.
- The server is the software running on the machine hosting the information requested.
- When the server receives the request it will perform any necessary checks, like verifying the user session. Then look up the requested information and format it as a HTTP response.
- The client then receives this HTTP response and renders it for the user.

18. Explain what [status codes](https://launchschool.com/books/http/read/processing_responses#statuscode) are, and provide examples of different status code types.

- Status codes are a 3 digit code with some text in a HTTP response indicating whether the server was able to retrieve the requested information. A `200 OK` status code means the request was handled successfully. `302 Found` indicates that the requested resource has changed, but was found. This usually results in a redirect to another URL. `404 Not Found` means the resource was not found. `500` means the server encountered an error, which could be anything from a  bug to a misconfiguration.

19. What is meant by 'state' in the context of the web, and explain some techniques that are used to simulate state.

- HTTP is a stateless protocol. This means that it does not hold on to information between request/response cycles and HTTP request/responses are not aware of each other. However, sometimes it is necessary for a website to behave as though it does retain this information. For example navigating from one part of a website to another involves sending a new HTTP request, but you don't want to log in every time you do this. 
- Web developers simulate stateful websites in a few ways. Three common tools for this are sessions, cookies and Asynchronous Javascript calls (AJAX).
- Sessions are when the client sends a 'session identifier' token which the server remembers and then uses to load the webpage settings specific to that user.
- Cookies are pieces of data that are sent from the server and stored on the client's browser during a request/response cycle. These files contain information about the session. The actual session data is saved on the server, but the cookie contains information used to identify the client to the server so it can load the right page.
- AJAX is a system that allows broiwsers to issue requests and process responses without refreshing the entire web-page. It means that client requests are performed asynchronously, which just means that the page doesn't refresh. A good example of AJAX is typing each letter into the google search bar, which generates new suggestions after each letter, even though we aren't refreshing the entire page. These suggestions are the result of a 'call back', which is a piece of logic that is triggered when the response is returned instead of rendering a whole HTML webpage.

20. Explain the difference between GET and POST. When is each appropriate?

- GET and POST are HTML request methods.
- GET is used for retrieving a resource and can be initialized by clicking on a link or entering an address into a web-browser. The response to this can be anything, but if it's HTML and references another resource your browser with automatically request that resource.
- POST is for initiating an action on the server, or submitting information. POST requests allow us to send much larger and more sensitive information to the server, like images or videos. The reason it's better than putting the same information into a GET query string is that the information would be exposed in the URL. (There is also a query string size-limit).
- When issueing a POST request from a browser the following sequence of actions are hidden:
 - Browser issues the original POST request.
 - The server sends back a responce with a `location` header.
 - The browser then sends another POST request (without any input from the user)
 - Browser receives second response and displays it.

21. What are the various [security](https://launchschool.com/books/http/read/security#securehttp) risks that can affect HTTP?
22. What measures can be used to mitigate against these risks?

- Session Hijacking is when a hacker gains access to the session id token, which allows them to access the same web application as the user. There are a few ways of preventing session hijacking:
  - Resetting sessions: This typically happens when a user is entering a part of the website with sensitive information or performing a task which requires greater security. For instance transferring money. The new session would have a new session id token and render the previous session invalid.
  - Having an expiraton time on sessions limits the access hackers have to exploit a session.
  - Using https across the app.
- Packet sniffing techniques: Requests and responses are sent as strings, so if hacker had access to the network they could use packet-sniffing techniques to read the packets. Requests contain the session id, so the hacker would be able to pretend to be you on the server. This would be like being logged in as you, without the need for your username or password. The best way to protect against this is using the `https` protocol, which encrypts every request/response before it is sent. These encryptions rely on TLS, the cryptographic protocol.
- Same origin policy is a security policy that restricts certain interactions between cross-orgin resources. That means that resources with the same scheme, host and port are granted unrestricted access accross the website, but not if any of these three are different. Bear in mind it's not all cross origin requests. Linking, redirects and form-submissions are generally allowed. The things which are restricted are more often trying to access information.
- XSS (cross site scripting) is an attack that happens when you allow users to input html or javascript that ends up being displayed by the site directly. If the server-side code doesn't protect against this the browser will interpret this as html/javascript. This can be used to do great damage, like grabbing the session id of every visitor to the page and then coming back to assume their identity.
- XSS can be fought in a few ways:
  - Making sure to always sanitize the user input. This is done by disallowing languages like html and javascript and illiminating script tags like <script>.
  - Another way is to escape all user input. Escaping here means replacing html characters with a combination of ASCII characters. These combinations of ASCII characters are called html entities.

23. What are the different services that TLS can provide, give a broad description of each of those services
 
- Encryption: this is encrypting a message so that only the person with the corresponding key can decrypt it.
- A secure connection is formed by performing the TLS handshake, after the TCP handshake.
  - The TLS connection is established with the TLS 3-way handshake. This goes as follows:
    1. After the TCP handshake is complete and the TCP ACK message has been sent a `ClientHello` message is sent by the client. The `ClientHello` message contains:
      - the maximum version of the TLS protocol that the client can support and 
      - a list of cipher-suites that the client can perform.
    2. The server responds with a message, including a `ServerHello` message. The `serverHello` message sets the protocol version and the cipher-suite. Also this message contains the server's certificate (containing the opublic key) and a `serverHelloDone` mearker, which indicates that this part of the handshake is complete.
    3. This is when the client begins the key exchange process.
  - TLS uses asymmetric and symmetric key encryption. 
    - Asymmetric is when a user generates a public and a private encryption key. The public encryption key is used to encrypt a message by the sender but the message can then only be decrypted with the private key. So the messages can only securely go one way.
    - Symmetric is when both parties use the same private key. The way that both parties can have access to this key without it having been intercepted is by exchanging the key with asymmetric encryption.

 
 
- Authentication: A process of checking the identity of a person in an exchange.
- Integrity checks: Checking if the message has been tampered with or faked completely.
 
 
