

I wanted simple experiment with [Tenserflow.js Models](https://www.tensorflow.org/js/models).  So I wanted to create a sound recognizer, for that I needed to be able to listen to user's microphone and recognize classes I created with [Goole Teachable Machine](https://teachablemachine.withgoogle.com/v1/) 

So in the frontend I could get acces to user's mic with WebRTC then create an object to convert audio into data with Web Audio API. Then send the data to the backend, to tenseflow's speech-command model(the only model that works with audio), which will send back percentage of predictions for each class by analyzing received audio. 

The things, I cannot use fetch or axios to send audio data to the server since I want it to send audio data in real time every secons or milliseconds, for that as i learned i needed WebSocket.

### so what's web socket ? 
Websocket is a service that enables to do http requests constantly from both sides(frontend, backend etc.) It creates a handshake(a one bridge between sides) though which both client and server can in real time send each other data with least possible delay.  

Websocket is mostly used in chat apps, where you need to send messages in real time between client and server. 
