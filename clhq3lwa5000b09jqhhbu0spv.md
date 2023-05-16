---
title: "What is HTTP"
seoTitle: "What is HTTP"
seoDescription: "HTTP stands for Hyper Text Transfer Protocol."
datePublished: Tue May 16 2023 09:55:26 GMT+0000 (Coordinated Universal Time)
cuid: clhq3lwa5000b09jqhhbu0spv
slug: http-in-a-brief-55dd5f35029f
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684230798548/b3fa78ac-22f6-4815-a311-7760713b8fab.jpeg
tags: http, javascript, web-development, computer-science, internet

---

#### What is HTTP?

HTTP stands for Hyper Text Transfer Protocol. So, it’s a protocol that’s used to transfer hypertext. In this context the term Hypertext means a text that contains links to other texts. It can be link of music videos or any other information too. So, we can say that:

> Hypertext Transfer Protocol is the set of rules, servers and browsers used to transfer web documents back and forth.

#### Principles of HTTP

HTTP is a synchronous protocol, which in this case means that after a client sends a request to a server, it waits for a single response. The server can only respond to requests. It cannot initiate a connection to the client.

Another principle is that HTTP is a stateless protocol. That means each individual request sent over the protocol is unique, and no request is connected to another request. This means a HTTP server needs not keep track of any state information. A HTTP server will not remember whether a client has visited it before, or how many time.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230785474/70cee6e0-1ea8-438a-92ef-534be8840489.png)

To fix this, http allows sessions. Stores the states between browser and server. So, http is stateless not session less. To share the information about where the user is in the sequence it uses cookies. In short we can say that cookies keep track of the user of that particular session.

> **Cookies:** An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to the user’s web browser. The browser may store it and send it back with later requests to the same server. Typically, it’s used to tell if two requests came from the same browser — keeping a user logged-in, for example. It remembers stateful information for the [stateless](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview#HTTP_is_stateless_but_not_sessionless) HTTP protocol.

Another principle is that http work on request and response pairs. Every action performed over HTTP starts with a request using one of the HTTP methods and ends with a response containing an HTTP status code saying what happened to the request along with the data like headers and content.

#### HTTP Workflow

First, the browser opens a [*TCP*](https://en.wikipedia.org/wiki/Transmission_Control_Protocol) (Transmission Control Protocol) connection to the server. This ensures data can be sent back and forth over the network and that the data sent from one end is put together the same way at the other end. If the connection happens over *HTTPS*, [*TLS*](https://www.cloudflare.com/learning/ssl/transport-layer-security-tls/) (Transport Layer Security) certificates are exchanged to ensure only the computer and the server can encrypt and decrypt the transmitted data. This prevents anyone from being able to eavesdrop on the conversation between the client and the server and steal the data they are transmitting.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230787895/465810a1-a819-4f1f-a567-3ba5ec02ac87.jpeg)

Second, the browser sends HTTP message containing HTTP methods like GET, PUT, DELETE, CONNECT, OPTIONS, HEAD, TRACE, PATCH and similar with a [*URL*](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL) pointing to the resource. It can also contain headers like cookies and authentication data and other data.

Third, the server process the request and sends a HTTP response containing some status code, headers with information about the response and the data was requested.

Finally the response is fully accepted, the TCP connection is closed. n most scenarios, the first HTTP transaction between a browser and a server is to retrieve a web document for a page or a view. This document typically holds links to CSS and JavaScript files as well as referenced elements like images.

#### HTTP/2

[HTTP/2](https://developers.google.com/web/fundamentals/performance/http2) is the upgraded version of HTTP that will make applications faster simpler and more optimized.

The primary goals for HTTP/2 are to reduce latency by enabling full request and response [multiplexing](https://stackoverflow.com/questions/36517829/what-does-multiplexing-mean-in-http-2), minimize protocol overhead via efficient compression of HTTP header fields, and add support for request prioritization and server push.

#### HTTPS

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230789252/f16f5fe6-9078-4506-a677-38a7dd56f178.png)

Hypertext transfer protocol secure ([HTTPS](https://www.cloudflare.com/learning/ssl/what-is-https/)) is the secure version of [HTTP](https://www.cloudflare.com/learning/ddos/glossary/hypertext-transfer-protocol-http/), which is the primary protocol used to send data between a web browser and a website. [HTTPS](https://www.cloudflare.com/learning/ssl/what-is-https/) is encrypted in order to increase security of data transfer. Cause we dont want to expose sensitive information in the web . In modern web browsers such as Chrome, websites that do not use HTTPS are marked differently than those that are.

#### Request/Response Pair

The core component of HTTP is Request/Response pair. Any operation happening on the website like clicking on a submit button or clicking into a link the browser sends a request and then the server gives a response to that.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230790499/70f6150b-ebc5-42e0-a7d3-d5207891310e.png)

> you can get the request and response details by getting into the browser developer console by pressing f12 or ctrl + shift + i (for windows/Linux) or cmd + option + i (for MAC). Then get to the network tab and refresh your browser tab and you can see all the request and responses and their method and more details too!

#### HTTP Methods

Every request sent over the HTTP protocol includes a method, aka a verb. This method tells the server what type of action we want to perform with the request. There are several types of methods:

**GET:**

The GET method requests a representation of the specified resource. Requests using GET should only retrieve data.

**HEAD:**

The HEAD method is similar to the GET method. But HEAD method only gives us the data of the response body.

**POST:**

The POST method is used to submit an entity to the specified resource, which causes change in state on the server.

**DELETE:**

The DELETE method deletes the resource.

**PUT:**

PUT request contains the ID of a resource and the new content to be added to that resource. If the resource already exists, the existing content is replaced with the contents in the PUT request. If no resource with this ID exists, the server will in some cases allow the new resource to be created with the user defined ID or you’ll get an error message.

**CONNECT:**

This specification reserves the method name CONNECT for use with a proxy that can dynamically switch to being a tunnel.

**OPTIONS:**

Returns a description of the communication options for the target resource.

**TRACE:**

The TRACE method is used to invoke a remote, application-layer loop- back of the request message.

#### HTTP Status codes:

When HTTP request is sent the server returns a HTTP response which includes a status code which explains what happened into the server. It can contain error codes too.

HTTP status codes are split into five different groups:

1.  ***Informational Responses (100–199):***

It contains codes like **“100 continue”** that means everything is fine and client should continue the request. **“101 switching protocol”** this code is sent in response to an upgrade request header from the client, and indicates the protocol the server is switching to. **“103 Early Hints”** This status code is primarily intended to be used with the link header letting the user start preloading resources while browser starts and so on.

***2\. Successful responses(200–299):***

It contains like **“200 OK”** which means request was successful, **“201 created”** that means request was successful and in return of that a new resource was created, **“202 Accepted”** states the request was accepted but not yet acted upon, **“204 no content ”** There is no content to send for this request, but the headers may be useful. The user-agent may update its cached headers for this resource with the new ones and many more.

***3\. Redirection Responses(300–399):***

Contains codes like **“301 moved permanently”** meaning url resource has changed permanently, **“302 Found”** stating that This response code means that the URI of requested resource has been changed *temporarily*. Further changes in the URI might be made in the future. Therefore, this same URI should be used by the client in future requests. **“304 not found”** used for caching purposes. It tells the client that the response has not been modified, so the client can continue to use the same cached version of the response and other codes.

***4\. Client Errors (400–499):***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230792893/58a6ccfe-6989-4d95-8d9c-b133de6863a4.png)

It contains status codes like **“404 Not Found”** means the content not found, **“400 Bad Request”** the server could not understand the request due to invalid syntax, **“403 Forbidden”** meaning the client does not have access to the specified content and many others.

**5\. Server Errors (500–599):**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230794369/c55b36fe-a41c-4bbe-b122-43e6a6a3727a.png)

Status codes like **“500 internal server error”** which means The server has encountered a situation it doesn’t know how to handle, **“502 Bad gateway”** meaning while working as a gateway to get a response needed to handle the request, got an invalid response, **“504 Gateway Timeout”** which states This error response is given when the server is acting as a gateway and cannot get a response in time.

> There are many more status codes which I’ve not included. You can learn this from [here.](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

#### HTTP Headers:

> An HTTP header is a human readable name value pair separated by a colon, added to the HTTP request or response, which can be used to pass standard or custom information back and forth between the client and the server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230795634/5796cbbe-232f-4527-bf32-ee5bf0de8640.png)

The request header is the message a client application sends over HTTP to the server, requesting to perform an action on a specific resource.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230797158/4a9fd809-de84-4063-bac1-3fe34c074d1e.png)

If there is a server at the requested address specified in the request header, that server will return a response even if that response is simply not found.

#### Caching:

The performance of websites can be improved by fetched resources. In websites there are files that are rarely updated like the JavaScript files, CSS files etc. Both server and client can cache the files means store the files for later use. Once cached the files will be used instead of downloading fresh ones which results dramatically speed up and performance of the site. There are two types of cache **1) Private Cache and 2) Shared Cache.**

**Conclusion:**

This are the basic fundamentals of HTTP.