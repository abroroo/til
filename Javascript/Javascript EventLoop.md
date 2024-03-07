# Event Loop:
The event loop is a continuous process that monitors both the call stack and the callback queue. It follows these steps:

     - If the call stack is empty, the event loop checks the microtasks queue.
     - If the microtasks queue is not empty, the event loop dequeues the first callback function and pushes it to the call stack for execution.
     - If the call stack is not empty, the event loop waits for the current function to complete and continue checking the call stack and microtasks queue.
     - If the microtasks queue is empty, the the event loop dequeues the first callback function in the callback queue and pushes it to the call stack for execution.

```
    +---------------------------------------------------+
    |                   Event Loop                      |         
    + --------------------------------------------------+
    |                                                   |
    |      +---------------+                            |                                +-----------------+                            
    |      | Callback Queue|                            |                                |   Web APIs      |
    |      +---------------+                            |                                +-----------------+ 
    |      |  setTimeout() |                            |       (async op completed)     | setTimeout()    |
    |      |   callback    | < - - - - - - - - - - - - - - - - - - - - - - - - - - - - - | XMLHttpReq...   |
    |      |   eventHandler|                            |                                | addEventListener|
    |      +---------------+                            |                                +-----------------+   
    |                |                                  |      
    |                | (After microtasks is empty)      |     
    |                V                                  |      
    |      +---------------+                            |            
    |      |Microtask Queue|                            |  
    |      +---------------+                            |            
    |      |  promise.then |                            |                                          
    |      |  queueMicro...|                            |                             
    |      |  async/await  |                            |                       
    |      +---------------+                            |  
    |                |                                  |      
    |                | (After call stack is empty)      |    
    |                V                                  |      
    |      +---------------+                            |  
    |      |   Call Stack  |  <-- Executes the code     |            
    |      +---------------+                            |  
    |      |   foo()       |                            |  
    |      |   bar()       |                            |  
    |      | promiseChain()|                            |  
    |      +---------------+                            |  
    |                                                   | 
    |                                                   |
    +---------------------------------------------------+     


```

Web APIs: Web APIs, such as setTimeout, XMLHttpRequest, and event listeners, are provided by the browser environment. When you use these APIs, they handle the asynchronous operations and push the corresponding callback functions into the callback queue once their tasks are completed.

