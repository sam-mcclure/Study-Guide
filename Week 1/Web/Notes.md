# Week 1
## REST 

* Representation State Transfer - A set of design principles for making network communication more scalable and flexible

* Roy T. Fielding first coined the term REST in 2000 in his PhD dissertation *Architectural Styles and the Design of Network-based Software Architectures*

* Fielding Constraints - Architectural constraints that a system must satisfy to be considered RESTful 

1. Client-server - The network must be made up of clients and servers. A server is a computer that has resources of interest and a client is a computer that wants to interact with the resources stored on the server. When you browse the interet, your computer is acting as a client and sends HTTP requests to a server in order to access and manipulate information. 

2. Stateless - Servers and clients do not need to keep track of eachother's state. When a client is not interacting with the server, the server has no idea of its existence. The server also does not keep a record of past requests. Each request is treated as a standalone

3. Uniform Interface - ensures that there is a common language between servers and clients that allows each part to be swapped out or modified without breaking the entire system. This is achieved through 4 sub-constraints: identification of resources, manipulation of resources through representations, self-descriptive messages, and hypermedia

    1. Identification of Resources - Each resource (HTML element, image, etc) must be uniquely identified by a stable identifier (does not change across interactions and does not change even when the state of the resource changes). Client makes GET request to URI and gets back HTML or an error

    2. Manipulation of resources through representations - The client manipulates resources through sending representations to the server - usually a JSON object containing the content that it would like to add, delete, or modify. In REST, the sever has full control of the resources and is responsible for any changes. Client sends respresentation of object in POST request

    3. Self-descriptive messages - One that contains all the information that the recipient needs to understand it. There should not be additional information in a separate documentation or in another website. Client makes GET request and gets back status, content-type, and content to render

    4. Hypermedia - Data sent from the server to the client that contains information about what the client can do next/what further requests it can make. Severs should only be sending hypermedia to clients

* Other Fielding Constraints: 

1. Caching - The constraint that sever responses should be labelled as either cacheable or non-cacheable. Caching occurs when the client stores previous responses it recieved from the server, so that when the data is needed again, it can save a round trip over the network by using the cached data.

2. Layered system - The fact that there can be more components than just servers and clients. There can be more than one layer in the system, however, each component is constrained to only see and interact with the very next layer

3. Code on Demand - Optional constraint - refers to the ability for a server to send executable code to the client (ie HTML's script tag)

## What happens when you type a URL into a browser and hit enter?

1. You type in www.google.com into the address bar in your browser
2. The browser checks the cache for a DNS record to find the corresponding IP address of www.google.com
    - DNS (Domain Name System) is a database that maintains the name of the website (URL) and the particular IP address assigned to it. The IP address belongs to the computer which hosts the server of the website we are requesting to access
    - DNS is a list of URLs and their IP addresses just like how a phone book is a list of names and their corresponding phone numbers
    - The main purpose of DNS is human-friendly navigation. It's easier to remember the name of the website using a URL and let DNS do the work for us with mapping it to the correct IP
    - In order to find the DNS record, the browser checks 4 caches: browser cache, OS cache, router cache, ISP cache
3. If the requested URL is not in the cache, ISP's DNS server initiates a DNS query to find the IP address of the server that hosts the website (ie www.google.com)
    - These requests are sent using small data packets which contain information such as the content of the request and the IP address it is destined for. These packets travel through multiple networking equipment between the client and the server before it reaches the correct DNS server.
4. Browser initiates a TCP connection with the server
    - Once the browser recieves the correct IP address, it will build a connection with the server tha matches the IP address to transfer information. TCP is the most common protocol used for any type of HTTP request
    - This connection is established using a process called the TCP/IP three-way handshake, a three step process where the client and the server exchange SYN(synchronize) and ACK(acknowledge) messages to establish a connection
    1. Client machine sends SYN packet to the server over the internet asking if it's open for new connections
    2. If the server has open ports that can accept and initiate new connections, it'll respond with an ACKnowledgement of the SYN packet using a SYN/ACK packet
    3. The client will recieve the SYN/ACK packet from the server and will acknowledge it by sending an ACK packet
5. The browser sends an HTTP request to the web server
    - Once the TCP connection is established, it's time to start transferring data. The browser will send a GET request asking for the www.google.com web page. If you're entering credentials or submitting a form, this could be a POST request
    - This request will also contain additional information such as browser identification (User-Agent header), types of requests it will accept (Accept header), and conenction headers asking it to keep the TCP connection alive for additional requests
6. The sever handles the request and sends back a response
    - The server contains a web server which receives the request from the browser and passes it to a request handler to read and generate a response
7. The server sends out an HTTP response
    - The server response contains the web page you requested as well as the status code, compression type (Content-Encoding), how the cache the page (Cache-Control), any cookies to set, privacy info, etc
8. The browser displays the HTML content (for HTML responses, which is the most common)

* DNS is controlled by IANA (Internet Assigned Numbers Authority)). They have the mandate of making sure the correct technical procedures are in place to have a safe and stable Domain Name System. Which also invovles ICANN (Internet Corporation for Assigned Names and Numbers)

* Besides providing technical operations of vital DNS resources, ICANN also defines policies for how the 'names and numbers' of the internet should run

W1D4 

## DNS

* A Domain Name System is one of the key components to how requests are made from your browser

* The DNS is often referred to as the backbone of the internet

* Steps for a DNS request:
1. A user asks their browser to visit www.google.com
2. The browser queries a DNS resolver(usually their ISP) where's google.com?
3. DNS Resolver queries the Root servers (which have a big important list that keeps this information). "where's .COM?' replies with Verisign
4. DNS Resolver then queries Verisign - where is google.com?. Verisign replies with the nameservers and the IP address
5. Hosting servers are queried with the IP address 'Give me the files for this IP address'
6. Website files are delivered and rendered on the page so the user can use it

W1D5

## TCP

* Information transer from computers doesn't follow a fixed path. Information travels between computers in a packet. It might take a different route every time. Digital info can be sent with IP packets.

* If you have large information to send, it may be made into thousands of packets. Each knowns the address of where it came from and where it's going. Routers direct the path the packets take. The may arrive at different times and in different orders.

* Routers choose the cheapest path for each packet, considering things such as time. Having options for paths make the internet fault tolerant. 

* TCP (Transmission Control Protocal) - When the packets arrive, TCP does a full inventory of the received packets. If they're all there, it is a success. If some packets are missing, TCP will request that packet to be resent

* TCP and Router systems are scalable

* TCP/IP Transmission Control Protocol/Internet Protocol

* The application layer has protocols like HTTP, the transport layer has TCP and UDP. After the application layer gets the data, it talks to the transport layer using ports. Once it gets the data, TCP breaks it into packets which can individually take the quickest route to the target computer. To make sure they can be put together correctly, TCP includes a header of instructions on how to assemble them and checks for any errors. The IP  (internet) layer checks the IP address. The last layer is something. 

## UDP

* The structure of a packet: there are 5 layers: Application(HTTP), Transport(UDP and TCP), Network(IP), Link(Ethernet or Wifi), Physical(coaxial Ethernet cable)

* UDP and TCP are part of the transport layer

* Purpose of the transport layer is to let multiple applications use one network connection simultaneously

* UDP (User Datagram Protocol) is the light-weight connectionless choice

* Advantages of UDP: smaller packet sizes, no connection to create and maintain, more control over when data is sent

* Disadvantages of UDP: has a primitive form of error detection, but it is not that reliable. When it detects corruption, it will not try to fix it. No compensation for lost packets. Every packet only gets set once. Packets can arrive out of order. No congestion control. Not that reliable

* TCP is the reliable, connection based choice

* Since TCP is connection based, you have to set up a connection first (three-way handshake). Because there is a connection, this allows for features such as delivery acknowledgements, retransmission (will send packet again if no delivery acknowledgement), in-order delivery, congestion control(delays transmission when the network is congested), enforces error detection

* Disadvantages of TCP: Require bigger headers, data doesn't always get sent out immeadiately(side effect of congestion control), has bigger overhead

* UDP better for video streaming (don't care if some packets go missing)

* UDP is message-oriented. Application sends data in distinct chunks

* TCP is stream-oriented. Used as continouous flow of data split up in chunks by TCP.

* For text conversation, TCP is better because it doesn't require much bandwith and the messages will ensure delivery and be in the right order.

* TCP is also best when data loss can't be tolerated or in-order delivery is needed, such as file transfers and remote access. Or if you need delivery acknowledgements

* For multimedia streaming, you can use UDP or TCP. UDP is preferred because there is less overhead, send delay is undesirable, and data loss can be masked. Some companies are using TCP when the overhead doesn't deteriorate performance or some firewalls block UDP for security reasons

* UDP can also be used for small transactions, such as DNS lookups(no need to create and close the connection first) or bandwidth-intensive apps that can tolerate packet loss

* TCP is used in the case of non-time critical applications and UDP is used for games or applications the require fast transmission of data.

* TCP is a connection oriented stream over an IP network. It guarantees that all sent packets will reach the destination in the correct order. This implies the use of acknowledgement packets sent back to the sender, and automatic retransmission, causing additional delays and a general less efficient transmission than UDP.

* UDP is a connection-less protocol. Communication is datagram oriented. The integrity is guaranteed only on the single datagram. Datagrams reach destination and can arrive out of order or don't arrive at all. It is more efficient than TCP because it uses non ACK. It's generally used for real time communication, where a little percentage of packet loss is preferable to the overhead of a TCP connection.

* In certain situations, UDP is used because it allows broadcast packet transmission. This is sometimes fundamental in cases like DHCP protocol, because the client machine hasn't still received an IP address (this is the DHCP negotiation protocol purpose) and there won't be any way to establish a TCP stream without the IP address itself