# [Intro to HTTP](https://launchschool.com/lessons/cc97deb5/assignments)

## [What to focus on](https://launchschool.com/lessons/cc97deb5/assignments/cd70ff6d)

- Develop a clear understanding of the role of HTTP (not in isolation, but in context). The web as a combination of inter-woven technologies of which HTTP is one.
- Break things down into individual components. Break concepts like HTTP and URLs into parts in order to ensure clarity of each part's purpose.

## [The Application Layer](https://launchschool.com/lessons/cc97deb5/assignments/c604eb60)

- Bear in mind that the application layer is not the application itself.
- The application can talk to other layers apart from the application layer, but it will mainly talk to the protocols at the application layer.
- The OSI model defines 2 more layers between the application and transport layers. This is because of OSI's emphasis on different functions. We won't look at what those two do right now. 
- A common example of applications communicating with other layers would be an application creating a socket at the Transport layer. But it hardly ever happens that an application would communicate directly with any layer below that.
- The protocols we've looked at so far have been focused on the flow of communications (how messages get from one point to another). Application layer protocols rely on the layers below them to do this and instead deal with the structure of the message and the data it should contain.

### Application layer protocols

- Application layer protocols are rules for how applications talk to each other at a syntactical level.
- As a result there are many different protocols that exist at this level. For example the rules of how an email client communicates with a web-server because emails and web pages are fundamentally different things.
- If you were building an application for transferring files it would likely work with FTP. If you were building an email client it would almost certainly have to use some SMTP along with either POP or IMAP. In this lesson we'll just look at HTTP. That is the primary protocol used in communication on the web.

## [HTTP and the web](https://launchschool.com/lessons/cc97deb5/assignments/e3d85587)

- HTTP is the primary protocol used for  communication on the web (not the internet).
- The internet: A network of networks. The physical infrastructure that enables inter-network communication. Both in terms of the physical network and lower level protocols that control its use.
- The World Wide Web: A service that can be accessed via the internet. A vast information system comprised of resources which are navigable by means of a  URL (uniform resource locator).
- HTTP is tied historically and functionally to the web as we know it. It is the primary way in which applications interact with resources which make up the web.

### A brief history of the web

- The idea for the web was conceived at CERN in 1989 by Tim Berners-Lee.
- His idea was to leverage the internet connectivity along with an emerging technology called Hypertext to create an easily accessible information system.
- This system required uniformity:
  - How the resources were structured
  - How they were addressed.
  - How a request for a resource was made.
  - How such a request would be responded to.
- The way this was achieved combined three technologies: HTML, URIs and HTTP. This was the earliest incarnation of the internet.

- HyperText Markup Language:  The means by which resources in this system would be uniformly structured. This early version of HTML was intended for structuring text documents using headings, paragraphs and lists. It was very basic containing only 18 elements. Of these the most revolutionary was the anchor, `<A>` this used a `href` attribute to provide a link from one resource to another.
  - A Uniform Resource Identifier (URI) is a string of characters which identifies a particular resource. It is part of a system by which resources should be uniformly addressed on the web:
    - The web is an information space. Human beings have a lot of mental machinery for manipulating, imagining and finding their way in spaces. URIs are the points in that space.
  - "URI" and "URL" are often used interchangeably, but they are distinct. (more later).
  - HTTP: is the set of rules which provide uniformity to the way resources on the web are transferred between applications
  - In the beginning it was just text files on the internet, since then it has adapted to include lots more.  

## Assignment: read HTTP book
[my notes](https://github.com/SandyRodger/launch_school_books/blob/main/http_book.md)
## [Some background diagrams](https://launchschool.com/lessons/cc97deb5/assignments/586769d9)

- When you're coding or debugging a web application it's important to be able to see where you are.
- The ability to zoom in to a section of code, while understanding where you are on a larger scale is key to web development.

### Client - server

HTTP: A stateless protocol for how clients communicate with servers.

<p align="center">
<img width="730" alt="Screenshot 2023-04-25 at 14 31 32" src="https://user-images.githubusercontent.com/78854926/234292904-f57fa633-ff6d-46c5-9e4f-22e8c2310af5.png">
</p>

This is every interaction you have with a website.

Here is what is happening at the server:

<p align="center">
<img width="889" alt="Screenshot 2023-04-25 at 14 34 53" src="https://user-images.githubusercontent.com/78854926/234293794-344a2813-8ca3-4b07-8b56-e3783cd25b21.png">
</p>

This is very simplified. Each of these components could be shared across multiple machines, with intermediary machines (like load balancers). So the word 'server' is an umbrella term. Let's look at the three parts in the diagram above:
  - The web server
  - The application server
  - The data store

- A webserver: A server that responds to requests for static assets (files, images, javascript, css). These requests don't require any processing, so can be handled by a simple web-server.
- An application server: Where application or business logic resides. Here, more complicated requests are handled. This is where your server side-code lives when deployed.
    - The application server will consult a persistent data-store, like a relational database, to retrieve or create data. Data stores can also be simple files or key-data stores, document stores or something else
    -  as long as it can save data in some format.
    - Regardless of how it is stored, it can be used to *persist* data between stateless request/response cycles.

### HTTP over TCP/IP

<p align="center">
<img width="902" alt="Screenshot 2023-04-25 at 14 48 52" src="https://user-images.githubusercontent.com/78854926/234297513-d971ea76-5f25-4ba9-9b1b-8e540f6bb1dd.png">
</p>

- This diagram shows that HTTP is actually relying on a TCP/IP connection most of the time, even though they are different protocols operating at different levels.

In summary HTTP operates at the application layer and is concerned with structuring the messages that are exchanged between applications, but it's actually TCP/IP that is doing all the heavy lifting and ensuring that the response/request cycle gets completed between your browser and the server.

## [URLs](https://launchschool.com/lessons/cc97deb5/assignments/a28ccb6f)

- Distinction between URL and URI

### Schemes and protocols

- Scheme names lower-case, Protocol names upper-case.

### URLs and Filepaths

- Much of the content on the web now is generated dynamically.

## [Practice problems: URL components](https://launchschool.com/lessons/cc97deb5/assignments/d69da941)

|  | First go | result | second go | third go 
| :--- | :---: | :---: | :---: | :--- 
|1.a) Host|amazon.com| correct
|1.b) names of the query parameters|B60HON32?ie and qid and sr and keywords| the first one is just `ie`
|1.c) values of the query parameters|UTF8 and 142952676 and 93 and commercial+fridge|correct
|1.d) the scheme|https|correct
|1.e) the path|/Double-Stainless-Commercial-Refrigerator| needs the `B60HON32` from above|
|1.f) the port|443|correct
|2.| http://amazon.com:3000/products/B60HON32?qid=142952676&sr=93| correct
|3.a) the query parameters| none| correct
|3.b)the scheme|http| correct
|3.c)the path|/todos/15| correct
|3.d) the host|localhost| correct
|3.e) the port|:4567| correct
|4.|%20 or +| correct
|5.|?| correct
|6.|=| correct
|7.|&| correct
|results|14/16 or 88%

## [The Request Response Cycle](https://launchschool.com/lessons/cc97deb5/assignments/83ae67aa)

1. What are the required components of an HTTP request? What are the additional optional components?
2. What are the required components of an HTTP response? What are the additional optional components?
3. What determines whether a request should use GET or POST as its HTTP method?


|  | First go | result | second go | third go 
| :--- | :---: | :---: | :---: | :--- 
|1.| Method, (Path, Parameters are optional) Headers, Body| wrong|
|2.| Status, Headers, Body| not exactly
|3.| Get is for fetching data from the server and post is for sending data to the server| Correct
|results|

1. The HTTP method and the path are required, and form part of what is known as the start-line or request-line. As of HTTP 1.0, the HTTP version also forms part of the request-line. The Host header is a required component since HTTP 1.1. Parameters, all other headers, and message body are optional.

Technically speaking the 'path' portion of the request-line is known as the 'request-URI', and incorporates the actual path to the resource and the optional parameters if present. In practice, most people simply refer to this part of the request-line as the 'path'.

2. A status line with a status code is required. Headers and body are optional.
3. GET requests should only retrieve content from the server. They can generally be thought of as "read only" operations, however, there are some subtle exceptions to this rule. For example, consider a webpage that tracks how many times it is viewed. GET is still appropriate since the main content of the page doesn't change.

POST requests involve changing values that are stored on the server. Most HTML forms that submit their values to the server will use POST. Search forms are a noticeable exception to this rule: they often use GET since they are not changing any data on the server, only viewing it.

## [Summary](https://launchschool.com/lessons/cc97deb5/assignments/9f4e349a)

I NEED TO RE-DO THIS PAGE NOTES

- A DNS is a distributed database that maps a domain name to an IP address.
- A URI is an identifier for a particular resource within an information space.
- A URL is a type of URI, but also contains information about how to find the resource.
- URLs are made of scheme, host, port, path and query string.
- Query strings pass aditional data to the server in a HTTP request.
- URL encoding encrypts certain chracters in a URL with an ASCII code.
- URL encoding is used if a character has no corresponding character in the ASCII set. It is unsafe because it is used for encoding other characters, or is reserved for special use within the url.
- An HTTP message takes place between a client and a server and contains:
  - A request:
    - request line
    - headers
    - (optional) body
  - A response
    - status line
    - (optional) headers
    - (optional) body
- Status codes are part of the status line in a response.
- HTTP is a stateless protocol
- Statefulness can be simulated.
- HTTP is inherently insecure.

## [Quiz - 25th April '23](https://launchschool.com/quizzes/7544b995)

| Question |correct?|Correction |
| :--- | :---: | :---: |
|1.|correct| D
|2.|correct|C
|3.|correct|A
|4.|correct|B
|5.|correct|C
|6.|correct|C
|7.|correct|B
|8.|correct|C
|9.|wrong|B,C,D
|10.|correct|C
|11.|correct|B
|12.|wrong|B,C
|13.|correct|A
| Results| 11/13 (85%)|

9. Get requests are also used to retrieve information. POST is also used to submit forms.
12. Statefulness is also simulated by sending data as parameters through a URL

## [Quiz 2nd attempt: 11th September 2023](https://launchschool.com/quizzes/7544b995)

| Question |my answer|correct?|Correction |
| :--- | :---: |:---: | :--- |
|1.|D| no|We use DNS to look up what is typed into a browser, to find a specific domain. DNS uses the domain in the URL typed into the browser to look up the IP address associated with that domain. The IP address is then used to look up the requested resource.
|2.|C|correct|
|3.|A|correct|
|4.|B| correct|
|5.|C|correct|
|6.|B|correct|
|7.|B|incorrect| `+` is also used to signify spaces.|
|8.|A|correct|
|9.|B,C|correct|
|10.|A|incorrect|. HTTP headers are name-value pairs included in a HTTP request or response. Headers act as metadata that provides supplemental information about the request or response to aid the server or client in processing the request or response.
|11.|A,B|incorrect| statelessness also means that each request should contain all the information necessary for the request to be fulfilled.|
|12.|B,C| incorrect| statefulness can also be simulated by sending data as parameters through the URL.|
|13.|B,C,D|correct|
|results|7/13 = 54%|


Overview:

|  | Once | Twice | Thrice | Comprehension | Retention
| :--- | :---: | :---: | :---: | :--- | :---
|1. What to Focus on|11th April|
|2. The Application Layer|11th April|
|3.  HTTP and the web|12th April|
|4. Assignment: read HTTP book|12th - 23rd April|
|5. Some background diagrams|24th April|
|6.  URLs|24th April|
|7. Practice problems: URL components|24th April|
|8. The Request Response Cycle|24th April|
|9. Summary|24th April|
|10. Quiz |25th April (85%)|11th September 2023 (54%)|
| + Read through Discussions |
