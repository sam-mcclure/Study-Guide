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
