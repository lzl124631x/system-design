# Server-to-client Communication

It's not uncommon that we want our client to proactively get the latest data from the server, or the server sends the latest data to the client.

A few ways to implement these:

* Short/Long Polling \(client pull\)
* WebSockets \(server push\)
* Server-Sent Events \(server push\)

## Short Polling

The client keeps sending request to the server periodically.

Pro: Easy to implement

Con: Waste system resource since lots of those requests will get empty response.

## Long Polling

Instead of returning the client request right away with empty response, the server holds the client connection open for as long as possible. It sends back a response only after the data becomes available or timeout threshold has been reached.

A flow for Long polling will look as follows

1. A client initiates an XHR/AJAX request, requesting some data from a server.
2. The server does not immediately respond with request information but waits until there is new information available.
3. When there is new information available, the server responds with new information.
4. The client receives the new information and immediately sends another request to the server restarting the process.

Pro: More efficient than short polling.

Con: With one HTTP handshake, the server can send response only once.

## WebSocket

WebSocket isa **computer communication protocol** which provides **full-duplex** communication channels over **a single TCP connection.**

* It's different from HTTP but compatible with HTTP.
* Located at layer 7 in the OSI model and depends on TCP at layer 4.
* Works over port 80 and 443 \( in case of TLS encrypted\) and supports HTTP proxies and intermediaries.
* To achieve compatibility, the WebSocket handshake uses _Upgrade_ header to update the protocol to the WebSocket protocol.

The WebSocket protocol enables interaction between a client and a web server with lesser overheads, providing real-time data transfer from and to the server. WebSockets keeps the connection open, allowing messages to be passed back and forth between the client and the server. In this way, a two-way ongoing conversation can take place between the client and the server.

![](.gitbook/assets/image%20%2836%29.png)

A WebSocket connection flow will look something like this.

1. A client initiates a WebSocket handshake process by sending a request which also contains _Upgrade_ header to switch to WebSocket protocol along with other information.
2. The server receives WebSocket handshake request and process it.
   1. If the server can establish the connection and agrees with client terms then sends a response to the client, acknowledging the WebSocket handshake request with other information.
   2. If the server can not establish the connection then it sends response acknowledging it cannot establish WebSocket connection.
3. Once the client receives a successful WebSocket connection handshake request, WebSocket connection will be opened. Now, client and servers can start sending data in both directions allowing real-time communication.
4. The connection will be closed once the server or the client decides to close the connection.

Example:

Client Side:

![](.gitbook/assets/image%20%2812%29.png)

Server Side:

![](.gitbook/assets/image%20%2819%29.png)

Pro:

* Full-duplex
* With a single HTTP handshake, multiple messages can be sent between a client and a server.

Con:

* Since WebSocket isn't really HTTP, some of the IT infrastructure might not work well with WebSocket like load balancer, firewall, etc.
* WebSockets don’t automatically recover when connections are terminated – this is something you need to implement yourself, and is part of the reason why there are many client-side libraries in existence.

WebSocket is the best solution for a real-time applications like chat room.

## Server-Sent Events

Unlike WebSockets, Server-Sent Events are a **one-way communication channel** where events flow from **server to client only**. Server-Sent Events allows browser clients to receive a stream of events from a server over an HTTP connection without polling.

A client subscribes to a “stream” from a server and the server will send messages \(“event-stream”\) to the client until the server or the client closes the stream. It is up to the server to decide when and what to send the client, for instance as soon as data changes.

![](.gitbook/assets/image%20%282%29.png)

A flow for server send events will be as follows.

1. Browser client creates a connection using an EventSource API with a server endpoint which is expected to return a stream of events over time. This essentially makes an HTTP request at given URL.
2. The server receives a regular HTTP request from the client and opens the connection and keeps it open. The server can now send the event data as long as it wants or it can close the connection if there are no data.
3. The client receives each event from the server and process it. If it receives a close signal from the server it can close the connection. The client can also initiate the connection close request.

Pro:

* As SSE is based on HTTP, it is more compliant with existing IT infrastructure like \(Load Balancer, Firewall, etc\), unlike WebSockets which can be blocked by some firewall.

Con:

* Server-Sent events are not supported by all browsers.

Use cases:

* A real-time chart of streaming stock prices
* Real-time news coverage of an important event \(posting links, tweets, and images\)
* A live Twitter dashboard wall fed by Twitter’s streaming API
* A monitor for server statistics like uptime, health, and running processes.

## Reference

1. [https://medium.com/system-design-blog/long-polling-vs-websockets-vs-server-sent-events-c43ba96df7c1](https://medium.com/system-design-blog/long-polling-vs-websockets-vs-server-sent-events-c43ba96df7c1)
2. [https://www.ably.io/blog/websockets-vs-long-polling/](https://www.ably.io/blog/websockets-vs-long-polling/)



