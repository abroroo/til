
# Chapter 8: Stratified Design

The idea here is to group functions into different levels, or layers, to isolate them from each other and reduce or eliminate side effects. Each function should be as independent as possible.

## Four Approaches to Stratified Design:

1. **Straightforward Implementation**
2. **Abstraction Barrier**
3. **Minimal Interface**
4. **Comfortable Layers**

In this chapter, we focus on **Straightforward Implementation**.

## Straightforward Implementation:

- **Low-Level Code**: Place low-level code (like `for` loops, array indexing, etc.) at the bottom layer.
- **Utility Functions**: These go on the second layer, using the low-level code within them.
- **Focused Utility Functions**: Next, create more specific utility functions that rely on the general utility functions but avoid using low-level code directly.
- **Business Logic**: Finally, at the top level, write business logic functions that only use the focused utility functions, not the lower layers.
  
![image](https://github.com/user-attachments/assets/14a6df74-cf5c-4a6b-8ab7-efbeb80d6824)


### The Big Rule:

Each layer should only use functions from the layer right below it. So, the top layer should only use the layer directly underneath, and so on. Don’t skip layers—this helps keep everything neat and reduces side effects.


![image](https://github.com/user-attachments/assets/4e8811a3-93f7-407f-a656-16f0cb99db61)
