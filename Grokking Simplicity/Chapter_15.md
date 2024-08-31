# Chapter 15 : 

The code can be put into a diagrom of timelines to see how each function(action types only) gets called. 

_**Timelines are importatnt when functions read or modify global variables, which may lead to wrong result because of sharing same gloabal variable.**_ 

![image](https://github.com/user-attachments/assets/30e3c8a8-3ae4-43ee-8a99-573a542f98ed)


## Timelines

This is how **Syncronyous** code timeline: 

![image](https://github.com/user-attachments/assets/2b74ff95-d0de-4f1a-9226-eca687691c8c)


This is how **Asynchronuous** code timeline would look like: 

![image](https://github.com/user-attachments/assets/044f7acb-eb36-49ba-90d7-c0ee87eb4bc0)
![image](https://github.com/user-attachments/assets/90416a97-4d95-45b0-a47b-4dacb5cd65ae)



### Improtant to note that!

In a sequential program, instructions usually execute one after the other, in a single straight line.
However, if two sequences of code (like two threads) are running concurrently, the instructions from these sequences might get "interleaved," meaning that a few instructions from one sequence might execute, then a few from another, and so on.

**For example** 

![image](https://github.com/user-attachments/assets/3d1e6341-4caf-45dd-ac00-b73dd1e1ad5a)
![image](https://github.com/user-attachments/assets/4f5485f3-bf4e-4a71-ba97-7b1da462025e)
![image](https://github.com/user-attachments/assets/27c29ad1-f0c3-4df0-8566-f5594091f3d8)

However, in some circumstances, we can prevent inter-leaving. For example, in JavaScript’s threading model, synchronous actions don’t interleave.

![image](https://github.com/user-attachments/assets/fedd4fe2-e2e9-45f8-9c50-db845f599c4b)


## Java multi-threding(async) => Race Condition 
In the context of Java multithreading, when two threads concurrently execute the addToX method, the operations can indeed interleave in a way that might cause unexpected results.

For example 
```java
int x = 0;

public void addToX(int y) {
    x += y;
}

// Two threads execute:
addToX(4);
addToX(2);

```

![image](https://github.com/user-attachments/assets/f12ae6e0-199b-43ce-9d7f-bc77d4bb2df5)


## Javascript (Sync) vs (Async) 

Sync: 

![image](https://github.com/user-attachments/assets/01351ba6-5f65-4a12-843d-925e773db2bc)

Async: 

![image](https://github.com/user-attachments/assets/f2e5d3a8-b674-4eda-949d-7449aab21ff6)


# [Javascript Async] Principle

![image](https://github.com/user-attachments/assets/75e552b5-2013-42b4-b763-081ab7e4f6c2)

We can’t return values from asynchronous calls. Asynchronous calls return immediately, but the value won’t be generated until later, when the callback is called. You can’t get a value out in the normal way, as you would with synchronous functions. The way to get a value out in asynchronous calls is with a call-
back. You pass a callback as an argument, and you call that call-back with the value you need. This is standard JavaScript asynchronous programming.





