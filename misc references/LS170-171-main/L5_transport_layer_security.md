# [Transport Layer Security](https://launchschool.com/lessons/74f1325b/home)

## [Introduction](https://launchschool.com/lessons/74f1325b/assignments/d62c25d3)

- The simplicity of HTTP (it's just plain text travelling across a network) is also the reason for it's relative insecurity.
- If an HTTP request/response is intercepted it can be easily read.
- It is also difficult to know if an HTTP message has been tampered with, or if its source is trustworthy.
- Security isn't always important, but sometimes it's essential. ie. online shopping, banking etc.
- Security was briefly touched upon in the [HTTP book](https://launchschool.com/books/http/read/security#securehttp)

## [What to focus on](https://launchschool.com/lessons/74f1325b/assignments/3daa92d0)

- TLS is the special sauce we rub on HTTP to make it secure.
- It's too big a topic to cover completely, so to begin with remember these points:
  - TLS allows for secure messages over insecure channels. Begin with an understanding of what a naked HTTP message looks like and then you'll have a better idea of what TLS brings to the table.
  - There are multiple aspects to security. TLS provides a number of services and each one tackles a specific problem.

## [The Transport Layer Security Protocol](https://launchschool.com/lessons/74f1325b/assignments/83bf156b)

- At first TLS was called SSL (Secure Sockets layer), which was developed and owned by Netcat. Renamed and standardized by IETF in 1999.
- People talk about SSL Certificates but what they're talking about is TSL Certificates (AKA Public-key certificates).
- The most recent version is TSL 1.3
- TSL does:
  - Encryption: Encypting a message so that only the person with the matching decryption key can read it.
  - Authentication: A process to identify the identity of a particular person in the exchange.
  - Integrity: Tell whether a message has been tampered with or faked entirely.
- A message doesn't have to use all three of these. You could, for instance, design an app to decrypt messages from a sender without authenticating where the message came from. But in practice, these three services are used together to provide the strongest encryption possible. 

## [TLS Encryption](https://launchschool.com/lessons/74f1325b/assignments/54f6defc)

- TLS sets up an encrypted connection with the "TLS Handshake".

A Brief history of Cryptography:

- The Caeser Cipher
- Blaise de Vigenere (I don't understand this cipher)

### Symmetric Key encryption

- Although cryptography has changed a great deal, the idea of both parties having a common encryption key is still the way it's done.
- A shared key system is called 'symmetric key encryption'

<img width="879" alt="Screenshot 2023-05-07 at 11 08 54" src="https://user-images.githubusercontent.com/78854926/236671235-2c0d72c6-bf76-458c-a2ed-81ed0a6e88ba.png">

- So how do sender and receiver exchange encryption keys in the first place?
- The most secure way would be in person. But over the internet this isn't an option. So we sort of need to encrypt the encryption.

### Asymmetric key encryption:

- (AKA Public key encryption) Uses a pair of keys:
  - A Public key 
  - A Private key.
- Unlike symmetric key encryption, where encryption and decryption both happen with the same key, in asymmetric key encryption the public key is used for encryption and the private key is used for decryption.
- THE MESSAGE IN ENCRYPTED WITH THE PUBLIC KEY, BUT CAN ONLY BE DECRYPTED WITH THE PRIVATE KEY.
- So the public key is visible to everyone, but the private key is only read by the message receiver.
- For example:
  - Crispian wants to receive encrypted messages, so he generates a public and private encryption key.
  - He makes the public key publicly available, but keeps the private key to himself.
  - Ellen writes a message and encrypts it with the public encryption key.
  - She then sends it to Crispian.
  - Crispian has the privtate encryption key and uses it to read Ellen's message.
  - These keys can't work in the opposite direction. Ellen would have to generate her own keys to receive an encrypted response from Crispian.

### The TLS Handshake

- To securely send messages via HTTP we need it to be encrypted both ways. Symmetric encryption would be best, but how?
- By sending the symmetric key  by asymmetric encryption, thus using a combination of both - best of both worlds.
- The set-up with asymmetric keys is called the 'TLS Handshake'.
- TLS assumes that TCP is being used at the Transport Layer. The TLS handshake happens after the TCP (I wrote 'TSL', but that's surely a mistake) handshake.
- The TLS handshake is as follows:
  - A `ClientHello` message is sent after the TCP `ACK`. This contains the maximum version of the TLS protocol that the client can support and a list of cipher suites that the client is able to use.
  - On receiving the `ClientHello` message, the server responds with its own message. This message includes a `ServerHello` message which sets the protocol version and Cipher Suite as well as other related information. The server includes its certificate (which contains its public key) and a `ServerHelloDone`, which tells the client that it is finished with the first part of the handshake.
  - Once the client has received this `ServerHelloDone` marker it will star the key exchange process. This is the process that allows client and server to securely obtain a copy of the symmetric encryption key. The exact process for generating this key varies, depending on which exchange algorithms were chosen as part of the cipher suite. You don't need to worry about these key exchange algorithms, but they give an example anyway.
  - The server also sends a message with `ChangeCipherSpec` and `Finished` flags. The client and server can now begin communicating using their symmetric key.

<img width="880" alt="Screenshot 2023-05-07 at 11 40 08" src="https://user-images.githubusercontent.com/78854926/236672666-8fa33609-310e-4586-a741-16222660f8dd.png">

- The TLS handshake is pretty complicated, you won't be expected to remember all of it. But you should have a high level mental model of how it works. Also the exact sequence of steps will vary depending on which version of TLS is being used.
- Key points about the TLS handshake to remember are that it is used to:
  - Agree which version of TLS is to be used in establishing a secure connection.
  - Agree on the various algorithms that are to be incuded in the Cipher Suite.
  - Enable the exchange of symmetric keys that will be used for message encryption.
- Be aware that this complexity has an effect on performance. The TLS handshake can add 2 round-trips of latency to the establishment of a connection. This is on top of the first TCP Handshake.
- And they make a note of Datagram Transport Layer Seurity, which is based on TLS. This is specifically for use with Network connections that work with UDP rather than TCP at the transport layer.

### Cipher Suites

- A Cipher is a cyptographic algorithm. So it's a set of steps for encrypting/decrypting. So a cipher suite is a collection of these sets of instructions.
- TLS uses different ciphers for different aspects of securing a connection.
- There are many algorithms that can be used for:
  - Performing the key-exchange process
  - authentication
  - symmetric key encryption
  - checking message integrity
- So the collection of cipher algorithms necessary to do all these tasks is the Cipher Suite. This is what is agreed upon in the TLS handshake.
- The `ClientHello` message lists which cipher algorithms it can do for each task and the server checks which algorithms it can also do and chooses from them.

## [TLS Authentication](https://launchschool.com/lessons/74f1325b/assignments/95e698ab)

- So far we have lovely encrypted message. But what if the sender is malicious? You might believe you're talking to your bank, but it could be someone pretending to be your bank. And if you think your encryption is sufficient, you could be sending all sorts of sensitive data.
- We need a way to identify the other party in our exchange.
- During the TLS handshake, the `ClientHello` message contains the server's certificate. This was to give the client the public key, but it has a second function of providing a means for identification.
- The Certificate will say who its owner is and some other things. Obviously this is publicly available, so someone can easily fake one. That's why there are a few more steps to the process.
- Which exact steps depends on which authentication algorithm is chosen as part of the Cipher Suite. But generally it's like this:
  - The server sends a certificate, with its public key inside.
  - The server creates a 'signature' in the form of some data encrypted with the server's private key.
  - This signature is transmitted along with the original data from which the signature was created.
  - On receipt of the message the client decrypts the signature using the server's public key and compares the decrypted data to the original.
  - If the two versions match then the signature could only have been created by a party in possession of the private key.

- All well and good, but what's to stop hackers from creating their own certificate and key-pair in immitation of a well-known bank? It's totally possible to create a fake certificate. This is where Certificate Authorities come in.

### Certificate Authorities.

- In order for Identification to be trustworthy we need to trust its source. For Digital Certificates these are called Certificate Authorities.
- When a CA issues a certificate it does these things:
  - Verifies the party requesting the certificate is who they say they are. The way they do this depends on the CA and the type of certificate. So for example if it's a 'domain validated server certificate' you'd want to prove that the sender actually owns the domain by uploading a specific file to a server that's accessible by the relevant domain. (Like email confirmation I guess).
  - They digitally sign the certificate being issued. This is usually done by encrypting some data with the CA's own private key and using this as a signature. The unencrypted version of the data is also included. This is to prove the certificate was issued by the CA. The signature can be decrypted using the CA's public key and checked for a match against the un-encrypted version.


#### Who are these CAs?

- There are different levels of CA.
- An intermediate CA can be any company or body authorised by a 'root CA' to issue certificates on its behalf. For example a widely used intermediatre CA is called 'Let's Encrypt', who provide free automated certificates.
- Google have their own CA called Google Internet Authority and they issue certificates for all of Google's domains.
- (Have they changes their name to Google Trust Services?)

<img width="1440" alt="Screenshot 2023-05-07 at 12 40 45" src="https://user-images.githubusercontent.com/78854926/236675292-f5ed8395-cae6-4045-bcb2-0a266ac75ebc.png">

- LS says the "chain of trust" should be "Google.com" to "Google Internet Security" to "GlobalSign". But what I'm seeing is "google.com" to "GTS CA 1C3" to "GTS Root R1". 
- The Root CA has the Root Certificate. Root Certificates are 'self-signed' and are the end-point in the chain of trust.
- Client software, like browsers, store a list of these authorities along with their root certificates (with their public keys). When receiving a certificate for checking, the browser can verify all the intermediaries in the list until it gets to the root CA.

<img width="874" alt="Screenshot 2023-05-07 at 12 52 07" src="https://user-images.githubusercontent.com/78854926/236675766-e03924c1-8175-48ff-bae6-6065ef9af357.png">

- This chain-like structure provides great security.
- The private key of Root CAs is closely guarded.
- They don't issue end-user certificates.
- If the private key of an intermediate CA is compromised then the root CA can cut off that Intermediate CA without the rest being compromised.
- The trustworthiness of the root CA comes from a company's reputation and longevity.
- Root CAs are a small group of organizations approved by browser and operating system vendors.
- The system isn't infallible and does ultimately rely on trust.

## [TLS Integrity](https://launchschool.com/lessons/74f1325b/assignments/a88271cf)

- TLS is a "session-layer-protocol" (according to the OSI). So it exists between the Application Layer (where HTTP resides) and the Transport Layer (where TCP resides). Don't get too bogged down with this, but remember TLS operates between HTTP and TCP.
- Just like other protocols TLS sends messages in a definite format. The format can vary depending on the particular function that TLS is performing, but when transporting application data, TSL does it the same way other PDUs do. This means meta-data in the header and footer with a Data Payload.

<img width="863" alt="Screenshot 2023-05-07 at 13 11 06" src="https://user-images.githubusercontent.com/78854926/236676664-0421a8a4-e592-43b4-8ad4-63ca4eecda8a.png">

- For proving message integrity we mainly want to be looking at the `MAC` field (Message Authentication Code). This is different to the MAC address on a computer (Media Access Control Address)

### Message Authentication Code

  - This field is similar to the checksum fields we've found in other PDUs. However there is a difference in implementation and intention. The checksum field in a TCP segment is meant to check for errors, which arise from corruption during transit. But the MAC field in a TLS record is to establish an added layer of security. It means we can check that the message wasn't tampered with in transit.
  - This is done with a hashing algorithm, that works thusly:
 1. The sender creates a 'digest' of the data payload. This is like a small amount of data taken from the actual data that will be sent in the MAC field. It is created using a hashing algorithm combined with a pre-agreed hash-value. These are decided during the TLS handshake.
 2. The sender encodes the data-payload using the symmetric key and encapsulate it into a TLS record. This is then passes down to the Transport layer to be sent to the other party.
 3. When the other party gets the message they decrypt it with the symmetric key. They will also create a digest using the agreed hashing algorithm. If the two digests match then it confirms the integrity of the message.

## [Summary](https://launchschool.com/lessons/74f1325b/assignments/238ff36f)

- HTTP requests are sent in plain text which makes them INHERENTLY INSECURE.
- We can use the TLS Protcol to add security to HTTP communications.
- TLS encryption allows us to encrypt messages so that only those with an authorised means of decoding the message can read it.
- TLS encryption uses a combination of symmetric and asymmetric encryption.
- The TLS handshake is the way that a client and server exchange encryption keys.
- A TLS handshake must be performed before secure data transfer can begin. It envolves several round-trips of latency and therefore has an impact on performance.
- A cipher suite is an agreed set of algorithms used by the client and the servers during the secure message exchange.
- TLS authentication is a means of verifying the identity of a participant in a message exchange.
- TLS authentication is implemented through the use of Digital Certificates.
- Certificates are signed by a certificate authority and work on the basis of a chain of trust, which leads up to a small group of root Certificate Authorities.
- The server's certificate is sent during the TLS handshake.
- TLS integrity allows a way of testing whether a message has been altered during transit.
- TLS integrity is implemented with the use of a MAC (Message Authentication Code).

## [Quiz](https://launchschool.com/lessons/74f1325b/assignments/b0fe5989)

|  | Once | Twice | Thrice | 
| :--- | :---: | :---: | :---: |
|1. | tick |
|2.| tick |
|3.|C, D|
|4. | tick |
|5. | tick |
|6. | tick |
|7. | tick |

3. But also A: The TLS Handshake is used to agree which version of TLS to us.

## [Quiz 2nd go](https://launchschool.com/lessons/74f1325b/assignments/b0fe5989)

| Q | My answer | Correct? | Correction | 
| :--- | :---: | :---: | :---: |
|1. |A,E,F| Tick|
|2. |C|Tick|
|3. |A,C|Cross| Also - The TLS Handshake is used to agree on the Cipher Suite.|
|4. |D| Cross| Other way around: TLS uses asymmetric key encryption for the initial key exchange, and then symmetric key encryption for actual message transfer.|
|5. | A,C,D|Cross| Not D: TLS Authentication is not used to determine if a message has been interfered with in transit, that is the role of TLS Integrity checking.
|6. |A| Cross| and D : Before issuing a certificate, CAs verify that whoever is requesting the certificate is who they claim to be.
|7. | A|Cross| MAC is an algorithmically generated code included in TLS record to provide a means of checking the integrity of the record payload. Not It is an algorithm used for encrypting the keys during the key exchange process.|

## Overview:

|  | Once | Twice (just notes) | Thrice | Comprehension | Retention
| :--- | :---: | :---: | :---: | :--- | :---
|1. Introduction|7/5/23|13/9/23||70%|70%|
|2. What to focus on|7/5/23|13/9/23||70%|70%|
|3.The Transport Layer Security Protocol|7/5/23|13/9/23||70%|70%|
|4. TLS Encryption|7/5/23|13/9/23||70%|70%|
|5. TLS Authentication|7/5/23|13/9/23||70%|70%|
|6. TLS Integrity|7/5/23|13/9/23||60%|70%|
|7. Summary|7/5/23|13/9/23||60%|70%|
|8. Quiz|86%|29%|
| + Read through Discussions |
.
