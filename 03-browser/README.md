# Browser Rendering

A browser can be used to view any kind of resource (e.g. JSON, CSS, JavaScript, Image).
It can even be used to access resources that are not served with the HTTP protocol (e.g. `file://` or `ftp://`).
However, it will only render resources that are in the HTML format.
HTML is truly the backbone of the Internet.

## HTML

HTML stands for HyperText Markup Language

[Wikipedia link](https://en.wikipedia.org/wiki/HTML)

An HTML document is a text document that follows a specific syntax
so that the browser can understand it and render its content properly.
Like XML, it is structured with tags, attributes and raw texts.

### In-line Code

An HTML document can contain other languages when used with proper tags.
Most commonly, CSS and JavaScript can be included in the HTML document itself.
They will be served as a part of the HTML document.

### Referenced Resources

An HTML document can also contain references to other resources.
When the browser renders the document,
it will attempt to make separate requests to retrieve those resources.

Almost all media resources (images, audios and videos) are served via references.

It is also a common practice to serve CSS and JavaScript in this way whenever possible,
to reduce load/ save bandwidth on the server.

## Static Resources and Caching

[MDN doc](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)

By default, the browser considers some types of resources as "static".
This is a different concept from static files on the server side,
although it is a good practice to serve static resources as static files.

Most commonly,
resources that are CSS or JavaScript files are treated as static,
and the browser will cache them locally,
so next time you visit the same website,
the resources will not need to be loaded via the Internet again.
The intention to both save bandwidth and speed up the page loading process.

During development however, it can create a problem.
When you update your css/js files on the server side you would want them to be updated on the browser as well.
To force the browser to refresh cached resources,
hold the `Shift` key when refreshing,
e.g. `Shift` + `F5` on Windows or `Shift` + `Cmd` + `R` on Mac.

## Executing JavaScript

When rendering an HTML page,
if there is JavaScript included,
either as inline code or as referenced resource,
the browser will execute JavaScript scripts sequentially in the order they appear in the HTML file.

Two important points here:

* Unlike Python scripts that you can execute in the terminal using the command `python xxx.py`, JavaScript is executed by the browser, and instead of executing the script directly, you'll need to reference it in an HTML file.

* The order scripts appear in the HTML file is important. Libraries must be included first before any other script can use them. Also all JavaScript code on the same page will be executed in the same scope `window`, so a variable in a script can be used in another.

---


[Index](../README.md)
/
Prev: [Server](../02-server/README.md)
