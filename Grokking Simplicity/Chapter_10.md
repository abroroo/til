# Chapter 10: First-Class Functions

In this chapter, the concept of "first-class functions" is introduced. The idea is that functions in programming aren't just limited to one specific use. Unlike variables that are only for storing values, or loops that follow a particular structure, functions are incredibly versatile.

### What Can First-Class Functions Do?

- **Assigned to variables:** You can store functions in variables, just like any other value.
- **Passed as arguments:** Functions can be passed as arguments to other functions, which opens up a lot of flexibility.
- **Returned from other functions:** A function can return another function, making it easy to create flexible and reusable code.
- **Stored in data structures:** Functions can be stored in arrays, objects, or other data structures, just like any other data type.

### Making Implicit Arguments Explicit

Sometimes, you might find different functions that are almost identical except for their names. These functions have what's called "implicit arguments." Instead of having multiple similar functions, you can create one general function and pass in the varying parts as explicit arguments. This makes your code more reusable and easier to manage.




![image](https://github.com/user-attachments/assets/74c99c38-ca2f-4b6d-9229-9015e49ddd78)

---

**Can be simplified as:**  



![image](https://github.com/user-attachments/assets/207f27ca-94a0-450d-88c2-576f1c942545)

    
---

## Replace body with a callback function

- *Identify the before, body and after sections.*
  
  ![image](https://github.com/user-attachments/assets/cfdf5332-3314-4f78-a8c5-abb78cf8a819)

- *Extract the whole thing into a function*
  
  ![image](https://github.com/user-attachments/assets/55eaf407-74ca-40f9-b034-6174712eefc7)





---

## Summary

- **First-class values** are anything that can be stored in a variable, passed as an argument, and returned from functions. A first-class value can be manipulated by code.
  
- Many parts of a language are not first-class. We can wrap those parts in functions that do the same thing to make them first-class.
  
- Some languages have first-class functions that let you treat functions as first-class values. First-class functions are necessary for this level of functional programming.
  
- **Higher-order functions** are functions that take other functions as arguments (or that return a function). Higher-order functions let us abstract over varying behavior.
  
- **Implicit argument in function name** is a code smell where the difference between functions is named in the function name. We can apply an explicit argument to make the argument first-class instead of an inaccessible part of the function name.
  
- We can apply the refactoring technique called **replace body with callback** to abstract over behavior. It creates a first-class function argument that represents the behavioral difference between two functions.

---
