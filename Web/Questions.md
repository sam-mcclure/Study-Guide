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

# Week 2

## HTTP

1. What are the common HTTP methods? When are they used, and what do they accomplish? (This is a big one)
    1. GET - Used to retrieve information from the given server using a given URI. Should only retrieve data. Main method used for document retrieval
    2. HEAD - Similar to GET, but server only sends back response line and header (no body)
    3. POST - Used to send data to the server from an HTML form (customer info, file upload, etc)
    4. PUT - Replaces all current represenatations of the target resource with the uploaded content, ie 'store the included data at a location specified by the URL'
    5. DELETE - Removes all current representations of the target resource given by a URI, used to delete the given file at the root of the server
    6. CONNECT - Establishes a tunnel to the server identified by a URI, used by the client to establish a network connection to a web server over HTTP
    7. OPTIONS - Describes the communication options for the target resource, used by the client to find out the HTTP methods and other options supported by a web server
    8. TRACE - Performs a messages loop-back test along the path to the target resource, used to echo the contents of an HTTP Request back to the requester for debugging

2. What are the 10 most common Status Codes?
    1. 200 OK
    2. 201 Created
    3. 204 No Content
    4. 304 Not Modified
    5. 400 Bad Request
    6. 401 Unauthorized
    7. 403 Forbidden
    8. 404 Not Found
    9. 409 Conflict
    10. 500 Internal Server Error

3. What are the types of status codes?
- 1xx - Informational, 2xx - Success, 3xx Redirection, 4xx - Client Error, 5xx - Server Error
