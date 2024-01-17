I came across this very simple and brilliant [article](https://www.freecodecamp.org/news/javascript-engine-and-runtime-explained/) about how JS Engine and Runtime works

Highly recommend to [read](https://www.freecodecamp.org/news/javascript-engine-and-runtime-explained/) it yourself

It explains it so well, I'll just add my summary of the article with some additonal research on the topic

So, 
## What's JS Engine? 
> A JavaScript engine is simply a computer program that executes JavaScript code. It's responsible for translating human-readable JavaScript code into machine-readable instructions that the computer's hardware can execute.

 Some of the popular ones include:
  - V8 (used in Google Chrome)
  - SpiderMonkey (used in Mozilla Firefox)
  - JavaScriptCore (used in Safari):
  - Chakra (used in Microsoft Edge):


### Js engine has two components : 

**Call Stack** and **Heap**

- In CallStack our code gets executed, it manages the order in which functions are called, each new function is added on top (stack data structure (Last In First Out)), when fnished execusion, its removed from top, and function below are left to be executed
- Heap is something like an open space where you can store things. In the case of JavaScript, it's where the computer allocates memory for variables and objects.

 


