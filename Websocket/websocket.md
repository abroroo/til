
So, I got curious about [Tenserflow.js Models](https://www.tensorflow.org/js/models) after reading this [article](https://dev.to/devdevcharlie/acoustic-activity-recognition-in-javascript-2go4) in medium about sound recognizer. 

I wanted it to try it myself with Next.js. The goal was simple: use the microphone to capture sounds and then identify them based on predefined classes I'd set up with [Google Teachable Machine](https://teachablemachine.withgoogle.com/v1/)

Starting on the frontend, I needed a way to access the user's microphone. 

I learned that I can achieve this with [WebRTC API](https://developer.mozilla.org/en-US/docs/Glossary/WebRTC)  which is native to browsers. Once I had access to the raw audio, I discovered the [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) which helped me convert those sound waves into actionable data points.

Now, to get this data over to the backend for processing, I faced a problem. 

Given the real-time nature of what I wanted to achieve **capturing and analyzing audio every millisecond** I couldn't rely on traditional methods like fetch or axios. That's where I learned about WebSockets. 

### Alright, so what's the deal with WebSockets?

> The [WebSocket API](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) is an advanced technology that makes it possible to open a two-way interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply.

In other words: 

Instead of constantly setting up new connections between the frontend and backend every time when you need to send or receive data, WebSockets set up this cool handshake thing. WebSockets Handshake ```ws://``` or with SLL `wss://`. It's like they're creating a direct line between your browser and the server. This way, they can shoot data back and forth super quickly, making it perfect for stuff like chat apps where you want things to happen instantly.

It's mostly used in chat apps where sending and receiveing data should be very fast in real time. 

