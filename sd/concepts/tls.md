## How ESNI works

ESNI (Encrypted Server Name Indication) is an extension to the TLS (Transport Layer Security) protocol, designed to protect the privacy of the Server Name Indication (SNI) extension during the TLS handshake. Here's how ESNI works:

Client initiates a TLS connection: A client initiates a TLS connection to a server by sending a ClientHello message, which includes a list of supported TLS extensions.

Server responds with a ServerHello message: The server responds with a ServerHello message, which includes a selected cipher suite and a list of supported TLS extensions.

Client sends ESNI key share: The client sends an ESNI key share extension in the ClientHello message, indicating its support for ESNI and providing a key share value.

Server sends ESNI key share: The server responds with an ESNI key share extension in the ServerHello message, indicating its support for ESNI and providing a key share value.

Client encrypts SNI: The client encrypts the SNI extension using the shared ESNI key and includes it in the encrypted extensions field of the ClientHello message.

Server decrypts SNI: The server decrypts the SNI extension using the shared ESNI key and reads the hostname to which the client wants to connect.

Server responds with encrypted data: The server responds with encrypted data, which is encrypted using the negotiated cipher suite and the shared ESNI key.

Client decrypts the data: The client decrypts the data using the negotiated cipher suite and the shared ESNI key.

By encrypting the SNI extension, ESNI prevents an attacker from intercepting and reading the SNI extension, protecting the privacy of the client's browsing activity. The use of ESNI also provides a more secure method for using encrypted DNS protocols, such as DNS over HTTPS (DoH) or DNS over TLS (DoT), since the SNI extension cannot be intercepted and used to determine which website the client is accessing.




## What if attacker intercepts the SNI
If an attacker intercepts the SNI (Server Name Indication) during the TLS handshake, they can use it to determine the hostname of the server the client is trying to connect to. This information can be used to perform various types of attacks, such as DNS spoofing, IP address spoofing, or man-in-the-middle attacks.

In a DNS spoofing attack, the attacker can use the intercepted SNI to redirect the client to a different IP address, which could be a fake website or a website controlled by the attacker. The attacker can also use the SNI to determine the IP address of the server hosting the website, which can be used in other types of attacks.

In an IP address spoofing attack, the attacker can use the intercepted SNI to determine the IP address of the server hosting the website and then spoof the IP address to intercept or modify the communication between the client and server.

In a man-in-the-middle (MITM) attack, the attacker intercepts the communication between the client and server, decrypts it, and then re-encrypts it with their own SSL/TLS certificate. This allows the attacker to read or modify the communication between the client and server, potentially stealing sensitive information such as passwords or credit card numbers.

To prevent these types of attacks, it is important to use secure protocols such as TLS with SNI encryption (ESNI) and encrypted DNS protocols like DNS over HTTPS (DoH) or DNS over TLS (DoT). By encrypting the SNI and using encrypted DNS protocols, it becomes much more difficult for attackers to intercept or modify the communication between the client and server, protecting the privacy and security of users on the internet.







## What is ESNI

ESNI stands for Encrypted Server Name Indication, and it is an extension to the TLS (Transport Layer Security) protocol. ESNI is designed to protect the privacy of the server name during the TLS handshake by encrypting the Server Name Indication (SNI) extension.

During the TLS handshake, the client sends an SNI extension in plain text to indicate the hostname of the server it wants to connect to. This SNI extension can be intercepted by an attacker who can use it to determine which websites the client is connecting to, even if the rest of the communication is encrypted.

ESNI solves this problem by encrypting the SNI extension using a symmetric key shared between the client and server. This makes it difficult for an attacker to intercept and read the SNI extension, protecting the privacy of the client's browsing activity.

ESNI is designed to be used with DNS over HTTPS (DoH) or DNS over TLS (DoT) protocols to provide end-to-end encryption for DNS queries. With ESNI and encrypted DNS protocols, an attacker cannot determine the website being accessed or the IP address of the server hosting the website.

ESNI is currently supported by modern web browsers and some servers, but its adoption is still limited. However, it is expected to become more widely adopted in the future as the need for privacy and security on the internet continues to grow.


## What is SNI

SNI stands for Server Name Indication, and it is an extension to the TLS (Transport Layer Security) protocol. SNI allows a client to indicate the hostname of the server it wants to connect to during the TLS handshake, allowing multiple SSL/TLS certificates to be hosted on the same IP address.

Before the introduction of SNI, only one SSL/TLS certificate could be associated with a single IP address. This meant that if a server hosted multiple websites with SSL/TLS certificates, it would need to have multiple IP addresses, which could be costly and complicated to manage.

With SNI, a client can include the hostname it wants to connect to in the initial TLS handshake, allowing the server to select the appropriate SSL/TLS certificate and establish a secure connection with the client. This allows multiple SSL/TLS certificates to be hosted on the same IP address, reducing the need for additional IP addresses.

SNI is widely supported by modern web browsers, but some older browsers and operating systems do not support it. In these cases, the server may not be able to determine the appropriate SSL/TLS certificate to use and may fall back to using the default certificate or display a warning to the user.

Overall, SNI provides a way for servers to host multiple SSL/TLS certificates on a single IP address, improving flexibility and reducing costs.


## Does HTTPS Uses TCP
Yes, HTTPS (Hypertext Transfer Protocol Secure) uses TCP (Transmission Control Protocol) as its underlying transport protocol.

HTTPS is a protocol for secure communication over the internet, which is used to transmit sensitive information such as passwords, credit card details, and other personal information. It is a combination of HTTP and SSL/TLS protocols, where SSL/TLS provides the security layer.

TCP, on the other hand, is a transport protocol that provides reliable, ordered, and error-checked delivery of data between applications over a network. It is responsible for breaking the data into packets, delivering them to the correct destination, and reassembling them in the correct order at the receiving end.

When a client sends an HTTPS request to a server, it establishes a TCP connection with the server before any data transmission occurs. Once the connection is established, the client and server can exchange encrypted data over this connection. Therefore, TCP provides the reliable transport layer for the secure data transmission in HTTPS.

## How HTTPS works
HTTPS (Hypertext Transfer Protocol Secure) is a protocol used for secure communication over the internet. It is a combination of the HTTP protocol for transmitting web content and the SSL/TLS protocols for providing encryption and authentication. Here's how HTTPS works:

Client initiates a request: A user types a web address in their browser or clicks on a link to a secure website, which initiates an HTTPS request.

Server responds with SSL/TLS certificate: The server responds to the request with its SSL/TLS certificate, which contains the public key used for encryption.

Client verifies the certificate: The client (usually a web browser) verifies the SSL/TLS certificate using a trusted Certificate Authority (CA). The CA ensures that the certificate is valid and issued to the correct domain name.

Client generates a symmetric key: After verifying the certificate, the client generates a symmetric encryption key to use for encrypting the data.

Client encrypts the symmetric key: The client encrypts the symmetric key using the server's public key obtained from the SSL/TLS certificate.

Client sends encrypted data: The client sends encrypted data (such as login credentials or other sensitive information) to the server over the secure connection.

Server decrypts the symmetric key: The server decrypts the symmetric key using its private key, which is kept secret and not shared with anyone.

Server decrypts the data: The server uses the decrypted symmetric key to decrypt the data received from the client.

Server sends encrypted response: The server responds with encrypted data, which is encrypted using the symmetric key.

Client decrypts the response: The client decrypts the response using the symmetric key, which is already known to it.

By using SSL/TLS encryption, HTTPS ensures that the data transmitted between the client and server is encrypted and secure from eavesdropping, tampering, and other attacks. The SSL/TLS certificates and the verification process help ensure that the client is communicating with the intended server and not an impostor.





## TLS Termination Proxy
```text
Client – [ Nginx – Server ]
When TLS termination happens at nginx layer then the plaintext or un-encrypt data transmission happens from nginx to server.
```
## TLS Forward Proxy
```text
Client – [ Nginx – Server ]

When encrypt data arrives at nginx. Nginx decrypts data and initiate a new TLS session with server.
Here nginx again encrypt the data and send to the server.
```
# Perfect Forward Secrecy
** Don’t use long-term secret key but Use session key (ephermal) for encrypted communication between client and server.
### Recap: TLS 1.2 Encryption
- Client sends Hello With Some string “x” to server. 
- Server sends Hello to client by giving server certificate and string as “y”.
- Client gets the public key from the server certificate. Client prepares a pre-master key using (“x” and “y”). 
  This pre-master key is signed with public key of the server in client side. Client sends this pre-master key to the server.
- Server decrypts the pre-master key using private key of the server. Now server sends OK to the client.
- Let say from now client & server started communicating using pre-master key encrypt and decrypt. 
```text
Assume The Snipper is aware about the encrypted pre-master key. If the snipper gets the private key of the server 
then he can decrypt the pre-master key. With this he can read the encrypted communication between client and server.

So instead using private/public key based pre-master key encryption for a long term we should have 
set of session keys(ephermal for each communication) which should not be helped attacker to read the 
encryption from past even though private/public key (long term key) is compromised.
```
- Long term private/public key should be used for authentication only and not for encryption.
- TLS 1.3 forces to use Diffie Hellman.

# What is SSL Stripping
SSL stripping is a type of attack where an attacker intercepts traffic between a user and a server that is supposed to be protected by SSL/TLS encryption and downgrades the connection to an unencrypted one. This attack is typically carried out by a man-in-the-middle (MITM) attacker who can intercept the traffic and modify it in transit.

The attacker first intercepts the user's request for an SSL/TLS-protected page and sends a fake response to the user indicating that the server does not support SSL/TLS. The attacker then establishes a separate connection with the server and communicates with it using SSL/TLS encryption. The attacker forwards the data back and forth between the user and the server, but only communicates with the server using SSL/TLS, while communicating with the user in plain text. This allows the attacker to monitor and potentially modify the data being sent between the user and the server.

The SSL stripping attack is successful when the user does not notice that the connection has been downgraded and continues to send sensitive information in plain text. To prevent SSL stripping attacks, website owners should enforce the use of SSL/TLS connections, use HTTP Strict Transport Security (HSTS) to ensure that all connections to the website are made using HTTPS, and educate their users about the risks of unencrypted connections. Additionally, users can protect themselves by looking for the lock icon in the browser's address bar to ensure that the connection is encrypted, and by being cautious when entering sensitive information on websites.

# how tls 1.3 protects from Man In The Middle attack
TLS 1.3 provides several security features to protect against Man-In-The-Middle (MITM) attacks. Here are some of the key ways in which TLS 1.3 helps prevent MITM attacks:

- Perfect Forward Secrecy (PFS): TLS 1.3 requires the use of PFS, which means that each session key is unique and not derived from any previous key. This makes it much harder for an attacker to decrypt intercepted traffic, even if they have captured previous encrypted sessions.

- Stronger Cryptography: TLS 1.3 uses stronger and more secure cryptographic algorithms, including Elliptic Curve Cryptography (ECC) for key exchange and Authenticated Encryption with Associated Data (AEAD) ciphers for data encryption. These algorithms are much more resistant to attacks than the older algorithms used in earlier versions of TLS.

- Reduced Exposure to Attacks: TLS 1.3 reduces the number of round-trips required to establish a secure connection, which helps to reduce the exposure of the initial handshake to attacks. Additionally, TLS 1.3 encrypts more of the handshake messages than previous versions of TLS, which further reduces the risk of interception and tampering.

- Certificate Transparency (CT): TLS 1.3 requires the use of CT, which provides an additional layer of security by allowing clients to verify that the server's certificate has not been tampered with or issued fraudulently.

- Mutual Authentication: TLS 1.3 supports mutual authentication, which means that both the client and the server can authenticate each other during the handshake. This helps to prevent MITM attacks by ensuring that both parties are who they claim to be.

Overall, TLS 1.3 provides a strong set of security features that make it much harder for attackers to intercept and tamper with TLS connections, thereby reducing the risk of MITM attacks.

# DIFFIE HELLMAN ALGO WITH TLS 1.3

TLS 1.3 (DIFFIE HELLMAN)

> Client: 
Private(x), 
Public(y)
    ClientHello: y , (x+y): 

> Server
Private(z)
z + (x+y) = k
   ServerHello: (y+z)

> Client:
      x + (y+z) = k
      
So total 1 Round Trip between server & client to get k(symmetric key).
### Mathmatical way to TLS 1.3
- client privatey key x. client has a function g. client sends g, g^x to the server.
- server private key y. server upon receiving g^x, it computes (g^x)^y = z. z is the symmetric key. server sends g^y to the client.
- client upon receiving g^y, computes (g^y)^x = z. z is the symmetric key.
- now both client and server able produce the same symmetric key and can start encrypted communication.

# How TLS 1.2 works?
TLS 1.2 (Transport Layer Security version 1.2) is a protocol used to establish a secure connection between a client and a server over the internet. Here are the basic steps of how TLS 1.2 works:
1.	Client Hello: The client sends a message to the server to initiate a TLS handshake. This message includes the client's preferred cryptographic protocols, such as the cipher suite and version.
2.	Server Hello: The server responds with a message indicating which cryptographic protocol will be used for the session, along with the server's digital certificate.
3.	Certificate Verification: The client verifies the server's certificate to ensure that it is valid and issued by a trusted certificate authority (CA).
4.	Client Key Exchange: The client generates a pre-master secret and encrypts it using the server's public key, which is obtained from the server's certificate.
5.	Server Key Exchange: If the server requires the client to authenticate itself, it sends its own certificate to the client, and the client verifies it. The server also generates a master secret and sends it to the client, encrypted with the client's public key.
6.	Change Cipher Spec: Both the client and server agree on the encryption algorithm to use for the session and send a message to switch to that algorithm.
7.	Finished: The client and server exchange messages to confirm that the handshake is complete and the session is secure.
Once the TLS handshake is complete, the client and server can securely exchange data over the encrypted connection using the agreed-upon encryption algorithm. TLS 1.2 offers strong security and privacy protection for internet communications, and is widely used for online transactions, email, and other sensitive communications.
  
# What is the use of pre-mater key in tls 1.2
1. The pre-master key is a crucial element in the TLS 1.2 handshake process, as it is used to derive the session keys that are used for encrypting and decrypting data exchanged between the client and server over the secure connection.
2. During the handshake, the client generates a random pre-master key, which is a shared secret between the client and server. The client encrypts this pre-master key using the server's public key, which is obtained from the server's digital certificate. The encrypted pre-master key is then sent to the server.
3. The server then decrypts the pre-master key using its private key, which is stored securely on the server. Both the client and server then use the pre-master key, along with some other data exchanged during the handshake, to generate a set of session keys that are used for encryption and decryption of data exchanged during the session.
4. By using a random pre-master key, the TLS protocol ensures that the session keys used for encryption and decryption are unique to each session and not easily predictable, which provides an additional layer of security against attacks. The use of the pre-master key helps to establish a secure and private connection between the client and server, which is essential for protecting sensitive data transmitted over the internet.
