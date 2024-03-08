# What's Web Worker: 
A [web worker](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) is a browser feature where you can run, some computation or additional scripts, separately from the main execution thread where the web page is running.

Web workers have their own event loop, separate from the main JavaScript event loop. This means that they have their own call stack, microtask queue, and callback queue, allowing them to operate independently without interfering with the main thread's event loop.

# How to use Web Worker in React: 

 - First, create a new file for the Web Worker, let's call it worker.js. This file will contain the logic that you want to run in a separate thread:
```javascript
  // worker.js
self.addEventListener('message', (event) => {
  // Receive data from the main thread
  const data = event.data;

  // Perform some computationally intensive task
  const result = computeIntensiveTask(data);

  // Send the result back to the main thread
  self.postMessage(result);
});

function computeIntensiveTask(data) {
  // Perform some long-running or computationally intensive task
  // ...
  // Return the result
  return result;
}

   ```
In your React component, you can create and use the Web Worker like this:

```javascript


```
