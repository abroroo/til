# Chapter 15 : Timelines

The code can be put into a diagrom of timelines to see how each function(action types only) gets called. 

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


### Java multi-threding(async) => Race Condition 
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

![image](https://github.com/user-attachments/assets/775ad344-31d8-471d-a923-067b1483a6d9)





