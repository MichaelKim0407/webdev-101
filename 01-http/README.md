# HTTP

HTTP stands for HyperText Transfer Protocol.

[Wikipedia link](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)

## Client and Server

__Server__ is the provider of HTTP service.
__Client__ (also known as user-agent or UA) is the consumer of HTTP service.

Client and server don't have to be physically separate -
if you start a server in terminal and visit the url in a browser,
you will have both on the same machine.

There are different kinds of clients.
Mostly commonly (for non-developers) it will be a web browser,
but essentially a client only needs to be a application that can send HTTP requests and receive responses.
E.g.

* The [`curl`](https://linux.die.net/man/1/curl) bash command
* A Python program built with [`requests`](http://docs.python-requests.org/en/master/) package

Client and server also don't have to be different applications.
If you build a api server that scrapes another website,
then the same application will be a server when serving api calls,
and a client when scraping.

## Request and Response

In each HTTP interaction,
the client send the server a request,
and the server will process the request and send back a response.

### Request URL

URL stands for Universal Resource Locator.

[Wikipedia link](https://en.wikipedia.org/wiki/URL)

[MDN doc](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL)

```
scheme://host:port/path?query#fragment
```

* __Scheme__ (also protocol): for HTTP it will just be `http`, or `https` when the server is encrypted with SSL/TLS.
* __Host__: An identifier to locate the server. It can be an IP, or a domain name (e.g. `google.com`) that can be resolved into an IP with DNS. The IP `127.0.0.1` always refers to the same machine that the client is on. The word `localhost` is an alias for `127.0.0.1`.
* __Port__: The port on the server that is listening for HTTP requests. If omitted, by default it is `80`. A machine can run multiple HTTP servers on different ports, but each port can only bind to one server application.
* __Path__: A `/`-splitted path to refer to a specific resource. (e.g. `/student` a list of students)
* __Query__: A list of parameters to specify how the resource should be accessed. (e.g. `/student?order=first_name` a list of students ordered by first name)
* __Fragment__: A reference for the browser to display a particular part on the page (e.g. a paragraph or a tab). This part is most commonly ignored by the server.

### Request Methods

[MDN doc](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

[RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)
(this doc has been deprecated but is still a good reference)

__GET__ and __POST__ are the two most commonly used methods.

GET is a safe method which means it should not change the state on the server.

[Related Twitter thread](https://twitter.com/rombulow/status/990684453734203392)

### Response Codes

[Wikipedia link](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

[RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)
(this doc has been deprecated but is still a good reference)

Commonly used:

* `200` __OK__: The request is successful. Should contain a response according to the request.
* `302` __Found__: A directive to tell the client to visit another url for the requested resource, or "redirect". Should not contain anything other than the redirection information.
* `404` __Not Found__: The requested resource does not exist. Some web services prefer to use this code for resources that the client are not authorized to access, to hide implementation details.

Concerning web developers:

* `400` __Bad Request__: There is an error in the request.
* `403` __Forbidden__: The request is valid, but the server refuses to serve the resource. Most commonly used when the client does not have proper permissions.
* `405` __Method Not Allowed__: The request method is not valid for the requested resource.
* `500` __Server Error__: An error happened when the server tried to process the response.

Concerning web scraping:

* `429` __Too Many Requests__: When the client makes too many requests in a limited amount of time. Some servers implement a quota system or a frequency threshold to limit the load on the server. This is useful to check against when programmatically downloading/ scraping resources.

---

[Index](../README.md)
/
Next: [Server](../02-server/README.md)
