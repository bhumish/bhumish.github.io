---
title: "SSL/TLS and Your Browser"
date: 2014-08-29
draft: false
tags: ["ssl", "tls", "https", "web-security", "cryptography", "certificate-authorities", "encryption"]
categories: ["Web Security"]
description: "A comprehensive guide to understanding how SSL/TLS works in browsers, covering the handshake process, certificate exchange, and security implications."
summary: "Deep dive into SSL/TLS protocol implementation in browsers, explaining the handshake process, certificate validation, and what attackers can see during encrypted connections."
---

SSL/TLS provides an extra layer of security to the HTTP, making it **HTTP Secure (HTTPS)**. It works on the Application Layer (OSI Model) along with HTTP. HTTPS is not a different protocol, but the underlying HTTP with implementation of SSL/TLS for security.

**Public Key Infrastructure** and **Certificate Authorities** are used for making it possible.

## How HTTPS works?

### Short Version

Just like the TCP Handshake, a handshake happens in SSL between the server and the client. We can break this handshake into three steps: **Hello**, **Certificate exchange** and **Key exchange**.

#### Hello
The client sends a Hello message and the server responds with its Hello message. These messages contain information like the SSL version supported, cipher suite and some random data for key generation.

#### Certificate Exchange
To provide its authenticity, the server has to send its SSL certificate to the client. On receiving the certificate, the client checks whether its verified and trusted by some Certificate Authority, and takes the decision accordingly. For some sensitive applications, the server can ask for a certificate from the client too.

#### Key Exchange
A symmetric key is exchanged between the two parties. The client computes a key, encrypts it with the server's public key, and sends it to the server. Only the server can decrypt it, by its own private key. All the communication then takes place encrypted with this symmetric key.

### Long Version

#### Client Hello

After the TCP connection is established, the clients starts the SSL handshake. The important data in the Client's Hello message includes:

- **Version Number** (eg. SSL 2.0, SSL 3.0, TLS 3.1)
- **Random Data** (which is later used with the Server's Random Data to generate a secret key)
- **Cipher Suite** (the list of cipher suite available with the client, which includes – the protocol version, the algorithm for key exchange, the algorithm for encryption, and a hash function)

The Client Hello message can be:

```
ClientVersion 3,1
ClientRandom[32]
SessionID: None (new session)
Suggested Cipher Suites:
TLS_RSA_WITH_3DES_EDE_CBC_SHA
TLS_RSA_WITH_DES_CBC_SHA
Suggested Compression Algorithm: NONE
```

#### Server Hello

The Server responds with its Hello message, and some of its fields are:

- **Version Number** (The highest version which both of them – server & client support)
- **Random Data** (which is later used with Client's Random Data to generate a secret key)
- **Cipher Suite** (the strongest cipher suite which both server & client support is chosen by the server. If there is none, the session will be ended with 'handshake failure')

The Server Hello message can be:

```
Version 3,1
ServerRandom[32]
SessionID: bd608869f0c629767ea7e3ebf7a63bdcffb0ef58b1b941e6b0c044acb6820a77
Use Cipher Suite:
TLS_RSA_WITH_3DES_EDE_CBC_SHA
Compression Algorithm: NONE
```

Along with the above mentioned details, the following steps take place in the Server Hello message:

- The server sends its **digital certificate** to the client, which has the server's public key
- Server creates a **temporary key** to the client
- Server asks the client for its **certificate**, to validate the client's authenticity
- **End of hello**, meaning the server's Hello message is done, and client can respond

#### Client Response

After getting the server's Hello Done message, client starts talking. It sends the necessary messages in the below mentioned sequence:

- **Client certificate** – contain's the client's public key, to provide its authentication at the server
- **Client Key exchange** – the most important part of the communication. The client computes a premaster key from both the random values previously exchanged. This key is then encrypted by server's public key before sending it, so that only the server can decrypt and get out the original key with its private key.
- **Change cipher spec** – all the further messages will be encrypted using keys and algorithms negotiated
- **Client Finished** – is the hash of the entire conversation. This is the first message which is encrypted and hashed for the session.

#### Server Final Response

This is the final message in the conversation between the server and the client to have a secured connection. The server's final response will have:

- **Change cipher spec** – will notify the client that the server will start encrypting the messages with the negotiated keys and algorithms
- **Server Finished** – is the hash of the entire conversation to this point. If the client can decrypt this message and validate the hashes, it means that the SSL/TLS handshake was successful.

After the SSL/TLS handshake is done, further communication is secure between the server and the client.

## Example

A representation of how your browser starts a HTTPS connection with website `example.com`:

1. **Firefox** (your browser, for example) connects with the server of `example.com` with HTTP and asks for the login page which uses HTTPS
2. For the communication, the server sends Firefox a **certificate**, which contains the server's public key
3. Firefox **verifies the public key** of the server from the certificate
4. Firefox chooses a **random symmetric key** and encrypts it with the public key of the server
5. On receiving the encrypted message, the server **decrypts it with its private key**. Nobody else on the network who has received the encrypted message can decrypt it, because they don't have the server's private key. Now the server has the symmetric key with it
6. Every time Firefox wants to send something to `example.com` in a secured manner, it will **encrypt it with the symmetric key**. On the other end, the server will decrypt it with the same key

Every website/server which wants to implement HTTPS (i.e. SSL/TLS security) has to buy SSL certificates from authorities like **VeriSign**, **Comodo**, etc. Many websites implement HTTPS part only for some important pages (like login or payment) and other parts of the website work on simple HTTP. 

Implementing HTTPS for the whole website is not much costly, but the CPU overload increases in processing the requests. Hence many website owners keep away from HTTPS because of the cost factor or the overload factor. Recently Google announced that it will reward the HTTPS webpages with a higher ranking in its search results ([source](http://googleonlinesecurity.blogspot.in/2014/08/https-as-ranking-signal_6.html)).

## Why not use asymmetric key encryption for the handshake?

There's an answer on [StackExchange](http://security.stackexchange.com/a/3661):
1. **Asymmetric encryption is much slower** compared to symmetric encryption
2. **For the same keylength, asymmetric is weaker** compared to symmetric encryption

## What an attacker can see if you are using SSL/TLS during your connection?

If you are using SSL/TLS correctly, the attacker can interpret only some of your data. That includes – **the domain you are connected to**, the related **IP address** and **port numbers**.

For example, if you are doing a Google search using https, the URL in the browser will be: `https://www.google.co.in/?gws_rd=ssl#q=what+is+https`, and you can see the full URL. But on your cable, only the domain name `google.co.in` is sent to the DNS for domain name resolution, instead of the full query/URL. Hence, you can say that **HTTPS hides your full URL, only the domain name is revealed**.

> **Important:** HTTPS provides **confidentiality of data**, but **not anonymity** of who is sending / receiving the data.

This [interactive image by EFF](https://www.eff.org/pages/tor-and-https) provides clear understanding of what can be seen by the eavesdroppers while you are using HTTPS and while you are using [Tor](https://www.torproject.org/).

---

**References:**
- [SSL/TLS in Detail](http://technet.microsoft.com/en-us/library/cc785811%28v=ws.10%29.aspx)
- [One more answer at StackExchange](http://security.stackexchange.com/a/20833)