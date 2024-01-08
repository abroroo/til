### Here is how it works: 
First client makes a HTTP 1.1 request with special `UPGRADE: websocket` header in that request, and when server receives it, it will upgrade the protocol sending back `101 - Switching Protocols` and that's the HandShake essentially. 

#### Here's how sample WebSocket Handshake looks like 

#### Client 

```
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-Websocket-Key: x3JJHMbDLEzLkh9Gv3d...
Sec-Websocket-Protocol: chat, superchat
Sec-Websocket-Version: 13
Origin: https://example.com
```
Client just do GET request with these headers, the headers like `Sec-Websocket-` are needed for the server to do some hashing and seeding and send back `Sec-Websocket-Accept` to the client so that client can verify and authenticate the server who's is sending the request. 

#### Server

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Sec-Websocket-Accept: HSmrcw0ksdlsdfs3mfdfg1DLkls...
Sec-Websocket-Protocol: chat
```


