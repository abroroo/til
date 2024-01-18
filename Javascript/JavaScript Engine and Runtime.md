I came across this very simple and brilliant [article](https://www.freecodecamp.org/news/javascript-engine-and-runtime-explained/) about how JS Engine and Runtime works

Highly recommend to [read](https://www.freecodecamp.org/news/javascript-engine-and-runtime-explained/) it yourself

It explains it so well, I'll just add my summary of the article with some additonal research on the topic

# You gotta understand some concepts first

When you write JavaScript code and run it in a browser, the code doesn't directly interact with your computer's hardware. Instead, it interacts with the **JavaScript engine**, which converts JS code into hardware readable binary code.

 > Some of the popular engines include:
 > - V8 (used in Google Chrome)
 > - SpiderMonkey (used in Mozilla Firefox)
 > - JavaScriptCore (used in Safari):
 > - Chakra (used in Microsoft Edge):


### JS Engine has two components : 

**Call Stack** and **Heap**

- CallStack - is where our code gets executed, it manages the order in which functions are called, each new __function__ (Execution Context) is added on top (stack data structure (Last In First Out)), when finished execusion its removed from top, and the function below is next to be executed
  
- Heap - is something like an open space where you can store things. In the case of JavaScript, it's where the computer allocates memory for variables and objects.

<img src="https://www.freecodecamp.org/news/content/images/2024/01/js_engine.png" width="600" height="400">

### **Compiliation** vs **Interpretation** 

- In **Compilation**, all of the code is converted into machine code first(written in a binary file) then it can be executed by hardware when needed. It is mostly refered as AOT - Ahead-Of-Time compiliation

- In **Interpretation**, code still needs to get converted into binary code, but this time it is happening line by line simultaneously executing that line by hardware.

#### Why need to know it? 
Well we know that JS is a purely interpreted language. 

But the modern JS engine now uses a mix of compilation and interpretation which is known as "just-in-time" (JIT) compilation.

JS engine uses JIT, where only the specific parts of the code that are needed for execution are translated into machine code and executed by the hardware right away. 

We'are done with the concepts, now let's get to the process 


 ## How actually Javascript gets converted into hardware-readable (binary) code?

1. Whenever a piece of JavaScript code enters the engine, the first step is to parse the code. 

   During this parsing process, the code is parsed into a data structure called the AST (Abstract Syntax Tree). This step also checks if there are any syntax errors. 

   You don't need to know or understand how AST works, just for curiosity you can play around in [here](https://astexplorer.net/#/gist/8db37db99b4a20190a348d92618df357/fb9a6139ecd6f9c515bd5c20d165cd6dd4a2a425), to see how JS code looks like in AST.

2. The next step is compilation. Here the engine takes the AST and compiles it to machine code.
3. Then, this machine code gets executed immediately because its using JIT – remember that this execution happens in the call stack.
   > The initial machine code generated might not be the most optimized for performance. The engine might prioritize quick execution over highly optimized code at this stage to start running the program as fast as possible.
   > 
   > Once the program is running, the JavaScript engine doesn't stop there. It continues to work in the background to optimize the code further.
   > 
4. The engine takes the already pre-compiled code that is currently running and applies optimizations to make it more efficient.
   > It does things like reordering instructions, inlining functions, or removing unnecessary operations 
