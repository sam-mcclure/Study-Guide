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

# Week 2

## HTTP Methods

1. GET - The GET method is used to retrieve information from the given server using a given URI. Requests using GET should only retrieve data and should have no other effect on the data
- A GET Request retrieves data from a web server by specifying parameters in the URL protion of the request. This is the main method used for document retrieval

2. HEAD - Same as GET, but transfers status line and header section only
- Functionally similar to GET, except that the server replies with a response line and headers, but no entity-body

3. POST - A POST request is used to send data to the server, for example, customer info, file upload, etc, using HTML forms
- Used when you want to send some data to the server

4. PUT - Replaces all current representations of the target resource with the uploaded content
- Used to request the server to store the included entitity-body at a location specified by the given URL

5. DELETE - Removes all current representations of the target resource given by a URI
- Used to request the server to delete the given file at the root of the server

6. CONNECT - Establishes a tunnel to the server identified by a URI
- Used by the client to establish a network connection to a web server over HTTP.

7. Options - Describes the communication options for the target resource
- Used by the client to find out the HTTP methods and other options supported by a web server. The client can specify a URL for the OPTIONS method, or an asterisk * to refer to the entire server.

8. TRACE - Performs a message loop-back test along the path to the target resource
- Used to echo the contents of an HTTP Request back to the requester which can be used for debugging purpose at the time of development

## HTTP Status Codes

* 1xx - Informational: Indicates a provisional response, consisting only of the Status-Line and optional headers, and is terminated by an empty line. There are no required headers. Request recieved, continuing process. Since HTTP/1.0 did not define any 1xx status codes, servers must not send a 1xx response to an HTTP/1.0 client except under experimental conditions

* 2xx - Success: Indicates the action requested by the client was receieved, understood, accepted, and processed successfully

* 200 OK - Standard response for successful HTTP requests. The information returned with the response will depend on the request method used 
    - GET -  an entity corresponding to the requested resource is sent in the response
    - HEAD - the entitiy-header fields corresponding to the requested resource are sent in the response without any message-body
    - POST - An entity describing or containing the result of the action
    - TRACE - an entity containing the request message as recieved by the end server
- General status code, most common code used to indicate success. In a GET request, the response will contain an entity corresponding to the requested resource. In a POST request, the response will contain an entity describing or containing the result of the action

* 201 Created - The request has been fulfilled and resulted in a new resource being created (via either POST or PUT)

* 204 No Content - The server successfully processed the request, but is not returning any content. Status when wrapped resonses (ie JSEND) are not used and nothing is in the body (ie DELETE)

* 3xx - Redirection: The client must take additional action to complete the request. Indicated that further action needs to be taken by the user agent in order to fulfil the request. The action required may be carried out by the user agent without interaction with the user if and only if the method used in the second request is GET or HEAD. A user agent should not automatically redirect a request more than five times, since such redirections usually indicate an infinite loop

* 304 Not Modified - If the client has performed a conditional GET request and access is allowed, but the documents has not been modified, the server SHOULD respond with this status cod. The 304 response MUST NOT contain a message-body, and thus is always terminated by the first empty line after the header fields
- Response MUST included Date
- Indicates the resource has not been modified since last requested. Used for conditional GET calls to reduce band-width usage. If used, must set the Date, Content-Location, and ETag headers to what they would have been on a regular GET call. There must be no body in the response

* 4xx Client Error - Intended for cases in which the client seems to have erred. Except when responding to a HEAD request, the server SHOULD include an entity containing an explanation of the error situation, and whether it is a temporary or permanent condition.

* 400 Bad Request - The request could not be understood by the server due to bad syntax. The client SHOULD NOT repeat the request without modifications. General error when fulfilling the request would cause an invalid state. Domain validation errors, missing data, etc 

* 401 Unauthorized - Error response for missing or invalid authentication token. The request requires user authentication. Similar to 403 Forbidden, but specifically for use when authentication is possible but has failed or not yet been provided. The response must include a WWW-Authentication header field containing a challenge applicable to the requested resource.

* 403 Forbidden - The request was a legal request, but the server is refusing to respond to it. Unlike a 401 Unauthorized response, authenticating will make no difference. Error code for user not authorized to perform the operation or the resource is unavailable for some reason. Authorization will not help and the request SHOULD NOT be repeated

* 404 Not Found - The requested resource could not be found but may be available again in the future. Subsequent requests by the client are permissible. Used when the requested resource is not found, whether it doesn't exist or if there was a 401 or 403 that, for security reasons, the service wants to mask. The server has not found anything matching the Request-URI. Used commonly when the server does not wish to reveal exactly why the request has been refused, or when no other response is applicable

* 409 Conflict - Indicates that the request could not be processed because of conflict in the request, such as an edit conflict. Whenever a resource conflict would be caused by fulfilling the request. The request could not be completed due to a conflict with the current state of the resource. This code is only allowed in situations where it is expected that the user might be able to resolve the conflict and resubmit the request.

* 5xx Server Error - Indicate cases in which the server is aware that it has erred or is incapable of performing the request. The server should include an entity containing an explanation of the error situation and whether it is a temporary or permanent condition. The server failed to fulfill an apparently valid request

* 500 Internal Server Error - The server encountered an unexpected condition which prevented it from fulfilling the request. A generic error message, given when no more specific message is suitable.