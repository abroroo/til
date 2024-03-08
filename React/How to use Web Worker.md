# What's Web Worker: 
A [web worker](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) is a browser feature where you can run additional scripts, some computations in separate from the main execution thread where the web page is running.

Web workers have their own event loop, separate from the main JavaScript event loop. This means that they have their own call stack, microtask queue, and callback queue, allowing them to operate independently without interfering with the main thread's event loop.

# How to use Web Worker in React: 

