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

## HTTP vs HTTPS

* Asymmetric key cryptography - even if you can encrypt a message, you can't decrypt it. The box it's put into is called the public key and the key to open it is the private key 

* Certification Authority - a signature from a trusted source on a trusted source

* HTTPS is a more secure version of HTTP. The computers send a code between them and then they scramble the messages using that code so that no one in between can read them. This keeps info safe from hackers. They use the code on a Secure Sockets Layer (SSL) to send the info back and forth

* HTTPS is the procedure for encrypting information and then exchanging it (HyperText Transfer Protocol Secure)

* Benfits of HTTPS:
    - Customer information, like credit card numbers, is encrypted and cannot be intercepted
    - Visitors can verify you are a registered business and you own the domain
    - Customers are more likely to trust and complete purchases from sites that use HTTPS

## GET vs POST

* GET is used to request data from a specified resource. It is one of the most common HTTP methods. The query string (name/value pairs) is sent in the URL of a GET request
- Can be cached
- Remain in the browser history
- Can be bookmarked
- Should never be used when dealing with sensitive data
- Have length restrictions
- Only used to request data (not modify)

* POST is used to send data to a server to create/update a response. The data sent the the server with POST is stored in the request body of the HTTP request. One of the most common HTTP methods
- Never cached
- Do not remain in the browser history
- Have no restrictions on data length

* PUT is used to send data to a server to create/update a resource. The difference between POST and PUT is that PUT requests are idempotent. That is, calling the same PUT request multiple times will always produce the same result. In contrast, calling a POST request repeatedly will create the same resource multiple times

* HEAD is almost identical to GET, but without a response body. In other words, if GET /users returns a list of users, then HEAD /users will make the sam request but will not return the list of users. They're useful for checking what a GET request will return before actually making a GET request - like before downloading a large file or response body

* The DELETE method deletes the specified resource

* The OPTIONS method describes the communication options for the target resource

* For GET: back button/reload is harmless, can be bookmarked, can be cached, uses application/x-www-form-urlencoded, parameters remain in browser history, there are restrictions on data length (when sending data, the GET method adds the data to the URL and the length of a URL is limited to 2048 characters), only ASCII characters are allowed, GET is less secure than POST because the data sent is part of the URL (never use GET when sending passwords or other sensitive info!),
and the data is visible to everyone in the URL

* For Post: hitting the back button/reload will resubmit the data (browser should alert the user), cannot be bookmarked, not cached, uses application/x-www-form-urlencoded or multipart/form-data (for binary data), parameters are not saved in browser history, no restrictions on data length, no restrictions on data type, POST is a little safer than GET because the parameters are not stored in browser history or web server logs, and data id not displayed in the URL

## PUT vs PATCH

* The PUT method requests that the enclosed entity be stored under the supplied Request-URI. If the Request-URI refers to an already existing resource, the enclosed entity SHOULD be considered as a modified version of the one residing on the origin server. If the request-URI does not point to an existing resource, and that URI is capable of being defined as a new resource by the requesting user agent, the origin server can create the resource with that URI

* The PATCH method requests that a set of changes described in the request entity be applied to the resource identified by the Request-URI

* PUT might be used to replace the entire entity (instead of a set of attributes as with PATCH)

## localStorage vs sesionStorage vs cookies 

* localStorage, sessionStorage, and cookies are all client storage solutions. Session data is held on the server where it remains under your direct control

* localStorage and sessionStorage are relatively new APIs (not all legacy browsers support them) and are near identical (both in APIs and capabilities) with the sole exception of persistence. 

* sessionStorage is only available for the duration of the browser session and is deleted when the tab or window is closed, though it does survive page reloads.

* If the data you are storing needs to be available on an ongoing basis, then localStorage is preferrable to sessionStorage - though both can be cleared by the user, so you should not rely on the continuing existance of data in either case. 

* localStorage and sessionStorage are perfect for persisting non-sensitive data needed within client scripts between pages (ie preferences, scores in games). 

* The data stored in localStorage and sessionStorage can easily be read or changed from within the client/browser, so should not be relied upon for storage of sensitive or security-related data within applications

* Cookies can also be trivially tampered with by the user and data can be read from them in plain text. 

* If you want to store sensitive data, then the session is your only option. If you're not using SSL, cookie information can also be intercepted in transit.

* Cookies can have a degree of protection applied from security risks such as Cross-site Scriptin(XSS)/Script injection by setting an HTTP only flag which means modern browsers will prevent access to the cookies and values from JavaScript.

* As cookies are used for authentication purposes and persistence of user data, all cookies valid for a page are sent from the browser to the sever for every request to the same domain. For this reason, cookies should not be used to store large amounts of information.

* Typically cookies are used to store identifying tokens for authentication, session, and advertising tracking.

* In terms of capabilities, cookies, sessionStorage, and localStorage only allow you to store string - it is possible to implicitly convert primitive values when setting but not Objects or arrays. Session storage will generally allow you to store any primitives or objects supported by your Server Side language/framework

* As HTTp is a stateless protocol, web applications have no way of identifiying a user from previous visits on returning to the website, so session data usually relies on a cookie token to identify the user for repeat visits.

* As session data is completely controlled by your application (server side), it is the best place for anything sensitive or secure in nature.

* The obvious disadvantage of server-side data is scalability - server resources are required for each user for the duration of the session, and that any data needed client side must be sent with each request. Session data must expire after a given time to avoid all server resources being taken up by abandoned sessions.

* When using session data, you should, therefore, be aware of the possibility that data will have expired and been lost, especially on pages with long forms. 

* localStorage, sessionStorage, and cookies are all subject to 'same-origin' rules, which means browsers should prevent access to the data except the domain that set the information to start with