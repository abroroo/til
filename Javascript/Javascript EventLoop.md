```
    +---------------------------------------------------+
    |                   Event Loop                      |         
    + --------------------------------------------------+
    |                                                   |
    |      +---------------+                            |                                +---------------+                            
    |      | Callback Queue|                            |                                |   Web APIs    |
    |      +---------------+                            |                                +---------------+ 
    |      |  setTimeout() |                            |       (async op completed)     | setTimeout()  |
    |      |   callback    | < - - - - - - - - - - - - - - - - - - - - - - - - - - - - - | XMLHttpReq... |
    |      |   eventHandler|                            |                                | addEventListener|
    |      +---------------+                            |                                +---------------+   
    |                |                                  |      
    |                | (After microtasks is empty)      |     
    |                V                                  |      
    |      +---------------+                            |            
    |      |Microtask Queue|                            |  
    |      +---------------+                            |            
    |      |  promise.then |                            |            
    |      |  queueMicro...|                            |  
    |      |  queueMicro...|                            |                             
    |      |   async/await |                            |
    |      |  queueMicro...|                            |  
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
(Color legend:
Red: Web APIs
Green: Callback Queue
Blue: Microtask Queue
Black: Call Stack)
