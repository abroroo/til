# Javascript Event Loop:
The event loop is a continuous process that monitors both the call stack and the callback queue. It follows these steps:
### How it works: 
- If the __call stack__ is empty, the event loop first checks the __microtasks__ queue.
- If the __microtasks queue is not empty__, the event loop dequeues the first callback function and pushes it to the call stack for execution.
- If the __call stack is not empty__, the event loop __waits for__ the current function to complete __and continue__ checking the __call stack and microtasks queue__.
- If the __microtasks queue is empty__, the the event loop dequeues the first callback function in the __callback queue__ and pushes it to the call stack for execution.

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

## Web APIs: 
Web APIs, such as __setTimeout__, __XMLHttpRequest__, and __event listeners__, are provided by the browser environment. When you use these APIs, they handle the asynchronous operations and push the corresponding callback functions into the callback queue once their tasks are completed.

