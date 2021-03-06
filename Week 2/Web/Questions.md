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

4. What is the difference between HTTP and HTTPS?
- HTTP does not use any kind of encryption, so it is not secure and is open to hacking. HTTPS adds encryption to the connection, protecting sensitive information.

## localStorage/sessionStorage/cookies

5. What is the difference between localStorage and sessionStorage?
- They are very similar, except for pesistence. sessionStorage is only available for the duration of the browser session and is deleted when the tab or window is closed. localStorage will presist until cleared by the user

6. Why is it important that users cannot modify their cookies?
- Cookies are typically used for user authentication and anyone with that cookie could become that user. Cookies have some built in. If a user could modify the cookie, it would be easy for them to attack the site with Script injection or login as other users

7. When are cookies sent to the server?
- Every time an HTTP request is sent

## XSS

8. What is the danger of an XSS?
- If a web application uses unvalidated or unencoded user input in the output it generates, a hacker can use Cross-site  Scripting to input malicious code into a form that will attack a user's browser when they navigate to that page. These scripts have access to anything JavaScript has access to and can be used for cookie theft, keylogging, phising, and identity theft.

## CSRF

9. What is a CSRF Attack?
- A CSRF attack is when an attacker tricks a user into clicking on a link or loading a page that then sends a malicious request to a website that the user is logged in to, using the victim's cookies to make it seem like a legitimate request. CSRF can be used to transfer money, change passwords, and steal data.

10. How can you prevent CSRF Vulnerabilities?
- The most common way to prevent CSRF attacks is to send a hidden anti-CSRF token with a submitted form. This token should be hard to guess and requests will only be accepted with the correct token. Another way to prevent CSRF is to use a same-site cookie, meaning a cookie that came from the same source as the cookie is being sent to. However, this is not supported in all browsers, so shouldn't be used except as an extra layer of defense
