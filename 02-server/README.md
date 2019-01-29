# Server

A server is an application that can receive HTTP requests and return responses.

## Static Server

A server that serves resources as-is from the file system.

Examples:

* Simple HTTP server with Python: `python -m http.server`
* [GitHub Pages](https://pages.github.com/)
* [Nginx](https://nginx.org/en/) (when serving static content)
* Public [s3](https://aws.amazon.com/s3/) bucket

## Application Server

A server that runs comprehensive code to determine the response.
This is where the job "backend developer" comes in.
It allows the server to process the request,
and have access to other services, e.g. databases.

Sometimes an application server has a section that serves static files (`/static`).

---

[Index](../README.md)
/
Prev: [HTTP](../01-http/README.md)
/
Next: [Browser Rendering](../03-browser/README.md)
