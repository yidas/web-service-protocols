HTTP
====

## HTTP

The **Hypertext Transfer Protocol (HTTP)** is an application layer protocol for distributed, collaborative, hypermedia information systems. HTTP is the foundation of data communication for the World Wide Web, where hypertext documents include hyperlinks to other resources that the user can easily access, for example by a mouse click or by tapping the screen in a web browser.

### Sequence Diagram

![HTTP Flow](https://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/yidas/web-service-principles/main/http/http-flow.plantuml)

---

## HTTPS

**Hypertext Transfer Protocol Secure (HTTPS)** is an extension of the Hypertext Transfer Protocol (HTTP). It is used for secure communication over a computer network, and is widely used on the Internet. In HTTPS, the communication protocol is encrypted using Transport Layer Security (TLS) or, formerly, Secure Sockets Layer (SSL). The protocol is therefore also referred to as **HTTP over TLS**, or **HTTP over SSL**.

### Sequence Diagram

Inciding Client-authenticated (Two-way SSL)

![HTTPS Flow](https://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/yidas/web-service-principles/main/http/https-flow.plantuml)

### Handshake Steps

1. Negotiation Phase:
- A client sends a **ClientHello** message specifying the highest TLS protocol version it supports, a random number, a list of suggested cipher suites and compression methods.
- The server responds with a **ServerHello** message, containing the chosen protocol version, a random number, cipher suite and compression method from the choices offered by the client. The server may also send a session id as part of the message to perform a resumed handshake.
- The server sends its **Certificate** message (depending on the selected cipher suite, this may be omitted by the server).
- The server sends its **ServerKeyExchange** message (depending on the selected cipher suite, this may be omitted by the server). This message is sent for all DHE, ECDHE and DH_anon ciphersuites.
- The server sends a **CertificateRequest** message, to request a certificate from the client.
- The server sends a **ServerHelloDone** message, indicating it is done with handshake negotiation.
- The client responds with a **Certificate** message, which contains the client's certificate, but not it's private key.
- The client sends a ClientKeyExchange message, which may contain a PreMasterSecret, public key, or nothing. (Again, this depends on the selected cipher.) This PreMasterSecret is encrypted using the public key of the server certificate.
- The client sends a CertificateVerify message, which is a signature over the previous handshake messages using the client's certificate's private key. -- This signature can be verified by using the client's certificate's public key. This lets the server know that the client has access to the private key of the certificate and thus owns the certificate.
- The client and server then use the random numbers and PreMasterSecret to compute a common secret, called the "master secret". All other key data ("session keys") for this connection is derived from this master secret (and the client- and server-generated random values), which is passed through a carefully designed pseudorandom function.
2. The client now sends a **ChangeCipherSpec** record, essentially telling the server, "Everything I tell you from now on will be authenticated (and encrypted if encryption was negotiated). " The ChangeCipherSpec is itself a record-level protocol and has type 20 and not 22.
- Finally, the client sends an encrypted Finished message, containing a hash and MAC over the previous handshake messages.
- The server will attempt to decrypt the client's Finished message and verify the hash and MAC. If the decryption or verification fails, the handshake is considered to have failed and the connection should be torn down.
3. Finally, the server sends a **ChangeCipherSpec**, telling the client, "Everything I tell you from now on will be authenticated (and encrypted if encryption was negotiated). "
- The server sends its own encrypted Finished message.
- The client performs the same decryption and verification procedure as the server did in the previous step.
4. Application phase: at this point, the "handshake" is complete and the application protocol is enabled, with content type of 23. Application messages exchanged between client and server will also be encrypted exactly like in their Finished message.

### Server Name Indication (SNI)

Server Name Indication (SNI) is an extension to the Transport Layer Security (TLS) computer networking protocol by which a client indicates which hostname it is attempting to connect to at the start of the handshaking process.

[Server Name Indication - Wikipedia](https://en.wikipedia.org/wiki/Server_Name_Indication)

### Key exchange/agreement and authentication

- [Key exchange/agreement and authentication (With version support list) - Wikipedia](https://en.wikipedia.org/wiki/Transport_Layer_Security#Key_exchange_or_key_agreement)

| Algorithm       | Key Exchange        | DH Key Type     | Cert Signature | [Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) | Notes                                        |
|-----------------|---------------------|------------------|----------------|------------------|----------------------------------------------|
| RSA             | RSA (Encrypted PMS) | ❌ (None)        | RSA            | ❌ No             | Pre-master secret encrypted with RSA pubkey  |
| DH-RSA          | Static DH           | ✅ Static DH     | RSA            | ❌ No             | Certificate includes static DH key           |
| DHE-RSA         | Ephemeral DH        | ✅ Ephemeral DH  | RSA            | ✅ Yes            | Most common DH setup with RSA cert           |
| DH-DSS          | Static DH           | ✅ Static DH     | DSS            | ❌ No             | Rarely used                                   |
| DHE-DSS         | Ephemeral DH        | ✅ Ephemeral DH  | DSS            | ✅ Yes            | DSS = DSA signature                          |
| ECDH-RSA        | Static ECDH         | ✅ Static ECDH   | RSA            | ❌ No             | Rare; cert includes static ECDH key          |
| ECDHE-RSA       | Ephemeral ECDH      | ✅ Ephemeral ECDH| RSA            | ✅ Yes            | Common in modern TLS                         |
| ECDH-ECDSA      | Static ECDH         | ✅ Static ECDH   | ECDSA          | ❌ No             | Uncommon                                      |
| ECDHE-ECDSA     | Ephemeral ECDH      | ✅ Ephemeral ECDH| ECDSA          | ✅ Yes            | Common in systems using ECDSA certs          |

#### Flow of different key exchange methods

##### RSA key exchange

![RSA](https://cf-assets.www.cloudflare.com/slt3lc6tev37/HMtyedlloYodaGnzxFcON/176dea4dbf1c8b4f3d58e6afd43ee9ea/ssl-handshake-rsa.jpg)

##### Ephemeral Diffie-Hellman Key Exchange

![Diffie-Hellman](https://cf-assets.www.cloudflare.com/slt3lc6tev37/1mzPVvjnKpVD0LUSsUlq2r/23c6dee053aaab22b122b53783dc098f/ssl-handshake-diffie-hellman.jpg)

---

References
----------

[Wikipedia - Hypertext Transfer Protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)

[Wikipedia - HTTPS](https://en.wikipedia.org/wiki/HTTPS)

[Wikipedia - TLS handshake](https://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_handshake)

[Moserware - The First Few Milliseconds of an HTTPS Connection](http://www.moserware.com/2009/06/first-few-milliseconds-of-https.html)

[How does keyless SSL work? | Forward secrecy | Cloudflare](https://www.cloudflare.com/learning/ssl/keyless-ssl/)
