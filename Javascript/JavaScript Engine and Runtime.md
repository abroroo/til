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

- CallStack - is where our code gets executed, it manages the order in which functions are called, each new __function__ (Execution Context) is added on top (stack data structure (Last In First Out)), when fnished execusion, its removed from top, and function below is next to be executed
  
- Heap - is something like an open space where you can store things. In the case of JavaScript, it's where the computer allocates memory for variables and objects.

![](https://www.freecodecamp.org/news/content/images/2024/01/js_engine.png)

### **Compiliation** vs **Interpretation** 

- In **Compilation**, all of the code is converted into machine code at once and written in a binary file later to be executed by hardware

- In **Interpretation**, code still needs to get converted into binary code, but this time it is happening line by line simultaneously executing that line by hardware.

 ## How Javascript gets converted into hardware-readable (binary) code?


