
So, I got curious about [Tenserflow.js Models](https://www.tensorflow.org/js/models) after reading this [article](https://dev.to/devdevcharlie/acoustic-activity-recognition-in-javascript-2go4) in medium.

I wanted it to try it myself with Next.js. The goal was simple: use the microphone to capture sounds and then identify them based on predefined classes I'd set up with [Google Teachable Machine](https://teachablemachine.withgoogle.com/v1/)

Starting on the frontend, I needed a way to access the user's microphone. 

I learned that I can achieve this with [WebRTC API](https://developer.mozilla.org/en-US/docs/Glossary/WebRTC)  which is native to browsers. Once I had access to the raw audio, I discovered the [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) which helped me convert those sound waves into actionable data points.

Now, to get this data over to the backend for processing, I faced a problem. 

Given the real-time nature of what I wanted to achieve **capturing and analyzing audio every millisecond** I couldn't rely on traditional methods like fetch or axios. That's where I learned about WebSockets. 

### So what's the deal with WebSockets?

> The [WebSocket API](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) is an advanced technology that makes it possible to open a two-way interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply.

In other words: 

Instead of constantly setting up new connections between the frontend and backend every time when you need to send or receive data, WebSockets set up this cool handshake thing. WebSockets Handshake ```ws://``` or with SLL `wss://`. It's like they're creating a direct line between your browser and the server. This way, they can shoot data back and forth super quickly, making it perfect for stuff like chat apps where you want things to happen instantly.

### How to set up socket in nextjs?

You can use npm packages, most common ones are [socket.io](https://www.npmjs.com/package/socket.io) for server side and [socket.io/client](https://www.npmjs.com/package/socket.io-client) for client side. 

In your `pages/api` directory
```
// pages/api/socket.js

import { Server } from "socket.io";

export default function handler(req, res) {
  if (!res.socket.server.io) {
    console.log("Starting socket.io");

    const httpServer = res.socket.server;
    const io = new Server(httpServer, {
      /* options */
    });


// 'connection' is event for setting up connection for server side 
    io.on("connection", (socket) => {
      console.log("New client connected");

    // define event name to listen to in this case it's 'audioData' 
      socket.on("audioData", (data) => {
        console.log("Data received from client:", data);


        const mutatedData = // do things with received data and send it back
        io.emit("soundPrediction", mutatedData);
      });

      socket.on("disconnect", () => {
        console.log("Client disconnected");
      });
    });

    res.socket.server.io = io;
  }

  res.end();
}

```

Your client side 

```
import { useEffect } from 'react';
import io from 'socket.io-client';

export default function SomeComponent() {
const audio = ['Data'];
  useEffect(() => {
    const socket = io.connect('/api/socket');

// for clinet 'connect' is event to set up connection
    socket.on('connect', () => {
      console.log('Connected to server');

// server is listening to 'audioData' event, so you can send audio data
      socket.emit('audioData', audio);
    });

// 'soundPrediction' is the eventName where server is sending data, so client is listening to it 
    socket.on('soundPrediction', (data) => {
      console.log('Received data from server:', data);
    });

    socket.on('disconnect', () => {
      console.log('Disconnected from server');
    });

    return () => {
      socket.disconnect();
    };
  }, []);

  return (
    <div>
     
      {/* Your components or content here */}
    </div>
  );
}


```




