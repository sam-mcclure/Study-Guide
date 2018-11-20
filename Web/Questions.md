# REST

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