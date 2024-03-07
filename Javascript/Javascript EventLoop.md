+---------------+
|   Web APIs    |
+---------------+
| setTimeout()  |
| XMLHttpReq... |
| addEventListener|
+---------------+
          |
          | (async op completed)
          V
+---------------+
| Callback Queue|
+---------------+
|  setTimeout() |
|   callback    |
|   eventHandler|
+---------------+
          |
          | (After microtasks)
          V
+---------------+
|Microtask Queue|
+---------------+
|  promise.then |
|  queueMicro...|
|   async/await |
+---------------+
          |
          | (After call stack is empty)
          V
+---------------+
|   Call Stack  |
+---------------+
|   foo()       |
|   bar()       |
| promiseChain()|
+---------------+

(Color legend:
Red: Web APIs
Green: Callback Queue
Blue: Microtask Queue
Black: Call Stack)