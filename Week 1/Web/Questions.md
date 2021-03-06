# Week 1
## REST

1. What are the three primary Fielding constraints? (Bonus if you can say who Fielding is!)
- Roy T. Fielding wrote a set of design principles for web architecture is 2000 in his PhD dissertation. The three main principals are: 
Client-Server (a network must be made up of servers, which hold the information of interest, and clients, which want to interact with those resources), 
Stateless (servers and clients do not need to keep track of each other's state), and 
Uniform Interface (ensure that there is a common language between servers and clients, which allows each part to be swapped or modified without breaking the entire system)

2. What sub-constraints make up a Uniform Interface?
- A system should have unique identifiers for each resource, manipulate them through sending representations from the client to the server, and have messages that are self-descriptive and composed of hypermedia
- Identification of Resources: Each resource (HTML element, image, etc) must be uniquely identified by a stable identifier
- Manipulation of Resources Through Representations: Client manipulates resources by sending representations to the server that contain the content that it would like to add, destroy, or modify
- Self-Descriptive Messages: Messages contain all of the info that the recipient needs to understand it and not broken up into multiple websites or anything
- Hypermedia: Data sent from the server to the client that contains inforamtion about what the client can do next

3. Walk through an arbitrary example of a RESTful request/response cycle, and describe what makes it RESTful
- For one of my projects, I was getting the top trending search terms from GoogleTrends. I made an HTTP GET request to GoogleTrends and got back a response with html elements that I could parse to get the data I wanted. This was a RESTful cycle because my client had to hit the google trends server, the two didn't keep track of each other's state, if I wanted to get more trends, I would have to make the request again, and the response had a uniform interface of a representation of hypermedia resources

## Web

4. What happens when you type in www.google.com and hit enter?
-1. You type www.google.com into the address bar of your browser and hit enter
2. The browser checks the cache for a DNS record to find the corresponding IP address of www.google.com
3. If the requested URL is not in the cache, ISP's DNS server initiates a DNS query to find the IP address of the server that hosts www.google.com
4. The browser initiates a TCP connection with the server
5. The browser sends an HTTP request to the web server
6. The server handles the request and sends back a response
7. The server sends out an HTTP response
8. The browser displays the content, typically HTML

5. Why do we need a DNS?
- DNS is like a phone book for the internet. Computers store web domains as IP addresses, which are hard for humans to remember. Humans use domain names, such as google.com and DNS takes that name and finds the IP address associated with it, so the computer can process the request.

6. Explain TCP, and why it is a necessary protocol
- Transmission Control Protocol. In order to send data between computers, the data is broken into many packets that can travel different routes. This prevents the data from bottlenecking and ensures that it is always taking the most efficient route. TCP is a standard for breaking these packets down, figuring out how to assemble them, and checking to see if all of the needed packets arrived at the destination. It ensures that all data is received and allows us to send and retrieve data faster by breaking it into packets.

7. What is a datagram?
- While TCP sends data in packets, UDP sends data in datagrams. A datagram is a very small amount of data that provides a connectionless communication of data. The arrival time and order of arrival of datagrams is not guaranteed by the network.

8. What are the benefits of UDP over TCP? What are the shortcomings?
- UDP has smaller packet sizes, no connection to create and maintain, and more control over when data is sent. However, it is not reliable, some data may not arrive or arrive corrupted and it won't request new data. Packets may arrive out of order and there is no congestion control