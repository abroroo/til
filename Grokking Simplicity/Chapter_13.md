# Chapter 13: Clarifying Chains

So, **Clarifying chains** is a refactoring technique that involves identifying logical steps within a function and either wrapping them in separate functions or naming their callbacks.

![image](https://github.com/user-attachments/assets/fba11e9c-57dd-40cb-b5a9-c002ed247bfd)

### Two Approaches:

1. **Name the Steps**:  
   - Break down each step into its own function and give it a clear name.
   
   ![image](https://github.com/user-attachments/assets/b45e9680-fd2b-4f62-b482-090cef8ff9f7)

2. **Name the Callbacks**:  
   - Keep using low-level methods like `map()` and `reduce()` but give the callbacks descriptive names.
   
   ![image](https://github.com/user-attachments/assets/04a88a58-a11d-49ae-b756-f1cb24517d85)

### Comparison:

- **Naming the Callbacks**: This approach can be clearer because it shows that the main function is using methods like `map()` and `reduce()`, giving a better understanding of the implementation.
- **Naming the Steps**: While this method might make the code more abstract, it could hide the quick understanding of how the function works at a glance.

