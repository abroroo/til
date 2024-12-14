# Monotonic Stacks

A Monotonic Stack is a special kind of stack, which maintains its elements in a specific order. 
Unlike a traditional stack, where elements are placed on top of one another based on when they arrive, a Monotonic Stack ensures that the elements inside the stack remain in an increasing or decreasing order. 
This is achieved by enforcing specific push and pop rules, depending on whether we want an increasing or decreasing monotonic stack.


## Types of Monotonic Stacks

### Monotonically Increasing Stack
A Monotonically Increasing Stack is a stack where elements are arranged in an ascending order from the bottom to the top. 
Here, every new element that's pushed onto the stack is greater than or equal to the element below it. 
If a new element is smaller, we pop the elements from the top of the stack until we find an element smaller than or equal to the new element, or the stack is empty. 
This way, the stack always maintains an increasing order.

![image](https://github.com/user-attachments/assets/bf0118d0-f814-463b-972f-5e02534dc6f9)

#### Code Template for Monotonically Increasing Stack

```python
create an empty stack
for each element in the array:
    while stack is not empty AND top of stack is more than the current element:
        pop the stack
    push the current element to stack

```

### Monotonically Decreasing Stack
Conversely, a Monotonically Decreasing Stack is a stack where elements are arranged in a descending order from the bottom to the top. 
When a new element arrives, if it's larger than the element on the top, we keep popping the elements from the stack until we find an element that's larger than or equal to the new element, or the stack is empty. 
This ensures that the stack always maintains a decreasing order.

![image](https://github.com/user-attachments/assets/9e60acaf-9bb7-4bce-9148-fcd38d3618e9)

#### Code Template for Monotonically Decreasing Stack

```python
create an empty stack
for each element in the array:
    while stack is not empty AND top of stack is less than the current element:
        pop the stack
    push the current element to stack

```

---
Each element in the input array is handled only twice (one push and one pop), making the overall **Time Complexity O(n)** for both increasing and decreasing stacks.
