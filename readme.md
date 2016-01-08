# How does the Internet work?

## IWBAT:
* Describe the basics of how computers communicate
* Name 4 ways that computers share data
* Define the following concepts:
  - Internet
  - IP Address
    * IPv4 and IPv6 addresses
    * static and dynamic
    * dotted decimal notation
  - port
  - socket
  - Internet Domain
  - URL
  - Messages and Packets
  - Communication protocols
    * IP
    * TCP
    * UDP
    * HTTP
    * lots of others
  - Routes
  - LAN and WAN
  - ping command
  - ifconfig / ipconfig commands
  - DNS
  - MIME Types
  - RESTful Web Services

## What is the Internet?

* A network of interconnected computers that communicate over a given set of protocols.

## How Do Computers Share information / Communicate?

1. Shared file systems
2. Shared databases
3. Remote Procedure Calls (RPC) - synch
4. Messages - asynch

### How do computers do (3) or (4)

* Addresses
* Protocols

## Addresses:

* What is an address?
* What is a street address?
* What is a phone number?
* What is a computer address?
  - IP = 74.125.21.113

```
dotted-decimal notation:    74     .     125    .     21     .    113
binary notation:         01001010     01111101     00010101     0111001
hexadecimal notation:       4A           7D           15           71
```

## IPv4 and IPv6

* An IPv4 address = 4 bytes = 32 bits = 2^32 unique addresses = 4 billion addresses
* We now have more than 4 billion computing devices so we need more bits to address all of them.

### Enter IPv6

* Has 16 bytes = 128 bits = 2^128 unique addresses
* That means we can assign 100 addresses to every atom on the surface of the earth.

### Static vs. Dynamic IP Addresses

* servers need static IP addresses
* clients can have dynamic IP addresses

### What is a URL?

* Uniform Resource Locator
* scheme://domain:port/path?query_string#fragment_id

![Anatomy of a URL](https://raw.github.com/ATL-WDI-Curriculum/how-the-internet-works/master/images/anatomy-url.png)

#### Example:

[http://www.google.com:80/search?q=taylor+swift](http://www.google.com:80/search?q=taylor+swift)

<table>
  <tr>
    <th>PROTOCOL</th>
    <th>HOST (AKA DOMAIN)</th>
    <th>PORT</th>
    <th>PATH</th>
    <th>QUERY PARAMS</th>
  </tr>
  <tr>
    <td>http://</td>
    <td>www.google.com</td>
    <td>:80</td>
    <td>/search</td>
    <td>?q=taylor+swift</td>
  </tr>
</table>


### LAN vs. WAN

* Local Area Networks
  - can have a private set of addresses:
  - 16-bit LAN addresses: 192.168.0.0
  - 24-bit LAN addresses: 10.0.0.0

```
$ ping google.com
$ ifconfig | grep inet

PING google.com (74.125.196.101): 56 data bytes
64 bytes from 74.125.196.101: icmp_seq=0 ttl=44 time=15.184 ms
```

Browser URL - http://74.125.196.101/

### IP = Internet Protocol

### Lab Time - Play the IP and TCP Game (Meet Ivan Pakkitz)

Ivan is a postal worker who can travel at the speed of light. He's happy to relay thousands of messages per second between you and a friend. However, he can only transport one message at a time and each message has to fit on a single index card.

Unfortunately Ivan is incredibly inattentive, so there are a few minor limitations in his service:

* Reliability: He cannot guarantee that every message will be delivered successfully.
* Order:       He cannot guarantee delivered messages will arrive in the same order that they were sent.
* Integrity:   He cannot guarantee that all messages will arrive in their entirety.
* Recipient:   He cannot guarantee that messages will always be delivered to the correct recipient.

For our lab, we will assume that Ivan:

* shuffles the cards before deliverying them
* sometimes drops a card on the floor (maybe 1 out of 10 cards)
* may rip the card in half before delivering it (maybe 1 out of 20 cards)
* may deliver the card to the wrong person (maybe 1 out of 20)

### Debbie N. Smith

* She knows the numeric address of everyone

### Circuit vs. Packet Switching

* Circuit Switching
  - think making a phone call
  - what does it mean to get a "fast busy" signal?

* Packet Switching
  - think sending packages via FedEx

Question: If I send 5 packages to Gerry, will all 5 packages

```
(a) arrive in the order I sent them?
(b) arrive via the same truck?
(c) arrive via the same route?
(d) does it matter?
```

* Which is Faster?
* Which is More Fault Tolerant?

### Messages and Packets

* Packets have a fixed maximum size (no 18 wheelers please)
  - theoretical maximum size of a TCP packet = 64KB
  - but usually the limit is smaller
  - the MTU (Maximum Transmission Unit) for Ethernet, for instance, is 1500 bytes
* Thus a single message is often split across several packets
* For example, the request for a 300KB image would require 300 * 1024 / 1500 = 205 packets.

![Anatomy of a URL](https://raw.github.com/ATL-WDI-Curriculum/how-the-internet-works/master/images/tcp-packet-structure.gif)

### What is a route?

### TCP = Transmission Control Protocol

Builds upon the foundation of IP:

* Adds reliability (handshakes to confirm receipt, can resend on failure)
* Reorders out-of-order packets
* Checks message integrity
* Controls network congestion

See: [The Anternet](http://priceonomics.com/the-independent-discovery-of-tcpip-by-ants/)

TCP is great for plain text messages like web content, e-mails, and IMs.

### UDP = User Datagram Protocol

* Favors speed over integrity
* Uses ports, but eliminates TCP's integrity checks.

UDP is great for streaming videos and game data feeds where bulk speed
is more important than occassional packet loss.

### DNS - similar to the Yellow Pages

I know your name but need to lookup your phone number

    becomes

I know your DNS name (google.com) but need to lookup your IP address

Mapping domains to IPs => Domain Name Service

Example: `mail.google.com`

```
mail = subdomain
google = 2nd level domain
com = top level domain
```

### HTTP - HyperText Transport Protocol

* Leverages TCP for sending text and file content with integrity.
* Defines a new format for addressing higher-level applications.
* HTTP Requests (verbs) - GET, PUT, POST, DELETE, PATCH

### Packets

* Packet: a discrete chunk of data transferred over an IP-based protocol.
* Header: meta data to address and define the packet content.
* Body: the data payload of the packet.

### Ports - like a telephone extension

Some Common Default Ports:

    FTP:    20
    SSH:    22
    TELNET: 23
    SMTP:   25   Simple Mail Transfer Protocol (email)
    DNS:    53
    HTTP:   80
    POP2:  109   Post Office Protocol (email)
    POP3:  110   Post Office Protocol (email)
    SQL:   118
    IMAP:  220   Internet Message Access Protocol (email)
    LDAP:  389   Lightweight Directory Access Protocol
    SHTTP: 443   Secure HTTP (HTTP over SSL)
    RSH:   514   Remote Shell
    IPP:   631   Internet Printing Protocol

### Socket: the combination of an IP address and a Port

Hint: think of an IP address as something like a telephone number and the port as an extension

Examples:

```
127.0.0.1:3000      port 3000 on the internal loopback address
localhost:3000      port 3000 on the internal loopback address
74.125.196.101:80   port 80 (the HTTP port) at google.com
```

### Asynchronous Request / Response

* Synchronous: phone conversation
  - establishes a dedicated connection (circuit switching)

* Asynchronous: email, text message
  - sends messages back and forth (packet switching)

## MIME Types (Multipurpose Internet Mail Extensions)

### Examples:

* Text (document)
* XML
* JSON

### MIME Type Categories:

* Application - pdf, javascript, json, zip
* Audio - mp3, mp4
* Image - jpg, gif, png
* Text - css, csv, html, plain, xml
* Video - avi, mpeg, mp4, quicktime
* Vendor - prefix with vnd - vnd.ms-excel

## RESTful approach (Representational State Transfer)

> Created by Roy Fielding for his Ph.D. thesis.

* TCP/IP gives us packetized messages with guaranteed delivery and integrity checks.
* HTTP gives us CREATE, PUT, POST, DELETE, and sometimes PATCH
* RESTful is an approach to using HTTP to do CRUD-like operations between a web client and a web app.

* Representational State Transfer:
  - client/server separation of responsibilities
    - client manages user state and user interface
    - server keeps persistent data
  - stateless: all of the needed state is transferred to the client so that the server can be stateless
  - the URL represents the unique identity of the resource
  - the client can send specific HTTP requests to the server with a payload of the state needed to fulfill the request

| Resource    |      GET     |    PUT     |    POST     |    DELETE  |
|:-----------:|:------------:|:----------:|:-----------:|:-----------:
| Collection  | get a list   | replace    | add an      | delete the |
|   /todos/   | of items*    | the entire | item to the | entire     |
|             |              | collection | collection* | collection |
|             |              |            |             |            |
| Element     | get an item* | replace an |     NA      | delete the |
|   /todos/3  |              | item*      |             | item*      |
|             |              | i.e. save  |             |            |

* The cells above with an asterick are the most common cases
* GET is immutable
* PUT and DELETE are idempotent
* PATCH is the new kid on the block and allows for partial updates
  (i.e. the client can send only the parts of the item that need to be updated and the server merges these with the current item state)

### More RESTful Examples:

* http://mytodos.com/mikeh/todos
* http://mytodos.com/mikeh/todos/3
* http://mytodos.com/mikeh/todos?due='2014-10-08'
* http://mytodos.com/mikeh

### See GitHub for more examples.

* https://github.com/drmikeh
* https://github.com/drmikeh?tab=repositories
* https://github.com/drmikeh?tab=activity
* https://github.com/drmikeh/talkative-robot/issues

## The Internet of Things

## Browsers, Web Servers, and Database Servers

* Tracing a request / response through the 3 tiers:
  - browser, web server, database
