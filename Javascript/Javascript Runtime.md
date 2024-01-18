First you need to know how Javascript Engine works

If you are not familiar with it, I recommend to read this [article](https://www.freecodecamp.org/news/javascript-engine-and-runtime-explained/), I've also summirezed its contents in [here](https://github.com/abroroo/til/blob/main/Javascript/JavaScript%20Engine.md)


# What's Javascript Runtime? 

> JS runtime is an ecosystem of components working together to facilitate the execution of JavaScript applications

JavaScript runtime is like a manager that handles your code's tasks, stores information, translates and runs code on the spot, uses special helpers for certain jobs, 
keeps things moving smoothly, and always looks for ways to make your code work better.

Depending on where JavaScript is running (the web browser or server-side with Node.js), there might be additional environment-specific features in the runtime. 
For instance, in a browser, there could be features related to handling browser events, accessing the DOM, and interacting with browser-specific functionalities.

#### We particularly focus on JS runtime in the browser

Just think of a JS runtime as a big box that includes all the things we need to run JavaScript in the browser.

<img src="https://www.freecodecamp.org/news/content/images/2024/01/JS_runtime_1.png" width="400" height="250" />

 - The core of a JS runtime is the __JS engine__.

 - JS runtimes, especially in the context of web browsers, come with __Web APIs__. 

     - Web APIs are functionalities that are provided to the engine but they are not a part of the JavaScript language itself. JavaScript gets access to these APIs through the `window` object.

 - Asynchronous operations in JavaScript, such as handling user input or making network requests, utilize callback functions. These functions are placed in a queue known as the __Callback Queue__, awaiting execution.

<img src="https://www.freecodecamp.org/news/content/images/2024/01/JS_runtime_4.png" width="400" height="250" />


# How JS Runtime works behind the scenes?

Let's take as an example *button click handler* function and see how it is executed by JS Runtime

1. First, after the `click` event occurs, the callback function `CLICK` is put into the callback queue.
   
     <img src="https://www.freecodecamp.org/news/content/images/2024/01/JS_runtime_5.png" width="400" height="250" />

2. Then, when the call stack is empty, the callback queue gets passed to the call stack so that it can be executed and this happens by something called the Event Loop.

   <img src="https://www.freecodecamp.org/news/content/images/2024/01/JS_runtime_7.png" width="400" height="250" />

    So, in short, the event loop takes callback functions from the callback queue and puts it into the call stack, so that it can be executed.
   
