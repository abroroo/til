### What's WebRTC? 
(Web Real-Time Communication)
[WebRTC](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API) allows two browsers to talk directly to each other without needing a server in the middle. 
Built with set of protocols and APIs, it can give access to microphone, camera and enables to connect with other browsers. 
WebRTC is mostly useful for video streams or phone calls via the web ([used](https://medium.com/swlh/webrtc-the-technology-that-powers-google-meet-hangout-facebook-messenger-and-discord-cb926973d786) in Goole Meets, Discord)  

### How to use WebRTC? 
There are three most common use cases
#### 1. Get User Media (Access to Microphone & Camera):
To initiate a media connection, you'll typically want to capture audio and/or video from the user's device. You can use `navigator.mediaDevices.getUserMedia` for this:
```
// Request access to the user's microphone and camera
navigator.mediaDevices.getUserMedia({ audio: true, video: true })
  .then(stream => {
    // 'stream' is the MediaStream containing both audio and video tracks

    // Accessing audio tracks from the MediaStream
    const audioTrack = stream.getAudioTracks()[0];
    console.log('Audio Track:', audioTrack);

    // Accessing video tracks from the MediaStream
    const videoTrack = stream.getVideoTracks()[0];
    console.log('Video Track:', videoTrack);

    // You can use 'audioTrack' and 'videoTrack' to manipulate or display the audio and video data.
    // For example, you can attach them to HTML elements for display.
  })
  .catch(error => {
    console.error('Error accessing media devices:', error);
  });


```
#### 2. Set Up Connection (For Audio & Video)
Think of RTCPeerConnection as the you set up a direct line between the two browsers. 
It's the technology that lets you chat or call someone directly over the internet without a middleman. 
You can use `RTCPeerConnection` to establish a connection with a remote peer:
```
const configuration = { iceServers: [{ urls: 'stun:stun.l.google.com:19302' }] };
const peerConnection = new RTCPeerConnection(configuration);

// Add the stream to the peer connection
stream.getTracks().forEach(track => peerConnection.addTrack(track, stream));

```
#### 3. Send and Receive Messages (Data)
RTCDataChannel is a feature that allows you to send extra bits of information directly to the other person while you're on a call. 
Think of it as sending a text message or sharing a small file while you're on a video call.
You create an `RTCDataChannel` on the peer connection:

```
const dataChannel = peerConnection.createDataChannel('myDataChannel');

dataChannel.onopen = () => {
  console.log('Now, you can send messages directly!');
};

dataChannel.onmessage = event => {
  console.log('Received a message:', event.data);
};


```

