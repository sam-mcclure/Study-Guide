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