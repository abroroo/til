
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

Example: 

 Imagine a recursive function that processes nested arrays:
    
  ```js
    function sumNested(arr) {
        let total = 0;
        for (let element of arr) {
            if (Array.isArray(element)) {
                total += sumNested(element); // Recursive call
            } else {
                total += element;
            }
        }
        return total;
    }
  ```


  Instead of repeatedly handling the complexity of checking if an element is an array and summing it, you could create an abstraction barrier:
    
  ```javascript
    
    function processElement(element, recursiveFunction) {
        return Array.isArray(element) ? recursiveFunction(element) : element;
    }

    function sumNested(arr) {
        let total = 0;
        for (let element of arr) {
            total += processElement(element, sumNested); // Abstraction barrier
        }
        return total;
    }
    
  ```

We could also create a util function for nested arrays: 

```js

    let total = 0; 
    
    function sum(num) {
        total += num; 
    }



    function processNestedArray(data, action) {
        for (let element of data) {
            if (Array.isArray(element)) {
                processNestedData(element, action);
            } else {
                action(element);
            }
        }
    }


    // Now, you can call it with any action:
    processNestedArray(data, sum);
    ```


```





![image](https://github.com/user-attachments/assets/55d15f7e-21db-4076-8b84-b6d8acef405f)

