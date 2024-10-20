# Session 1: Networking Basics -- TCP/IP and HTTP/s

We cover the fundamentals of HTTP and TCP, understanding how HTTP defines the rules for communication between clients and servers, while TCP ensures reliable data transmission. Next up we discussed the DNS[^1], which translates human-readable domains to IP addresses of the requested service. Without DNS we would have to remember numerical ip addresses for each and every websites we would ever want to visit.

Next, we explored Client-Server architecture and the importance of servers. Servers can be written in multiple languages like Javascript(using NodeJS), Java, Golang (which happens to be our choice of programming language for this cohort) and many more. Golang is a modern and easy to understand language using which developers can easily work with HTTP requests and respond to them properly.

## 1. DNS - Domain Name System

### 1.1 Why do we need DNS?

Humans identify each other using names. That is not the case for computers. Computers uses numerical IP addresses to identify and locate each other. They look like this `192.168.0.1` (version 4 - IPv4) and `2001:0db8:85a3:0000:0000:8a2e:0370:7334` if they are of version 6 (IPv6). So for you to access a resource on another computer (servers) you need to know its IP addresses. But we access tens, if not hundreds, of websites and services everyday. Like for example, you're reading this through www.github.com. Remembering addresses for all these services would not be convinient, so a system was developed named DNS -- Domain Name System.

**The job of DNS is to resolve IP addresses of domain names.** Lets understand how it works.

<div align="center">
  <img src="./media/where-domain.png">
</div>

### 1.2 How does DNS work?

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./media/dns-dark.png">
  <source media="(prefers-color-scheme: light)" srcset="./media/dns-light.png">
  <img alt="DNS: Domain Name System" />
</picture>

All the sorcery begins when the user accesses a website/resource, typically, from their web browser (or any client using a protocol that requires domains to be resolved. For example, E-mail, SSH & FTP clients).

> [!NOTE]
> "Client" is just a way of referring to an application being used by user. Like Web Browsers. Please do not confuse yourself

The client accesses a resource located on a server, but the client doesn't know yet who to talk to, meaning where to look for the requested resource. The browser first looks into its own DNS Cache if the IP of the domain is already available. If it doesn't have then it looks into the Operating System's DNS Cache. If it doesn't find the IP there, It queries a **Recursive Resolver**.

#### 1.2.1 Recursive Resolvers:

A Recursive Resolver is typically hosted by your ISP. Big tech companies like Google and Cloudflare also offer their dns resolvers for us to use. It is called Recursive Resolver because it recursively queries multiple servers to resolve a domain. Don't worry, we'll discuss them all as we proceed.

When a resolver receives a query for a domain, it looks up into its own cache first. If it doesn't finds the IP, it then queries a **Root Server**. **Lets just say, the resolver knows a guy, who knows a guy, who knows another guy!**

#### 1.2.2 Root server:

The Root Server is at the top of the DNS heirarchy. There are 13 sets of root servers, operated by 12 organizations placed strategically placed around the world. Each set has its own unique IP.
The Root server itself doesn't have any information on the IPs of any domain. Instead they store the addresses of **TLD Server: Top Level Domain Server**. **The root server will direct the resolver to a TLD server for the requested TLD (TLD are .com, .org, .in etc).** Each TLD has its own TLD server. That is the sole purpose of a Root server

#### 1.2.3 TLD Server:

When resolver queries the TLD, the TLD server also doesn't knows the IP of the domain. Instead the TLD holds information of the **Authoritative Name Server** which holds the information of the requested domain. The TLD server now directs the resolver to Authoritative Server of the required domain

#### 1.2.4 Authoritative Name Server:

This is the last step in the process of resolving a domain. This server holds all the imformation of a domain including its IP address. They provide the IP address of a domain to our resolver. They store information about the domains such as A/AAAA records, MX records, CNAME records etc.

The resolver finally gets the IP address and returns it to the client. It also caches the IP, in case it is requsted again soon so it dosn't have to repeat all the steps.

Note that all of this happens under just a fraction of a second.

**Also visit:** [howdns.works](https://howdns.works/)

## 2. TCP - Transmission Control Protocol

TCP[^2] remains on the Transport Layer[^3] of the OSI Model[^4]. It is built on top of Internet Protocol (IP)[^5]. Therefore, the entire suite is commonly referred as TCP/IP. TCP offers reliable, ordered and error-checked delivery of bytes between applications. TCP has major applications today such as world wide web, file transfers, email, etc[^6]. The TCP protocol is very huge, In this document we'll only cover what we need.

### 2.1 How does it works?

TCP is a connection-oriented protocol, meaning a connection between client and server needs to be established before any exchange of data can happen. TCP does this using three-way handshake procedure. Lets understand it.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./media/3wayhandshake-dark.png">
  <source media="(prefers-color-scheme: light)" srcset="./media/3wayhandshake-light.png">
  <img alt="Representation of TCP 3-Way Handshake" />
</picture>

In Simpler words: \
**1. Client:** Hey, server, i would like to establish a connection. Here's my _request_ \
**2. Server:** Hey client, i'm ready for connection. I've received your _request_ and here's my _acknowledgement_ to your request. \
**3. Client:** Okay i've received your _acknowledgement_. here's my _acknowledgement_ to your acknowledgement. \
**4. Client:** Okay mr. server, i'll need "ABC", "DEF", "GHI" and also "XYZ" \
**5. Server:** Alright here's all the jargon you've wanted :) / Oops, i don't have any of that dude :(

The client starts by sending whats called a SYN packet. This SYN packet contains a random number which will be used to track the conversation. the server sees this and sends back a SYN+ACK packet. This is basically server saying, "hey client, i am ready to connect and i acknowledge you". The client sees this and sends back its own acknowledgement to the server. \
Steps 1 to 3 represents this. The steps 4, 5 and further are the actual exhange of data that happens (like requesting html documents and all sorts of media).

#### 2.1.1 TCP Segment Structure

Protocols like TCP, and also HTTP, exchange data in packets. Ever wondered whats inside those packets? These packets are strictly structured and have multiple segments distinguishing various information inside a packet. Take a look at it [here](https://en.wikipedia.org/wiki/Transmission_Control_Protocol#TCP_segment_structure). Programmers are not _required_ to know this by heart for everyday tasks, but you should definitely take a look at it once to have a deeper understanding.

### 2.2 HTTP/HTTPS

To work with the web, TCP alone isn't enough because it doesn't have a lot of higher level functionality to make the web work properly. It lacks the ability to identify a "specific" resource, it lacks caching, it also lacks a way of storing some persistent data (like cookies) which are essential today. TCP is only concerned with delivering raw data, which makes it impossible for This is where HTTP(or HTTPS) comes into play.

#### 2.2.1 What is HTTP/HTTPS

HTTP (HyperText Transfer Protol) is an **application level** protocol. If you remember, the language for sharing documents through the web was and is HTML, HyperText Markup Language. HTTP defines rules for how the data (HTML in our case, JS and CSS included in modern times) should be trasported. It provides us a Request/Response[^7] architecture.

HTTP offers multiple **methods** which specify the action required to be performed on a given resource. Commonly used methods are: **GET, POST, DELETE, PUT, PATCH, OPTIONS.**[^8]

This is what a HTTP request and repsonse looks like:

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./media/http-request-dark.png">
  <source media="(prefers-color-scheme: light)" srcset="./media/http-request-light.png">
  <img alt="HTTP Request" />
</picture>
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./media/http-response-dark.png">
  <source media="(prefers-color-scheme: light)" srcset="./media/http-response-light.png">
  <img alt="HTTP Response" />
</picture>

**HTTPs** is same as HTTP with added security. It encrypts the communication between server and the client using **SSL/TLS**. With HTTPs, the server provides a digital certificate that verifies its identity, ensuring users are communicating with the intended server and not a malicious one.

Just like TCP, HTTP also has a lot to it. Please refer to [this page](https://en.wikipedia.org/wiki/HTTP)

[^1]: https://howdns.works/
[^2]: https://en.wikipedia.org/wiki/Transmission_Control_Protocol
[^3]: https://en.wikipedia.org/wiki/Transport_layer
[^4]: https://en.wikipedia.org/wiki/OSI_model
[^5]: https://en.wikipedia.org/wiki/Internet_Protocol
[^6]: https://stackoverflow.com/questions/5330277/what-are-examples-of-tcp-and-udp-in-real-life
[^7]: https://en.wikipedia.org/wiki/Request%E2%80%93response
[^8]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods
