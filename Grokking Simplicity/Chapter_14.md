
# Chapter 14: Updating Nested Objects with Recursion

This chapter dives into how we can update nested objects using recursion.

When working with nested data, recursive functions are more effective, whereas loops are better suited for flat data like arrays.



## Three Key Rules for Writing Recursive Functions:

1. **Always have a base case**: This is where the recursion stops.
2. **Reduce the argument**: Each recursive call should work with a reduced version of the argument.
3. **Move toward the base case**: The function should always progress toward the base case, not away from it.

![image](https://github.com/user-attachments/assets/777b40e2-84c0-421d-a7c2-8d4d78974024)


---


## Abstraction Barrier in Recursive Functions

### Functional tools for nested data
Use abstraction barrier on deeply nested data to reduce cognitive load.

Working with recursive functions can get complicated, especially when dealing with multiple arguments. In such cases, it's helpful to simplify things by replacing explicit arguments with reusable functions.

![image](https://github.com/user-attachments/assets/55d15f7e-21db-4076-8b84-b6d8acef405f)

