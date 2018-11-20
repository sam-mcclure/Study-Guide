# REST

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