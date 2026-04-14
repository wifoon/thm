HyperText Transfer Protocol is set of rules used for communicating with web servers for transmitting of webpage data.

#### Methods

**GET Request**
This is used for getting information from a web server.  

**POST Request**
This is used for submitting data to the web server and potentially creating new records  

**PUT Request**
This is used for submitting data to a web server to update information

**DELETE Request**  
This is used for deleting information/records from a web server.

#### Requests

**Example Request:**

```http
GET / HTTP/1.1
# request is sending the GET method; request the home page with /; what protocol we are using HTTP ver 1.1

Host: tryhackme.com
# tell web server which website we want
User-Agent: Mozilla/5.0 Firefox/87.0
# which browser we are using
Referer: https://tryhackme.com/
```

**Example Response:**

```http
HTTP/1.1 200 OK
# protocol and version the server is using followed by the HTTP Status Code 200 OK means request has completed successfully

Server: nginx/1.15.8
# web server software and version
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
# tells the client what sort of information is going to be sent
Content-Length: 98
# tells the client how long the response is, this way we can confirm no data is missing.

<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>
```


#### Common HTTP Status Codes

| **200 - OK**                     | The request was completed successfully.                                                                                                                                                                                       |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **201 - Created**                | A resource has been created (for example a new user or new blog post).                                                                                                                                                        |
| **301 - Moved Permanently**      | This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere else and to look there instead.                                                                                |
| **302 - Found**                  | Similar to the above permanent redirect, but as the name suggests, this is only a temporary change and it may change again in the near future.                                                                                |
| **400 - Bad Request**            | This tells the browser that something was either wrong or missing in their request. This could sometimes be used if the web server resource that is being requested expected a certain parameter that the client didn't send. |
| **401 - Not Authorised**         | You are not currently allowed to view this resource until you have authorised with the web application, most commonly with a username and password.                                                                           |
| **403 - Forbidden**              | You do not have permission to view this resource whether you are logged in or not.                                                                                                                                            |
| **405 - Method Not Allowed**     | The resource does not allow this method request, for example, you send a GET request to the resource /create-account when it was expecting a POST request instead.                                                            |
| **404 - Page Not Found**         | The page/resource you requested does not exist.                                                                                                                                                                               |
| **500 - Internal Service Error** | The server has encountered some kind of error with your request that it doesn't know how to handle properly.                                                                                                                  |
| **503 - Service Unavailable**    | This server cannot handle your request as it's either overloaded or down for maintenance.                                                                                                                                     |
