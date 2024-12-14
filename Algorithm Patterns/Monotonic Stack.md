# Monotonic Stacks

A Monotonic Stack is a stack data structure that keeps its elements in a specific order—either increasing or decreasing. The order is maintained by applying specific rules during the push and pop operations. This makes Monotonic Stacks useful for solving problems like finding the next greater or smaller element in an array efficiently.


## Types of Monotonic Stacks

### Monotonically Increasing Stack
This stack maintains elements in **ascending order** from bottom to top.

#### Explained
Here, every new element that's pushed onto the stack is greater than or equal to the element below it. 
If a new element is smaller, we pop the elements from the top of the stack until we find an element smaller than or equal to the new element, or the stack is empty. 
This way, the stack always maintains an increasing order.

![image](https://github.com/user-attachments/assets/bf0118d0-f814-463b-972f-5e02534dc6f9)

#### Code Template for Monotonically Increasing Stack

```python
stack = []
for element in array:
    while stack and stack[-1] > element:
        stack.pop()
    stack.append(element)


```

### Monotonically Decreasing Stack
This stack maintains elements in **descending order** from bottom to top.

#### Explained
When a new element arrives, if it's larger than the element on the top, we keep popping the elements from the stack until we find an element that's larger than or equal to the new element, or the stack is empty. 
This ensures that the stack always maintains a decreasing order.

![image](https://github.com/user-attachments/assets/9e60acaf-9bb7-4bce-9148-fcd38d3618e9)

#### Code Template for Monotonically Decreasing Stack

```python
stack = []
for element in array:
    while stack and stack[-1] < element:
        stack.pop()
    stack.append(element)

```

---
Each element in the input array is handled only twice (one push and one pop), making the overall **Time Complexity O(n)** for both increasing and decreasing stacks.
